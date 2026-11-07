
# POP 002 - INVESTIGAÇÃO E DIAGNÓSTICO DE DNS

**Área:** Segurança da Informação | SOC  
**Sistema operacional:** Ubuntu Linux  
**Categoria:** Análise e resolução de nomes  
**Status:** Concluído

---

## 1. OBJETIVO

Estabelecer um procedimento para investigar falhas de resolução DNS, verificar servidores configurados e analisar a comunicação entre o equipamento e os servidores DNS.

## 2. ESCOPO

Procedimento aplicável às atividades de suporte técnico, infraestrutura e operações de segurança (SOC), especialmente durante a investigação de falhas de acesso a domínios e possíveis problemas de resolução de nomes.

## 3. CONCEITOS IMPORTANTES

- **DNS:** Domain Name System. Sistema responsável por traduzir nomes de domínio em endereços IP.
- **Resolver:** componente responsável por realizar consultas DNS.
- **Nameserver:** servidor responsável por responder às consultas DNS.
- **IPv4:** protocolo de endereçamento de 32 bits.
- **IPv6:** protocolo de endereçamento de 128 bits.
- **Registro A:** associa um nome de domínio a um endereço IPv4.
- **Registro AAAA:** associa um nome de domínio a um endereço IPv6.
- **UDP:** protocolo de transporte utilizado normalmente nas consultas DNS.
- **TCP:** também pode ser utilizado nas consultas DNS.
- **Porta 53:** porta padrão utilizada pelo serviço DNS.
- **DNSSEC:** Domain Name System Security Extensions, conjunto de mecanismos para validar a autenticidade e integridade das respostas DNS.

## 4. FERRAMENTAS UTILIZADAS

- Ubuntu Linux
- Terminal
- `ping`
- `getent`
- `resolvectl`
- `nslookup`

## 5. PROCEDIMENTO OPERACIONAL

### ETAPA 1 - Verificar a conectividade com um endereço IP externo

**Comando:**

```bash
ping -c 4 1.1.1.1
```

**Finalidade:**

Verificar se existe comunicação IP com um endereço externo, sem depender da resolução de nomes DNS.

**Interpretação:**

- `4 packets transmitted`: quatro pacotes enviados.
- `4 received`: quatro respostas recebidas.
- `0% packet loss`: nenhuma perda durante o teste.
- `time`: tempo de resposta em milissegundos.

**Resultado do laboratório:**

Foram recebidas quatro respostas, sem perda de pacotes.

**Conclusão:** houve comunicação com o endereço IP testado. Isso não garante, isoladamente, que todos os serviços da Internet estejam funcionando.

### ETAPA 2 - Testar a resolução de nomes

**Comando:**

```bash
getent hosts google.com
```

**Finalidade:**

Verificar se o sistema consegue resolver o nome de domínio para um endereço IP.

**Interpretação:**

Se o comando retornar um endereço IP associado ao domínio, a resolução foi realizada com sucesso.

O resultado pode apresentar um endereço IPv4 ou IPv6.

**Resultado do laboratório:**

O sistema retornou um endereço IPv6 associado ao domínio `google.com`.

**Conclusão:** a resolução de nomes funcionou nesse teste.

### ETAPA 3 - Identificar os servidores DNS configurados

**Comando:**

```bash
resolvectl status
```

**Finalidade:**

Consultar as informações de resolução DNS utilizadas pelo sistema.

**Analisar:**

- Servidores DNS configurados.
- Servidor DNS atual.
- Interface de rede associada.
- Domínios de pesquisa.
- Estado das configurações DNSSEC.

**Resultado do laboratório:**

Foram identificados servidores DNS associados à interface `enp0s3`, incluindo:

- `189.7.40.43`
- `189.7.40.48`
- `fd17:625c:f037:2::3`

O servidor indicado como atual foi `189.7.40.43`.

**Conclusão:** foi possível identificar os servidores DNS configurados no ambiente.

### ETAPA 4 - Consultar o DNS utilizando nslookup

**Comando:**

```bash
nslookup google.com
```

**Finalidade:**

Consultar a resolução DNS utilizando o resolvedor configurado no sistema.

**Resultado do laboratório:**

O retorno apresentou:

- Servidor local: `127.0.0.53`
- Porta: `53`
- Registros IPv4 e IPv6 associados ao domínio.

