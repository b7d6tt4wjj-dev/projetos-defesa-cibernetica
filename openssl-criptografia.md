# Laboratório 8.1.13: Criptografia e Descriptografia com OpenSSL

## Objetivo
Praticar a criptografia e a descriptografia de arquivos utilizando OpenSSL no Ubuntu Linux.

## Ferramentas utilizadas
- Ubuntu Linux
- OpenSSL 3.5.5
- Terminal Linux

## Algoritmo utilizado
AES-256-CBC, um algoritmo de criptografia simétrica que utiliza a mesma senha para criptografar e descriptografar os dados.

## Atividades realizadas

### 1. Verificação do OpenSSL
Comando utilizado:

    openssl version

### 2. Criação do arquivo
Criei um arquivo de texto chamado `mensagem.txt` contendo uma mensagem de demonstração.

### 3. Criptografia
Comando utilizado:

    openssl enc -aes-256-cbc -salt -in mensagem.txt -out mensagem.enc

O arquivo resultante contém os dados criptografados.

### 4. Descriptografia
Comando utilizado:

    openssl enc -d -aes-256-cbc -in mensagem.enc -out mensagem_recuperada.txt

### 5. Verificação do resultado
Utilizei o comando `cat mensagem_recuperada.txt` para conferir o conteúdo recuperado.

Resultado:

    Esta e uma mensagem secreta.

## Aprendizados
- Diferença entre texto original e conteúdo criptografado.
- Uso do OpenSSL para criptografia simétrica.
- Importância de proteger a senha utilizada.
- Verificação da integridade prática do processo por meio da comparação do conteúdo recuperado com o original.

## Observação de segurança
Este foi um exercício educacional. Para aplicações reais, é importante utilizar parâmetros modernos de derivação de chave e modos de criptografia autenticada, conforme a necessidade.
