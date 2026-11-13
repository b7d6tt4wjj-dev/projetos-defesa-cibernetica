Análise de Segurança do Serviço CUPS no Ubuntu

1. Objetivo do laboratório

Realizar uma análise básica de segurança do serviço CUPS (Common UNIX Printing System) no Ubuntu, utilizando ferramentas de linha de comando para identificar portas abertas, verificar serviços ativos e testar respostas HTTP.

2. Ambiente utilizado

* Sistema operacional: Ubuntu Linux
* Ambiente virtualizado: VirtualBox
* Ferramenta de varredura: Nmap 7.98
* Ferramenta de requisições HTTP: cURL
* Gerenciamento de serviços: systemctl
* Verificação de conexões: ss

3. Etapas executadas

Etapa 1: Verificação do Nmap

Comando:

nmap --version

Resultado: Nmap 7.98 instalado e funcionando.

Etapa 2: Varredura de portas locais

Comando:

nmap 127.0.0.1

Resultado encontrado:

* Host ativo: 127.0.0.1 (localhost).
* 999 portas TCP fechadas.
* Porta 631/TCP aberta.
* Serviço identificado: IPP (Internet Printing Protocol).

Etapa 3: Identificação dos serviços em execução

Comando:

sudo ss -lntp

Resultado:

Foi identificado o serviço CUPS (cupsd) escutando na porta 631, nos endereços locais IPv4 e IPv6.

Etapa 4: Verificação do serviço CUPS

Comando:

systemctl status cups

Resultado:

O serviço cups.service apresentou o estado ACTIVE (RUNNING), indicando que estava em execução.

Etapa 5: Teste de resposta HTTP

Comando:

curl -I http://127.0.0.1:631

Resultado:

HTTP/1.1 200 OK

Interpretação: o serviço respondeu corretamente à requisição HTTP.

Etapa 6: Teste do método OPTIONS

Comando:

curl -i -X OPTIONS http://127.0.0.1:631

Resultado:

HTTP/1.1 200 OK

O servidor respondeu à requisição OPTIONS.

Etapa 7: Verificação do conteúdo disponibilizado

Comando:

curl -s http://127.0.0.1:631/ | head -20

Resultado:

Foi identificado o conteúdo HTML da página inicial do CUPS, incluindo informações e links de administração.

4. Análise dos resultados

Durante a atividade, foi possível identificar:

* O computador estava ativo.
* A porta 631/TCP estava aberta.
* O serviço CUPS estava em execução.
* O servidor respondeu às requisições HTTP.
* A interface web do CUPS disponibilizou conteúdo HTML.

As 999 portas fechadas não aceitaram conexões TCP durante a varredura. Isso reduz os pontos de acesso disponíveis, mas não garante proteção contra ataques.

5. Conclusão

O laboratório permitiu praticar reconhecimento de serviços, identificação de portas abertas e verificação de respostas HTTP utilizando ferramentas do Linux.

A atividade demonstrou a importância de identificar serviços em execução e avaliar se as portas disponibilizadas são realmente necessárias.

6. Ferramentas e conhecimentos desenvolvidos

* Linux e terminal
* Nmap
* cURL
* Análise de portas TCP
* Serviços de rede
* Protocolo HTTP
* Identificação de serviços
* Fundamentos de análise de segurança

7. Observação de segurança

A análise foi realizada em ambiente próprio e local (localhost), para fins educacionais.

Projeto desenvolvido como prática de estudos em Defesa Cibernética.
