
# 🔐 Laboratório: Armazenamento de Autoridade de Certificação

## 1. Objetivo
Verificar certificados digitais HTTPS utilizando OpenSSL e compreender a função das Autoridades Certificadoras (CA) na segurança das conexões.

## 2. Conceitos importantes

**Autoridade Certificadora (CA)**
É uma entidade responsável por emitir e assinar certificados digitais, confirmando a identidade de sites e servidores.

**Certificado digital**
É um documento eletrônico que identifica um servidor e permite estabelecer uma conexão HTTPS segura.

**Fingerprint (impressão digital)**
É uma sequência de caracteres calculada a partir do certificado por um algoritmo hash. Funciona como uma identificação do certificado.

**SHA-1**
É um algoritmo hash utilizado neste laboratório para calcular a impressão digital. Atualmente, é considerado ultrapassado para aplicações de segurança.

**Proxy HTTPS**
É um intermediário entre o computador e o site. Para inspecionar o tráfego HTTPS, pode atuar como intermediário TLS, utilizando um certificado próprio confiável pelo computador.

## 3. Ferramentas utilizadas

- Linux (Cybersecurity LabVM)
- OpenSSL
- Terminal
- Protocolo HTTPS
- Porta 443

## 4. Comandos executados

### Verificar a versão do OpenSSL
```bash
openssl version
```

Resultado: OpenSSL 3.0.2.

### Configurar o teclado
```bash
setxkbmap -model abnt2 -layout br
```

### Obter o certificado HTTPS da Cisco
```bash
echo -n | openssl s_client -connect cisco.com:443 | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > ./cisco.pem
```

### Calcular a impressão digital SHA-1
```bash
openssl x509 -noout -in cisco.pem -fingerprint -sha1
```

Resultado obtido na máquina virtual:

```text
9F:3A:B4:7A:43:CB:0B:A6:DE:2A:CB:D4:74:ED:54:7D:A5:6B:C6:53
```

## 5. O que foi analisado?

O comando OpenSSL estabeleceu uma conexão com o servidor Cisco pela porta 443 e obteve seu certificado digital.

Depois, o certificado foi armazenado no arquivo cisco.pem.

Por último, utilizamos o OpenSSL para calcular sua impressão digital SHA-1.

## 6. Comparação dos certificados

A atividade propôs comparar a impressão digital obtida diretamente do site com aquela obtida pela máquina virtual.

- Impressões digitais iguais: indicam que os certificados comparados são iguais.
- Impressões digitais diferentes: podem indicar certificados diferentes, inclusive devido à presença de um proxy HTTPS ou à atualização dos certificados.

A comparação deve considerar o mesmo certificado e o mesmo algoritmo hash.

## 7. Proxy HTTPS: pergunta de reflexão

Para um proxy HTTPS funcionar realizando inspeção do tráfego criptografado, é necessário que ele consiga interceptar e estabelecer conexões TLS com o cliente e com o servidor.

O computador precisa confiar na Autoridade Certificadora utilizada pelo proxy, por meio da instalação de seu certificado raiz como confiável.

## 8. O que aprendi neste laboratório?

- Verificar a versão do OpenSSL.
- Utilizar comandos no terminal Linux.
- Estabelecer conexões HTTPS pela porta 443.
- Obter e armazenar certificados digitais.
- Calcular fingerprints com SHA-1.
- Compreender a função das Autoridades Certificadoras.
- Identificar como um proxy HTTPS pode interferir na validação dos certificados.

## 9. Conclusão

Este laboratório permitiu compreender, na prática, como os certificados digitais ajudam a proteger as conexões HTTPS e como o OpenSSL pode ser utilizado para analisar certificados e verificar suas impressões digitais.

**Área:** Segurança da Informação  
**Projeto:** Defesa Cibernética  
**Laboratório:** Autoridades de Certificação (PKI)

