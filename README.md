# VoIP com Asterisk e Linphone via Docker

Este projeto cria um ambiente de VoIP com Asterisk (PBX) e dois clientes Linphone com interface gráfica, interligados por uma rede interna Docker (`redeasterisk`). O usuário `pedro` pode ligar para `maria` discando o número `0800`.

---

## Pré-requisitos

- Docker e Docker Compose instalados
- Ambiente gráfico Linux com suporte a X11 (ex: Ubuntu)
- Permissão para containers acessarem o display gráfico

---

## 🧱 Estrutura do projeto

```text
voip-projeto/
├── docker-compose.yml
├── Dockerfile-linphone
├── Dockerfile-asterisk
├── etc/
│   └── asterisk/
│       ├── asterisk.conf
│       ├── extensions.conf
│       ├── logger.conf
│       ├── modules.conf
│       └── sip.conf
```

## 📦 Build dos containers

```bash
docker compose build
```

---
## 🚀 Executando o ambiente

1. Libere o acesso gráfico para containers:

```bash
xhost +local:root
```

2. Suba o ambiente:

```bash
docker compose up
```

## 🛠️ Configuração dos usuários SIP no Linphone

No Linphone de cada container, vá até:

Options → Preferences → Manage SIP Accounts → Add
 
### 🔧 Configuração para **Pedro**:

- **Username:** `pedro`  
- **Password:** `1234`  
- **Domain:** `asterisk`  
- **Proxy:** `sip:asterisk`  

### 🔧 Configuração para **Maria**:

- **Username:** `maria`  
- **Password:** `1234`  
- **Domain:** `asterisk`  
- **Proxy:** `sip:asterisk`  

> ⚠️ **Importante:** no campo **Domain**, digite apenas `asterisk` (sem `sip:` e sem o nome de usuário). Exemplo errado: `sip:pedro@asterisk`.

Após preencher os campos corretamente, clique em **Apply**.

Se o registro for bem-sucedido, o status no canto inferior direito do Linphone ficará **verde**.
