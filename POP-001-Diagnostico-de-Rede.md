
# POP 001 - DIAGNÓSTICO INICIAL DE REDE

**Área:** Segurança da Informação | SOC  
**Sistema operacional:** Ubuntu Linux  
**Categoria:** Análise de conectividade  
**Status:** Concluído

---

## 1. OBJETIVO

Padronizar o diagnóstico inicial de conectividade de rede, identificando interfaces, endereços IP, endereço MAC, gateway padrão e possíveis falhas de comunicação.

## 2. ESCOPO

Procedimento aplicável às atividades de suporte técnico, infraestrutura e análise inicial de alertas de rede em ambientes Linux.

## 3. FERRAMENTAS UTILIZADAS

- Ubuntu Linux
- Terminal
- Comando `ip`
- Comando `ping`

## 4. PROCEDIMENTO OPERACIONAL

### ETAPA 1 - Identificar as interfaces de rede

**Comando:**

```bash
ip -br addr
```

**Finalidade:** visualizar as interfaces disponíveis, seu estado e os endereços IP configurados.

**Interpretação:**
- `lo`: interface de loopback.
- `enp0s3`: exemplo de interface de rede.
- `UP`: interface ativa.
- `DOWN`: interface desativada.
- `127.0.0.1`: endereço de loopback.
- `/24`: prefixo CIDR da rede.

### ETAPA 2 - Identificar o endereço MAC

**Comando:**

```bash
ip link show enp0s3
```

**Finalidade:** identificar o endereço MAC da interface.

**Interpretação:**

O endereço exibido após `link/ether` corresponde ao endereço MAC.

O MAC identifica a interface na comunicação da rede local.

### ETAPA 3 - Identificar o gateway padrão

**Comando:**

```bash
ip route
```

**Finalidade:** verificar as rotas configuradas no sistema.

**Interpretação:**
- `default`: rota padrão.
- `via`: endereço do gateway.
- `dev`: interface utilizada.
- `src`: endereço IP de origem.

O gateway padrão permite a comunicação com outras redes.

### ETAPA 4 - Testar a comunicação com o gateway

**Comando:**

```bash
ping -c 4 IP_DO_GATEWAY
```

Substituir `IP_DO_GATEWAY` pelo endereço encontrado na etapa anterior.

**Finalidade:** verificar a comunicação entre a estação e o gateway.

**Interpretação:**
- `4 packets transmitted`: quatro pacotes enviados.
- `4 received`: quatro respostas recebidas.
- `0% packet loss`: nenhuma perda durante o teste.
- `time`: tempo de resposta em milissegundos.

## 5. ANÁLISE DOS RESULTADOS

| Resultado | Possível interpretação |
|---|---|
| Interface DOWN | Interface desativada |
| Sem endereço IP | Possível falha de configuração ou DHCP |
| Gateway ausente | Possível problema de rota |
| Ping sem resposta | Possível falha de comunicação ou bloqueio de ICMP |
| 0% de perda | Comunicação confirmada durante o teste |

**Atenção:** ausência de resposta ao ping não comprova, isoladamente, que um equipamento está indisponível. O tráfego ICMP pode estar bloqueado.

## 6. AÇÕES EM CASO DE FALHA

1. Verificar se a interface está ativa.
2. Conferir se existe endereço IP configurado.
3. Verificar a rota padrão.
4. Testar novamente a comunicação com o gateway.
5. Investigar possíveis falhas de configuração ou conectividade.
6. Registrar as evidências e encaminhar o incidente quando necessário.

## 7. REGISTRO DE EVIDÊNCIAS

Registrar:
- Data e horário da análise.
- Sistema operacional.
- Interface analisada.
- Endereço IP e prefixo.
- Gateway padrão.
- Resultado dos testes.
- Mensagens de erro.
- Ações executadas.

Não divulgar dados de ambientes reais sem autorização.

## 8. RESULTADO DO LABORATÓRIO

Durante a prática realizada no Ubuntu, foram executadas verificações de interface, endereço IP, MAC e rota padrão.

**Resultado do teste de conectividade com o gateway:**
- Pacotes enviados: 4
- Pacotes recebidos: 4
- Perda de pacotes: 0%

**Conclusão:** a comunicação com o gateway foi confirmada durante o teste.

## 9. CONCLUSÃO TÉCNICA

O diagnóstico inicial de rede é uma etapa fundamental na investigação de incidentes.

A identificação de interfaces, endereços IP, MAC e gateway permite ao analista iniciar a investigação de problemas de conectividade de maneira organizada, técnica e documentada.

---

**Projeto:** Laboratório Prático de Defesa Cibernética  
**Área:** Redes e Operações de Segurança (SOC)  
**Documento:** POP 001  
**Status:** Concluído
