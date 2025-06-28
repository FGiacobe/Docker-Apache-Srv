# Docker-Apache-Srv
Projeto servidor Apache em container Docker.

## 📘 Descrição do `docker-compose.yaml`

Esse `docker-compose.yaml` define um serviço chamado **`apache`** que usa o container **`httpd:alpine3.22`** para rodar um servidor Apache leve e rápido.

* **`image: httpd:alpine3.22`**
  Utiliza uma imagem oficial do Apache HTTP server baseada em Alpine Linux — leve e com todas as funcionalidades essenciais.

* **`container_name: apache-srv`**
  Define um nome fixo para o container, facilitando comandos e logs (ex.: `docker logs apache-srv`).

* **`ports: - 80:80`**
  Mapeia a porta 80 do host para a porta 80 do container, permitindo acesso via navegador em `http://localhost`.

* **`volumes: - ./www:/usr/local/apache2/htdocs`**
  Sincroniza a pasta `www` no diretório atual com a pasta de documentos do Apache dentro do container. Você pode editar arquivos localmente e ver os resultados imediatamente (Host → Container).

* **`command: httpd-foreground -c "ServerName localhost"`**
  Inicia o Apache em primeiro plano, definindo `ServerName localhost` para evitar warnings sobre nomes de servidor desconhecidos ([docs.alpinelinux.org][1], [forums.docker.com][2], [linkedin.com][3], [mialikescoffee.com][4], [linuxelite.com.br][5], [blog.nitishkumarsingh.xyz][6]).

---

## 🚀 Como usar esse `docker-compose.yaml`

### 1. Estrutura de pastas prevista

```text
projeto/
├── docker-compose.yaml
└── www/
    └── index.html  ← seu conteúdo HTML
```

### 2. Iniciar o serviço

Na raiz do projeto, rode:

```bash
docker compose up -d
```

Isso fará com que o Apache seja iniciado com nome `apache-srv` e ouça na porta 80.

### 3. Testar no navegador

Acesse `http://localhost` (ou o IP do host). Seu `index.html` na pasta `www/` será servido diretamente pelo Apache.

### 4. Parar e remover os containers

```bash
docker compose down
```

Isso para e remove o serviço `apache-srv`.

---

## ⚙️ Ajustes opcionais

* **Adicionar SSL**: coloque certificados em `www/ssl` e modifique o `httpd.conf` para habilitar HTTPS.
* **Múltiplos serviços**: você pode adicionar mais serviços ao `docker-compose.yaml` (como `db`, `php`, etc.).
* **Bind Mount em outras pastas**: para logs, configurações ou caches, use volumes como:

  ```yaml
  volumes:
    - ./config:/usr/local/apache2/conf
    - ./logs:/usr/local/apache2/logs
  ```

---

## 🗣️ Conclusão

Você tem aí um ambiente Apache **leve, simples e voltado para desenvolvimento**:

* Atualização imediata de conteúdo via bind mount.
* Sem complicação na configuração – apenas um `docker compose up`.
* Ideal para protótipos, testes ou aprendizado com containers web.

