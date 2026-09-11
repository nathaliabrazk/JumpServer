
# Jump Server

# 🔐 Estudos sobre JumpServer

Repositório destinado aos estudos, conceitos, configurações e práticas relacionadas ao **JumpServer**, uma plataforma de **Gerenciamento de Acesso Privilegiado (PAM)** de código aberto.

O objetivo deste repositório é documentar o aprendizado sobre o uso do JumpServer como ponto centralizado e seguro para gerenciamento de acessos a servidores, bancos de dados, clusters e outros recursos de uma infraestrutura de TI.

---

## 📌 O que é o JumpServer?

O **JumpServer** é uma plataforma de gerenciamento de acesso privilegiado (PAM) que permite às equipes de TI e DevOps controlar e monitorar o acesso a diferentes recursos de uma infraestrutura.

Ele funciona como um **servidor intermediário (Jump Server)**, permitindo que usuários autorizados acessem servidores e outros ativos de forma controlada, sem a necessidade de conexão direta com os ambientes internos.

Por meio de uma interface web, é possível estabelecer sessões para diferentes tipos de recursos, como:

- 🐧 Servidores Linux via SSH
- 🪟 Servidores Windows via RDP
- 🗄️ Bancos de dados
- ☸️ Clusters Kubernetes
- 🌐 Aplicações e recursos remotos

---

## 🔑 O que são plataformas PAM?

É um sistema de cibersegurança usado para controlar, monitorar e proteger contas com permissões elevadas ou de superusuário em uma empresa. 

**O que o PAM faz**

**Cofre de senhas:** Armazena senhas de administradores de forma criptografada. 

**Controle de acesso mínimo:** Garante que os usuários tenham apenas as permissões necessárias para o trabalho.

**Monitoramento de sessões:** Grava e audita o que os administradores fazem nos servidores e sistemas.

**Acesso sob demanda:** Concede permissões temporárias apenas quando necessário. 

**Para que serve** - Evitar roubo de credenciais: Protege contra ataques que tentam usar contas de administradores para invadir redes.Atender a normas: Ajuda empresas a cumprir regras de auditoria e segurança de dados.

**Diferenças entre PAM e IAN** - 
A principal diferença entre IAM (Identity and Access Management) e PAM (Privileged Access Management) está no tipo de usuário e no nível de acesso que cada um gerencia. Enquanto o IAM cuida dos acessos do dia a dia de todos os funcionários, o PAM é uma camada extra de segurança focada exclusivamente nas contas que têm "superpoderes" no sistema.


# ⚙️ Principais funcionalidades

## 🎭 Mascaramento de acesso

O JumpServer fornece um **portal web centralizado** por meio do qual os administradores e usuários autorizados podem acessar os recursos da infraestrutura.

O usuário realiza o acesso ao JumpServer e, a partir dele, inicia sessões SSH, RDP ou conexões com bancos de dados.

Dessa forma, o acesso aos servidores internos fica centralizado e controlado pelo JumpServer.

---

## 🔒 Isolamento de IP

Uma das características importantes é o isolamento do acesso aos servidores internos.

O usuário final nunca digita, pinga ou enxerga o IP do servidor interno. O tráfego morre no JumpServer e ele inicia uma nova conexão isolada por trás dos panos até o host final.

O fluxo ocorre de forma semelhante a:

```text
Usuário
   |
   | HTTPS
   v
JumpServer
   |
   | SSH / RDP / Banco de Dados
   v
Servidor interno
```
---

## 🔍 Segurança e auditoria
Gravação completa de sessões em vídeo, controle baseado em funções (RBAC) e detecção de ameaças em tempo real. 

**Gravações de sessão**

## 🎥 Gravação e Auditoria de Sessões ##

O **JumpServer** possui recursos de gravação e auditoria de sessões que permitem registrar as atividades realizadas pelos usuários durante o acesso aos ativos da infraestrutura.

As gravações funcionam de forma **automatizada e transparente**, utilizando componentes intermediários que atuam como proxy entre o usuário e o ativo de destino, permitindo o monitoramento e o registro das atividades realizadas.

