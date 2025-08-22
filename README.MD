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


