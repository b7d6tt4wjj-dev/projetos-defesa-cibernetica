
# LAB 04 - SOCIAL ENGINEER TOOLKIT (SET)

**Área:** Cibersegurança  
**Curso:** Ethical Hacker  
**Plataforma:** Cisco Networking Academy  
**Ambiente:** Kali Linux / Cybersecurity LabVM  
**Aplicação de laboratório:** DVWA  
**Status:** Em andamento

---

# 1. OBJETIVO DA ATIVIDADE

Explorar o Social-Engineer Toolkit (SET), compreender suas funcionalidades e conhecer os métodos utilizados em testes de segurança relacionados à engenharia social.

A atividade também permite estudar a interação entre ferramentas de segurança, aplicações web e ambientes controlados de laboratório.

# 2. AMBIENTE UTILIZADO

- Kali Linux.
- Cybersecurity LabVM.
- Terminal Linux.
- Navegador Firefox.
- Social-Engineer Toolkit (SET).
- Damn Vulnerable Web Application (DVWA).
- VirtualBox / ambiente virtualizado.

# 3. PREPARAÇÃO DO AMBIENTE

## 3.1. Configuração do teclado

Foi identificado um problema no layout do teclado do Kali Linux.

Para corrigir a configuração ABNT2, foram utilizados os comandos:

```bash
apt update
apt install -y x11-xkb-utils
setxkbmap -model abnt2 -layout br
```

**Resultado:** layout do teclado brasileiro configurado corretamente.

## 3.2. Verificação de conectividade

Foi realizado um teste de comunicação com o endereço IP do DVWA:

```bash
ping -c 4 10.6.6.13
```

**Resultado observado:**
- 4 pacotes enviados.
- 4 pacotes recebidos.
- 0% de perda.

A comunicação com o endereço de destino foi confirmada.

# 4. EXPLORAÇÃO DO SOCIAL-ENGINEER TOOLKIT

## 4.1. Inicialização da ferramenta

O SET foi iniciado pelo terminal:

```bash
setoolkit
```

Foi apresentada a solicitação de aceitação dos termos de uso.

Após a confirmação, o menu principal da ferramenta foi exibido.

## 4.2. Menu principal

Foram identificadas as seguintes opções:

1. Social-Engineering Attacks
2. Penetration Testing (Fast-Track)
3. Third Party Modules
4. Update SET
5. Update SET config
6. Help, Credits e About
99. Exit

## 4.3. Website Attack Vectors

Dentro da categoria Social-Engineering Attacks, foi explorada a opção Website Attack Vectors.

Foram identificados os seguintes métodos:

- Java Applet Attack Method.
- Metasploit Browser Exploit Method.
- Credential Harvester Attack Method.
- Tabnabbing Attack Method.
- Web Jacking Attack Method.
- Multi-Attack Web Method.
- HTA Attack Method.

## 4.4. Credential Harvester

Foi acessado o menu Credential Harvester Attack Method.

Foram identificadas três opções:

1. Web Templates.
2. Site Cloner.
3. Custom Import.

O objetivo desta etapa foi compreender o funcionamento da técnica de clonagem de páginas e os riscos relacionados a formulários de autenticação.

# 5. AMBIENTE DVWA

## 5.1. Acesso à aplicação

A aplicação DVWA foi acessada pelo navegador Firefox:

`http://10.6.6.13`

Foi realizado o login no ambiente de laboratório.

## 5.2. Configuração de segurança

A página de configuração de segurança foi acessada:

`http://10.6.6.13/security.php`

O nível de segurança foi configurado como:

**LOW**

## 5.3. Verificação HTTP

Foi utilizado o comando:

```bash
curl -I http://10.6.6.13
```

Foi observada uma resposta HTTP:

**302 Found**

O servidor identificado foi Apache/2.4.10 (Debian), com redirecionamento para a página de login.

# 6. ESTUDO DA TÉCNICA SITE CLONER

A opção Site Cloner foi localizada dentro do menu Credential Harvester.

Durante a exploração, foram identificados campos relacionados ao endereço de retorno e à página utilizada como referência.

A atividade permitiu compreender conceitos importantes:

- Clonagem de páginas web.
- Formulários HTML.
- Requisições HTTP.
- Método POST.
- Riscos de páginas falsas de autenticação.
- Engenharia social e roubo de credenciais.

**Registro do resultado:** a tentativa realizada apresentou erro e a clonagem não foi concluída.

Nenhuma captura de credenciais foi considerada concluída nesta atividade.

# 7. CONHECIMENTOS ADQUIRIDOS

Ao longo da prática, foram trabalhados os seguintes conhecimentos:

- Utilização do terminal Kali Linux.
- Configuração do teclado ABNT2.
- Testes básicos de conectividade.
- Inicialização e navegação no SET.
- Identificação dos módulos de engenharia social.
- Acesso e configuração do DVWA.
- Interpretação de respostas HTTP.
- Conceitos de clonagem de páginas.
- Identificação dos riscos de formulários de autenticação.

# 8. CONSIDERAÇÕES FINAIS

A atividade proporcionou contato prático com ferramentas utilizadas em laboratórios de Ethical Hacking.

O estudo do SET e do DVWA contribuiu para compreender como técnicas de engenharia social podem explorar a confiança dos usuários e como aplicações web podem ser utilizadas em ambientes controlados para fins educacionais.

A documentação será atualizada conforme as próximas etapas forem executadas.

---

**Projeto de estudos em Cibersegurança | Ethical Hacking**
