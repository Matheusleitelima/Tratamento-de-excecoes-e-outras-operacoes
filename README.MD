# 🛠️ Tratamento de Exceções na Manipulação de Arquivos em Python

Durante a manipulação de arquivos, problemas como arquivos inexistentes ou falta de permissões são comuns e só podem ser detectados em tempo de execução. Sem tratamento adequado, essas exceções podem interromper o programa e comprometer a experiência do usuário e a integridade dos dados.

---

## 📌 Conceito de Exceção

Quando ocorre um problema inesperado que o interpretador Python não consegue resolver, dizemos que houve uma **exceção**.  
Exemplos comuns em manipulação de arquivos:

- **FileNotFoundError** → arquivo não existe.  
- **PermissionError** → sem permissão de acesso.  
- **FileExistsError** → tentativa de criar arquivo ou diretório já existente.  

> Praticamente todas as exceções herdam da classe `Exception`. Quanto mais específica a exceção, melhor é o tratamento.

---

## 🧑‍💻 Tratando Exceções com `try` / `except`

A sintaxe básica:

```python
try:
    # Código que pode gerar erro
except TipoDeErro as erro:
    # Código que será executado caso ocorra a exceção
```

- O código crítico vai dentro do `try`.  
- O código alternativo ou de aviso vai dentro do `except`.  
- Podemos ter **múltiplos excepts** para diferentes tipos de exceção.

---

## 🔹 Exemplo 1: Arquivo inexistente

```python
try:
    with open("teste.txt", "r") as arquivo:
        conteudo = arquivo.read()
except FileNotFoundError as erro:
    print("Arquivo inexistente.")
    print("Detalhes do erro:", erro)
```

**Explicação:**

1. Tentamos abrir o arquivo `teste.txt` para leitura.  
2. Como ele não existe, o Python lança `FileNotFoundError`.  
3. O código dentro do `except` é executado, exibindo uma mensagem amigável e os detalhes do erro.  

---

## 🔹 Exemplo 2: Arquivo sem permissão

```python
try:
    with open("teste.pdf", "w") as arquivo:
        arquivo.write("Conteúdo qualquer")
except PermissionError as erro:
    print("Sem permissão para acessar o arquivo.")
    print("Detalhes do erro:", erro)
```

**Explicação:**

- Tentamos abrir o arquivo `teste.pdf` para escrita.  
- Se o arquivo estiver aberto em outro programa ou sem permissão, Python lança `PermissionError`.  
- O fluxo pula para o `except` correspondente, evitando que o programa quebre.

---

## ⚠️ Boas práticas

- **Use exceções específicas** sempre que possível (`FileNotFoundError`, `PermissionError`).  
- Evite capturar exceções genéricas como `Exception`, pois podem silenciar erros inesperados.  
- Consulte a documentação das funções que você utiliza para identificar quais exceções podem ser lançadas.  

---

## 🔹 Hierarquia de exceções relacionadas a arquivos

```
Exception
 └── OSError
      ├── FileNotFoundError
      ├── PermissionError
      └── FileExistsError
```

---

## 🎯 Objetivo educacional

- Garantir que o programa continue rodando mesmo em situações de erro.  
- Fornecer mensagens claras ao usuário sobre o problema.  
- Tornar o código mais robusto e confiável.  

---

> Observação: O tratamento de exceções é essencial em qualquer aplicação real que manipule arquivos, evitando travamentos e perda de dados.



# Operações Adicionais em Arquivos com Python

Conhecer as operações com arquivos em Python é fundamental para qualquer desenvolvedor que lide com manipulação de dados. Além da leitura e escrita, operações como **remoção** e **renomeação** de arquivos são essenciais para automatizar tarefas, organizar informações e manter a integridade dos dados.

Compreender como realizar essas operações de forma eficiente e segura permite desenvolver aplicações mais robustas e confiáveis, evitando problemas como perda de dados ou interrupções inesperadas do programa.

---

## Conteúdo

