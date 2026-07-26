# 🛡️ Cloudflare Zero Trust & SSE (Security Service Edge) Lab

Este repositório documenta a implementação prática de uma arquitetura de **Security Service Edge (SSE)** e **Zero Trust** utilizando a plataforma **Cloudflare One (Cloudflare Zero Trust)**. 

O objetivo deste laboratório é demonstrar a aplicação de conceitos modernos de segurança de rede, substituição de VPNs tradicionais, inspeção de tráfego na camada de aplicação (L7) e controle de acesso condicional.

---

## 📐 Arquitetura do Laboratório

A plataforma foi configurada para validar os três pilares fundamentais do **SSE**:

1. **SWG (Secure Web Gateway) / Cloudflare Gateway:** Filtragem de tráfego de saída, inspeção de DNS/HTTP e bloqueio de aplicações de risco ou não autorizadas.
2. **ZTNA (Zero Trust Network Access) / Cloudflare Access:** Conectividade segura e isolada para aplicações internas sem exposição de portas na internet e sem necessidade de VPN.
3. **Device Posture & Identity (Cloudflare WARP Client):** Validação do estado de segurança do dispositivo (*Endpoint*) e integração com provedor de identidade (IdP) para autenticação multifator.

---

## 🧪 Módulos Implementados

### 1. Secure Web Gateway (SWG) — Filtragem de Tráfego & L7
- **Objetivo:** Impedir o vazamento de dados e o uso de aplicações não autorizadas (Shadow IT) na rede corporativa.
- **Implementação:**
  - Criação de **Políticas de Firewall de DNS e HTTP** no Cloudflare Gateway.
  - Bloqueio de requisições direcionadas a serviços de mídia e APIs de aplicações (ex: `cdninstagram.com`, `graph.instagram.com`, `fbcdn.net`).
  - Bloqueio de bypass de DNS privado (**DoH / DNS-over-HTTPS**) através da restrição do domínio `dns.google`.
  - Configuração de **Locations** e apontamento de IPs de DNS para aplicação de políticas em dispositivos *agentless* (via infraestrutura de rede/roteador).

### 2. Zero Trust Network Access (ZTNA) — Acesso Condicional
- **Objetivo:** Substituir a VPN tradicional por conexões perimétricas estritas focadas na aplicação.
- **Implementação:**
  - Publicação e proteção de recursos internos garantindo o princípio do **Menor Privilégio**.
  - Regras de controle de acesso baseadas em identidade (e-mail/grupo) e validação de contexto antes de liberar o acesso à aplicação.

### 3. Gerenciamento de Endpoint & Monitoramento
- **Objetivo:** Garantir a telemetria do dispositivo do usuário (*Home Office*) e rastreabilidade total.
- **Implementação:**
  - Associação do **Cloudflare One Client (WARP)** ao *Team Name* corporativo usando protocolo WireGuard.
  - Inspeção e monitoramento centralizado através dos **Logs de Auditoria** e eventos de bloqueio no painel.

---

## 🛠️ Tecnologias e Conceitos Utilizados
- **Conceitos:** SSE, Zero Trust (ZTNA), SWG, Least Privilege, Device Posture, Micro-segmentação.
- **Protocolos & Tecnologias:** DNS, HTTP/HTTPS, TLS Inspection, DoH, WireGuard, IPv4/IPv6.
- **Ferramentas:** Cloudflare One (Zero Trust Dashboard), Cloudflare WARP Client.

---

## 📸 Evidências de Configuração

*(Adicione aqui os prints das telas do seu painel Cloudflare)*

1. **Políticas de Firewall DNS / HTTP ativas:**
   `![Políticas SWG](./prints/firewall-policies.png)`

2. **Log de Eventos e Bloqueio de Tráfego:**
   `![Logs de Auditoria](./prints/audit-logs.png)`

3. **Status de Conexão do Cloudflare WARP:**
   `![WARP Connected](./prints/warp-client.png)`
