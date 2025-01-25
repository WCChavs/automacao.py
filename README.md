# automacao.py


# Projeto de Automação de Cadastro de Produtos

Este projeto foi desenvolvido durante um curso intensivo da hashtag, com o objetivo de automatizar o processo de login e cadastro de produtos em um sistema da empresa, utilizando Python e a biblioteca `pyautogui` para automação de tarefas repetitivas em uma interface gráfica.

## Descrição do Projeto

O script automatiza as seguintes etapas:

1. **Acesso ao sistema**: O script abre o navegador, acessa a URL do sistema da empresa e realiza o login com um email e senha fornecidos.
2. **Importação de dados**: Carrega uma base de dados (um arquivo CSV com informações dos produtos).
3. **Cadastro de produtos**: Preenche automaticamente os campos do formulário de cadastro de produtos, utilizando as informações da base de dados.
4. **Repetição do processo**: O script repete o processo para todos os produtos na base de dados.

## Requisitos

- Python 3.x
- Bibliotecas:
  - `pyautogui` (para automação de cliques e digitação)
  - `pandas` (para manipulação de dados em formato CSV)
  
Você pode instalar as dependências utilizando o comando:
```bash
pip install pyautogui pandas
```

## Como Utilizar

### Passo 1: Acesso ao Sistema

O primeiro passo do script é abrir o navegador Google Chrome e acessar o link de login fornecido.

```python
pyautogui.press("win")
pyautogui.write("chrome")
pyautogui.press("enter")
pyautogui.write("https://dlp.hashtagtreinamentos.com/python/intensivao/login")
pyautogui.press("enter")
```

### Passo 2: Login

O script realiza o login no sistema, preenchendo os campos de email e senha, e clicando no botão de login.

```python
pyautogui.click(x=510, y=424)  # Clica no campo de email
pyautogui.write("pythonimpressionador@gmail.com")  # Preenche o email
pyautogui.press("tab")  # Passa para o próximo campo
pyautogui.write("sua senha")  # Preenche a senha
pyautogui.click(x=678, y=592)  # Clica no botão de login
```

### Passo 3: Importação da Base de Produtos

A base de dados dos produtos é carregada de um arquivo CSV utilizando a biblioteca `pandas`. Este arquivo deve conter as colunas `codigo`, `marca`, `tipo`, `categoria`, `preco_unitario`, `custo` e `obs`.

```python
import pandas

tabela = pandas.read_csv("produtos.csv")
print(tabela)
```

### Passo 4: Cadastro de Produtos

O script percorre cada linha da base de dados e preenche os campos correspondentes no formulário de cadastro de produtos.

```python
for linha in tabela.index:
    pyautogui.click(x=653, y=294)  # Clica no campo de código
    codigo = tabela.loc[linha, "codigo"]
    pyautogui.write(str(codigo))  # Preenche o campo de código
    pyautogui.press("tab")  # Passa para o próximo campo
    pyautogui.write(str(tabela.loc[linha, "marca"]))  # Preenche o campo de marca
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha, "tipo"]))  # Preenche o campo de tipo
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha, "categoria"]))  # Preenche o campo de categoria
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha, "preco_unitario"]))  # Preenche o campo de preço unitário
    pyautogui.press("tab")
    pyautogui.write(str(tabela.loc[linha, "custo"]))  # Preenche o campo de custo
    pyautogui.press("tab")
    obs = tabela.loc[linha, "obs"]
    if obs != 'nam':
        pyautogui.write(str(tabela.loc[linha, "obs"]))  # Preenche o campo de observações
    pyautogui.press("tab")
    pyautogui.press("enter")  # Clica no botão de enviar
    pyautogui.scroll(5000)  # Rola para cima para limpar os campos
```

### Passo 5: Repetição do Processo

O processo de cadastro é repetido até que todos os produtos da base de dados sejam cadastrados no sistema.

## Observações

- **Coordenadas de clique**: O script usa coordenadas fixas na tela (ex: `pyautogui.click(x=653, y=294)`) para localizar os campos de preenchimento. Certifique-se de que sua resolução de tela seja compatível com as coordenadas fornecidas ou ajuste-as conforme necessário.
- **Arquivo CSV**: O arquivo `produtos.csv` deve estar no mesmo diretório do script e deve conter as informações de cada produto a ser cadastrado.
- **Sincronização e espera**: O script utiliza `time.sleep(3)` em alguns pontos para garantir que a página ou o sistema tenha tempo suficiente para carregar antes de continuar.

## Conclusão

Este projeto exemplifica como a automação pode ser utilizada para reduzir o tempo gasto com tarefas repetitivas e minimizar erros humanos, aumentando a eficiência dos processos. É uma ótima maneira de aprender como interagir com a interface gráfica do usuário usando Python e `pyautogui`.
