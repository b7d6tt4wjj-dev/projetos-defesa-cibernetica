# ASSINATURA DIGITAL COM OPENSSL

## 1. Objetivo
Realizar a criação e a verificação de uma assinatura digital utilizando OpenSSL e criptografia assimétrica.

## 2. Ferramentas utilizadas
- Linux (LabVM)
- OpenSSL
- Terminal
- Chaves RSA pública e privada

## 3. Arquivos utilizados
- private_key.pem: chave privada.
- public_key.pem: chave pública.
- contract.txt: documento que será assinado.
- signature: arquivo que armazena a assinatura digital.

## 4. Etapas realizadas

### Etapa 1: Verificação da chave privada
Comando:
openssl pkey -in private_key.pem -check -noout

Resultado: a chave privada foi considerada válida.

### Etapa 2: Criação do documento
Foi criado o arquivo contract.txt com uma mensagem de texto.

### Etapa 3: Geração da chave pública
Comando:
openssl pkey -in private_key.pem -pubout -out public_key.pem

### Etapa 4: Criação da assinatura digital
Comando:
openssl dgst -sha256 -sign private_key.pem -out signature contract.txt

A assinatura foi gerada utilizando a chave privada e o algoritmo SHA-256.

### Etapa 5: Verificação da assinatura
Comando:
openssl dgst -sha256 -verify public_key.pem -signature signature contract.txt

Resultado: Verified OK.

## 5. Resultado e aprendizado
A assinatura digital foi criada com sucesso e sua autenticidade foi verificada utilizando a chave pública correspondente.

O processo demonstra como a criptografia assimétrica permite verificar a integridade de um documento e confirmar que a assinatura corresponde à chave privada utilizada.

## 6. Observação de segurança
A chave privada deve ser mantida em sigilo e nunca deve ser publicada no GitHub.