**Interpretação importante:**

O endereço `127.0.0.53` representa o resolvedor local do serviço `systemd-resolved` no Ubuntu.

Ele não é, necessariamente, o servidor DNS externo. O resolvedor local encaminha as consultas aos servidores DNS configurados.

### ETAPA 5 - Consultar diretamente um servidor DNS externo

**Comando:**

```bash
nslookup google.com 1.1.1.1
```

**Finalidade:**

Realizar uma consulta diretamente ao servidor DNS público da Cloudflare.

**Interpretação:**

O comando permite comparar a resposta obtida diretamente de um servidor DNS externo com a resposta do resolvedor configurado no sistema.

**Resultado do laboratório:**

A consulta retornou registros IPv4 e IPv6 para o domínio `google.com`.

**Conclusão:** o servidor DNS externo respondeu à consulta realizada.

### ETAPA 6 - Testar consulta DNS utilizando TCP

**Comando:**

```bash
nslookup -vc google.com 1.1.1.1
```

**Finalidade:**

Verificar a resposta de uma consulta DNS utilizando TCP em vez do transporte UDP normalmente utilizado.

**Interpretação:**

- `-vc`: força o uso de TCP no `nslookup` compatível com essa opção.
- `google.com`: domínio consultado.
- `1.1.1.1`: servidor DNS consultado.

**Resultado do laboratório:**

A consulta utilizando TCP foi concluída e retornou registros DNS.

**Conclusão:** houve resposta do servidor DNS durante o teste via TCP.

## 6. ANÁLISE DOS RESULTADOS

| Teste | Resultado observado |
|---|---|
| Ping para 1.1.1.1 | Sem perda de pacotes |
| Resolução com getent | Sucesso |
| Identificação dos DNS | Servidores identificados |
| nslookup padrão | Consulta respondida |
| Consulta direta a 1.1.1.1 | Consulta respondida |
| Consulta DNS via TCP | Consulta respondida |

## 7. AÇÕES EM CASO DE FALHA

1. Verificar a conectividade IP.
2. Conferir os servidores DNS configurados.
3. Testar a resolução de nomes com `getent`.
4. Realizar consultas com `nslookup`.
5. Comparar o resolvedor local com um servidor DNS externo autorizado.
6. Investigar possíveis bloqueios da porta 53, falhas de configuração ou indisponibilidade do servidor.
7. Registrar evidências e encaminhar o incidente quando necessário.

**Atenção:** uma falha de consulta DNS não significa necessariamente que a Internet esteja indisponível. É necessário separar problemas de conectividade IP de problemas de resolução de nomes.

## 8. REGISTRO DE EVIDÊNCIAS

Registrar:

- Data e horário da análise.
- Sistema operacional.
- Interface de rede.
- Servidores DNS identificados.
- Domínio consultado.
- Tipo de registro retornado.
- Protocolo utilizado na consulta.
- Resultado dos testes.
- Mensagens de erro.
- Ações executadas.

Não divulgar dados sensíveis de ambientes reais sem autorização.

## 9. RESULTADO DO LABORATÓRIO

Durante a prática realizada no Ubuntu, foram executados testes de conectividade IP, resolução de nomes, identificação de servidores DNS e consultas utilizando UDP e TCP.

Os testes demonstraram:

- Conectividade com o endereço IP externo testado.
- Resolução bem-sucedida do domínio `google.com`.
- Identificação dos servidores DNS configurados.
- Resposta de consultas ao resolvedor local.
- Resposta de consulta direta ao DNS público `1.1.1.1`.
- Resposta de consulta DNS utilizando TCP.

**Conclusão:** os testes de resolução DNS foram concluídos com sucesso no ambiente de laboratório.

## 10. CONCLUSÃO TÉCNICA

A análise de DNS é essencial para investigar problemas de acesso a serviços, falhas de resolução de nomes e possíveis anomalias na comunicação de rede.

O analista deve compreender a diferença entre conectividade IP, resolução DNS, resolvedor local e servidor DNS externo.

A comparação entre consultas realizadas por diferentes métodos ajuda a identificar onde pode estar a origem de uma falha.

---

**Projeto:** Laboratório Prático de Defesa Cibernética  
**Área:** Redes e Operações de Segurança (SOC)  
**Documento:** POP 002  
**Status:** Concluído