1. [Remover Arquivos](#remover-arquivos)  
2. [Renomear Arquivos](#renomear-arquivos)  
3. [Exceções Comuns](#exceções-comuns)  
4. [Dicas](#dicas)  

---

## Remover Arquivos

Para remover um arquivo, utilizamos a função `remove` do módulo `os`.

**Sintaxe:**

```python
import os

os.remove(caminho)
```

- `caminho`: caminho para o arquivo que desejamos remover.  

Para remover diretórios, usamos a função `rmdir` em vez de `remove`.

**Exemplo:**

```python
import os

# Remover arquivo teste.txt no mesmo diretório
os.remove("teste.txt")
```

---

## Renomear Arquivos

Para renomear arquivos, utilizamos a função `rename` do módulo `os`.

**Sintaxe:**

```python
import os

os.rename(origem, destino)
```

- `origem`: caminho do arquivo atual  
- `destino`: novo nome ou caminho do arquivo  

**Exemplo:**

```python
import os

# Renomear teste_alfa.txt para teste_beta.txt
os.rename("teste_alfa.txt", "teste_beta.txt")
```

---

## Exceções Comuns

### Função `remove`

- `FileNotFoundError`: arquivo não existe  
- `PermissionError`: sem permissão para alterar o arquivo  
- `IsADirectoryError`: tentamos remover um diretório com `remove`  

### Função `rename`

- `FileNotFoundError`: arquivo de origem não existe  
- `FileExistsError`: arquivo de destino já existe  
- `PermissionError`: sem permissão para alterar o arquivo de origem ou criar o destino  

---

## Dicas

- Para renomear **sobrescrevendo o arquivo destino**, caso ele exista, podemos usar a função `replace` do módulo `os`.  

```python
import os

os.replace("teste_alfa.txt", "teste_beta.txt")
```

- Sempre trate exceções para evitar que seu programa seja interrompido inesperadamente.

# Manipulação de Diretórios com Python

Conhecer operações com diretórios em Python é essencial para organizar e gerenciar dados em projetos. Essas operações incluem **criação**, **remoção** e **listagem de diretórios**, permitindo uma estruturação adequada dos arquivos.

O domínio dessas técnicas facilita a automação de tarefas, melhora a manutenção do sistema e garante um ambiente de trabalho mais organizado e eficiente.

---

## Conteúdo

1. [Criando e Removendo Diretórios](#criando-e-removendo-diretórios)  
2. [Tratando Exceções Comuns](#tratando-exceções-comuns)  
3. [Listando Conteúdo de Diretórios](#listando-conteúdo-de-diretórios)  

---

## Criando e Removendo Diretórios

Para **criar** um diretório, utilizamos a função `mkdir` do módulo `os`.  
Para **remover** um diretório, utilizamos a função `rmdir` do módulo `os`.

**Sintaxe:**

```python
import os

# Criar diretório
os.mkdir("meu_diretorio")

# Remover diretório
os.rmdir("meu_diretorio")
```

**Exemplo:**

```python
import os

# Criar diretório
os.mkdir("meu_diretorio")
print("Diretório criado!")

# Remover diretório
os.rmdir("meu_diretorio")
print("Diretório removido!")
```

---

## Tratando Exceções Comuns

Ao criar ou remover diretórios, podem ocorrer exceções:

### Criação de diretórios (`mkdir`)

- `PermissionError`: sem permissão para criar o diretório  
- `FileExistsError`: diretório já existe  

### Remoção de diretórios (`rmdir`)

- `PermissionError`: sem permissão para remover  
- `FileNotFoundError`: diretório não existe  
- `OSError`: diretório não está vazio  

**Exemplo com `OSError` e módulo `errno`:**

```python
import os
import errno

try:
    os.rmdir("meu_diretorio")
except OSError as erro:
    print("Número do erro:", erro.errno)
    if erro.errno == errno.ENOTEMPTY:
        print("Erro: Diretório não está vazio!")
```

> Observação: a exceção `OSError` é mais abrangente e deve ser tratada por último.

---

## Listando Conteúdo de Diretórios

Para listar arquivos e subdiretórios de um diretório, utilizamos `os.scandir`.

**Sintaxe:**

```python
import os

with os.scandir("meu_diretorio") as entradas:
    for entrada in entradas:
        print(entrada.name, "-> Diretório" if entrada.is_dir() else "-> Arquivo")
```

- `entrada.name`: nome do arquivo ou diretório  
- `entrada.path`: caminho completo  
- `entrada.is_dir()`: verifica se é diretório  
- `entrada.is_file()`: verifica se é arquivo  
- `entrada.stat()`: retorna atributos como tamanho, data de modificação, etc.

**Exemplo:**

```python
import os

os.mkdir("meu_diretorio")  # criando para exemplo
with open("meu_diretorio/arquivo1.txt", "w") as f:
    f.write("Olá!")

with os.scandir("meu_diretorio") as entradas:
    for entrada in entradas:
        tipo = "Diretório" if entrada.is_dir() else "Arquivo"
        print(entrada.name, "->", tipo)
```

---

Este README oferece um guia completo para criar, remover e listar diretórios em Python, tratando exceções comuns e garantindo um código mais robusto e organizado.

# 📂 Exceções e o módulo `os` em Python

## 📌 Introdução
A capacidade de ler, processar e escrever dados de maneira eficiente é importante para inúmeras aplicações, como processamento de dados, geração de relatórios e automação de tarefas.

Além disso, o tratamento de exceções garante que o código seja **robusto** e capaz de lidar com situações inesperadas, como arquivos inexistentes ou falta de permissões, aumentando a confiabilidade e a resiliência das aplicações.

A prática de ler um arquivo de texto, adicionar um cabeçalho e escrever o conteúdo em um novo arquivo permite aos desenvolvedores entenderem a importância de manipular arquivos de forma segura.  
Compreender como tratar exceções específicas, como `FileNotFoundError` e `PermissionError`, ajuda a criar scripts que não falhem inesperadamente, proporcionando uma experiência de usuário mais estável e profissional.

Ao dominar essas técnicas, você poderá criar soluções automatizadas que requerem manipulação de arquivos, essenciais em diversos campos da tecnologia.

Neste exemplo, veremos uma situação prática para tratamento de exceções em leitura e escrita de arquivos. Adicionalmente, empregaremos o módulo **`os`**, presente na biblioteca padrão do Python e amplamente utilizado para referenciar caminhos no sistema operacional.

---

## 🎯 Situação-problema
Você foi contratado por uma empresa para desenvolver um script em Python que automatize a organização de arquivos de texto.  

A tarefa envolve:
- Ler o conteúdo de arquivos
- Processar as informações
- Escrever em novos arquivos
- Tratar exceções que possam surgir (como arquivos inexistentes ou falta de permissões)

---

## 📝 Tarefa
Implemente um script em Python que realize as seguintes operações:

1. Leia o conteúdo de um arquivo de texto.  
2. Escreva o conteúdo lido em um novo arquivo, adicionando uma linha de cabeçalho.  
3. Trate possíveis exceções durante as operações, exibindo mensagens informativas ao usuário.  

---

## 🛠️ Resolução

### Passo 1: Preparação
Crie um diretório de trabalho e coloque alguns arquivos de texto de exemplo (`.txt`) nesse diretório.

### Passo 2: Estrutura do código
Importe o módulo necessário:

```python
import os
```

### Passo 3: Função para ler e escrever arquivos
Crie uma função para ler o conteúdo de um arquivo e escrever em um novo arquivo com uma linha de cabeçalho:

```python
def processar_arquivo(arquivo_origem, arquivo_destino):
    try:
        if not os.path.exists(arquivo_origem):
            raise FileNotFoundError(f"O arquivo '{arquivo_origem}' não foi encontrado.")

        with open(arquivo_origem, "r", encoding="utf-8") as f:
            conteudo = f.read()

        with open(arquivo_destino, "w", encoding="utf-8") as f:
            f.write("=== Arquivo processado automaticamente ===\n")
            f.write(conteudo)

        print(f"✅ Arquivo processado com sucesso! Salvo em: {os.path.abspath(arquivo_destino)}")

    except FileNotFoundError as e:
        print(f"❌ Erro: {e}")

    except PermissionError:
        print(f"❌ Erro: Sem permissão para acessar ou criar '{arquivo_destino}'.")

    except Exception as e:
        print(f"⚠️ Ocorreu um erro inesperado: {e}")
```

### Passo 4: Script principal
Defina os arquivos de origem e destino e chame a função criada:

```python
if __name__ == "__main__":
    diretorio = os.getcwd()
    arquivo_origem = os.path.join(diretorio, "arquivo_origem.txt")
    arquivo_destino = os.path.join(diretorio, "arquivo_destino.txt")

    processar_arquivo(arquivo_origem, arquivo_destino)
```

---

## ✅ Teste e validação

1. Crie um arquivo de texto chamado `arquivo_origem.txt` no diretório de trabalho e insira algum conteúdo.  
2. Execute o script e verifique se o conteúdo foi escrito em `arquivo_destino.txt` com a linha de cabeçalho adicionada.  
3. Simule diferentes exceções:
   - Renomeie o arquivo para que não seja encontrado → `FileNotFoundError`  
   - Remova permissões de escrita/leitura → `PermissionError`  

---

## 🎯 Resultado esperado
O script deve:
- Ler o conteúdo do arquivo `arquivo_origem.txt`  
- Escrever esse conteúdo em `arquivo_destino.txt` com uma linha de cabeçalho  
- Exibir mensagens informativas para qualquer exceção encontrada durante o processo  

---


# Organização de Arquivos por Extensão

## Descrição

Este projeto tem como objetivo a **organização automática de arquivos** em diretórios específicos de acordo com suas extensões.  
Ele utiliza os módulos `os` e `shutil` para criar diretórios (se não existirem) e mover arquivos para suas respectivas pastas.

---

## Conteúdo da Atividade (Faculdade)

Ao mover arquivos para diretórios específicos com base em suas extensões, você está aplicando conceitos de organização e automação, essenciais para a gestão eficiente de dados em projetos reais.

Além disso, o uso do módulo `shutil` para operações de movimentação e o módulo `os` para verificação e criação de diretórios são práticas comuns em tarefas de administração de sistemas e desenvolvimento de software.

Ao mover arquivos, independentemente da biblioteca ou do módulo utilizados, devemos dar atenção ao **tratamento de exceções**, garantindo que seu código seja capaz de lidar com situações inesperadas, como diretórios inexistentes ou falta de permissões.

Essa prática prepara você para enfrentar desafios mais complexos em ambientes de **Front**, onde a integridade e a organização dos dados são prioritárias. Ao compreender e implementar essas operações, você melhora a eficiência e a confiabilidade dos seus scripts, facilitando a manutenção e a escalabilidade de suas aplicações.

Neste exemplo, simulamos uma **biblioteca pública** que digitaliza documentos e salva arquivos em um diretório de trabalho.  
O objetivo é desenvolver um script que mova automaticamente esses arquivos para subdiretórios com base em suas extensões.

---

## Tarefa

- Verifique se os diretórios de destino (`pdf`, `txt`, `img`) existem; caso contrário, crie-os.  
- Mova os arquivos do diretório de trabalho para os diretórios correspondentes com base em suas extensões.  
- Trate possíveis exceções durante as operações, exibindo mensagens informativas ao usuário.

---

## Roteiro de prática

### Passo 1: Preparação
Crie um diretório de trabalho e adicione alguns arquivos de exemplo com diferentes extensões (`.pdf`, `.txt`, `.jpg`) nesse diretório.

### Passo 2: Estrutura do código
Importe os módulos necessários:
- `os`
- `shutil`

O módulo **shutil** é especialmente útil para copiar, mover, renomear e remover arquivos e diretórios.

### Passo 3: Função para criar diretórios
Crie uma função que verifique se os diretórios existem e, caso não, crie-os.

### Passo 4: Função para mover arquivos
Crie uma função que mova os arquivos para os diretórios correspondentes com base em suas extensões.

### Passo 5: Script principal
No script principal:
1. Defina o diretório de trabalho.  
2. Chame as funções criadas para organizar os arquivos.

### Passo 6: Teste e validação
1. Execute o script e verifique se os arquivos foram movidos para os diretórios corretos (`pdf`, `txt`, `img`).  
2. Simule exceções, como alterar permissões ou usar arquivos inexistentes, para validar o tratamento de erros.

---

## Resultado esperado

- Os diretórios `pdf`, `txt` e `img` devem ser criados, caso não existam.  
- Os arquivos devem ser movidos automaticamente para suas respectivas pastas com base nas extensões.  
- O script deve exibir mensagens claras em caso de erro (como permissões insuficientes ou arquivo inexistente).

---

## Exemplo de Estrutura de Pastas

```
📂 trabalho/
 ┣ 📜 documento.pdf   → 📂 pdf/
 ┣ 📜 texto.txt       → 📂 txt/
 ┣ 🖼️ imagem.jpg      → 📂 img/
```

---

## Tecnologias Utilizadas

- Python 3.8+
- Módulos nativos: `os`, `shutil`