Os recursos podem ser utilizados para auditoria, segurança, investigação de incidentes e acompanhamento das atividades realizadas nos ativos.

---

## 🔄 Como funciona a gravação de sessões?

O processo de gravação pode ser dividido em algumas etapas:

```text
┌─────────────────┐
│     Usuário     │
└────────┬────────┘
         │
         │ Acesso
         ▼
┌─────────────────┐
│    JumpServer   │
│      Proxy      │
└────────┬────────┘
         │
         │ Sessão
         ▼
┌─────────────────┐
│      Ativo      │
│ Linux / Windows │
│ Banco / Rede    │
└─────────────────┘
         │
         ▼
┌─────────────────┐
│    Gravação     │
│    e Auditoria  │
└─────────────────┘
```
## 🛡️ Suporte a MFA (autenticação multifator) ##
Possui integração com LDAP/Active Directory e verificação de identidade em várias camadas.

**Escopo Global ou por Perfil:** O MFA pode ser configurado para abranger todos os usuários da plataforma ou apenas grupos específicos, como os administradores

**Métodos Nativos e Padrões:** TOTP (Time-based One-Time Password): Utiliza aplicativos autenticadores tradicionais (como Google Authenticator, Microsoft Authenticator ou FreeOTP) para gerar códigos temporários de 6 dígitos.Passkey (FIDO2 / WebAuthn): Permite autenticação sem senha baseada em criptografia de chave pública, usando biometria do dispositivo ou chaves de segurança físicas.E-mail: Envio de código dinâmico de verificação por correio eletrônico.

**Integrações Externas:** Suporte a provedores via RADIUS (com suporte a OTP integrado).Integração com diretórios e Single Sign-On (SSO) como CAS, OIDC, SAML2 e OAuth2 (onde o MFA pode ser herdado do provedor de identidade externo, como Azure Entra ID/Okta).

**Proteção de Credenciais Sensíveis:** O JumpServer também pode impor a checagem obrigatória de MFA no momento em que um operador tenta visualizar a senha de uma conta privilegiada armazenada no cofre

---

##  🎯 Onde o Jump Server é usado?
Jump Servers são amplamente utilizados em ambientes corporativos, especialmente em setores que lidam com informações sensíveis, como finanças, saúde e tecnologia. Eles são ideais para empresas que precisam garantir que apenas usuários autorizados tenham acesso a sistemas críticos. Além disso, são frequentemente empregados em operações de gerenciamento de TI, onde a segurança e a conformidade são prioridades.

---

##  ⭐ Vantagens
**Instalação Rápida:**  A versão comunitária (Community Edition) do JumpServer é gratuita para até 5.000 ativos e pode ser instalada em um servidor Linux limpo (64-bit, recomendação mínima de 4vCPU e 8GB de RAM) executando o comando de inicialização rápida via Docker

**Custo-Benefício:** Conta com uma edição comunitária gratuita robusta (Community Edition) e custos significativamente menores em versões empresariais se comparado a concorrentes proprietários.


---

##  🧩 Desafios na implementação de Jump Servers
Embora os Jump Servers ofereçam diversas vantagens, sua implementação pode apresentar desafios. Um dos principais obstáculos é **garantir que todos os usuários estejam adequadamente treinados para utilizar o Jump Server de forma segura**. Além disso, **a configuração inadequada pode levar a vulnerabilidades**, tornando essencial que as equipes de TI sigam as melhores práticas e realizem testes de segurança regulares.

---

##  🥊 Jump Server vs VPN
Embora tanto o Jump Server quanto a VPN (Virtual Private Network) sejam utilizados para acesso remoto, eles servem a propósitos diferentes. 

A VPN cria um túnel seguro para a rede, permitindo que os usuários acessem recursos internos como se estivessem fisicamente presentes. Por outro lado, o Jump Server é um ponto de acesso controlado que limita o acesso a servidores específicos. Em muitos casos, as organizações optam por usar ambos em conjunto para maximizar a segurança.
