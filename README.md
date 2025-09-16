# Saudações Dockerizadas 🎉

Este projeto é composto por três serviços **Dockerizados** que trabalham em conjunto para gerar saudações aleatórias integradas a pessoas aleatórias.  

O repositório traz a configuração necessária para rodar os serviços localmente via **Docker Compose**.

---

## 📋 Pré-requisitos

Antes de rodar o projeto, certifique-se de ter instalado:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

> ⚠️ Importante:  
> - No **Linux**, geralmente é necessário usar `sudo` antes dos comandos.  
> - No **Windows**, os comandos devem ser executados no **PowerShell** ou **Prompt** com permissões administrativas.  

---

## 🚀 Passo a passo (Linux/Ubuntu/Debian)

1. **Clonar o repositório**
```bash
git clone https://github.com/skvanderson/saudacoes-dockerizadas.git
cd saudacoes-dockerizadas
```
2. **Verificar instalação do Docker e Docker Compose** 
```
sudo docker -v
sudo docker-compose -v
```
3. **Subir os containers**
```
sudo docker-compose up -d
```
O parâmetro -d roda em segundo plano.
  Se quiser reconstruir as imagens (após mudanças no código/Dockerfile), use:
```
sudo docker-compose up --build -d
```
4. **Verificar os containers rodando**
```
sudo docker ps
```

| CONTAINER ID | IMAGE                                     | PORTS                   |
|--------------|-------------------------------------------|-------------------------|
| `xxxxxxxx`   | `sharlles13/ms-saudacoes-aleatorias:1.0`  | `0.0.0.0:8081->8080/tcp`|
| `yyyyyyyy`   | `sharlles13/ms-pessoas-aleatorias:1.0`    | `0.0.0.0:8003->8000/tcp`|
| `zzzzzzzz`   | `sharlles13/gerador_saudacao:version-1.0` | `0.0.0.0:8080->80/tcp`  |

5. **Acessar a Aplicação**

* **Frontend (site):** [http://localhost:8082](http://localhost:8082)
* **Microsserviço de pessoas:** [http://localhost:8003](http://localhost:8003)
* **Microsserviço de saudações:** [http://localhost:8081](http://localhost:8081)

6.**Parar os containers**
```
sudo docker-compose down
```

---

## 🚀 Passo a passo (Windows)

---

1.  **Instalar o Docker Desktop**
    * Baixe e instale o [Docker Desktop](https://www.docker.com/products/docker-desktop/).
    * Durante a instalação, certifique-se de que a opção para incluir o **Docker Compose** está habilitada.
    * Após a conclusão da instalação, reinicie o computador para aplicar todas as configurações.
  
2. **Clonar o Reposítório**
   Abra o PowerSherll e execute.
```
git clone https://github.com/skvanderson/saudacoes-dockerizadas.git
cd saudacoes-dockerizadas
```
3. **Verificar instalação do Docker e Docker Compose**
```
docker --version
docker-compose --version
```
4. **Subir os containers**

```
docker-compose up -d
```
Se precisar reconstruir:
```
docker-compose up --build -d
```

5. **Verificar containers em execução**
```
docker ps
```
6. **Acessar a Aplicação**

* **Frontend (site):** [http://localhost:8082](http://localhost:8082)
* **Microsserviço de pessoas:** [http://localhost:8003](http://localhost:8003)
* **Microsserviço de saudações:** [http://localhost:8081](http://localhost:8081)

7. **Parar os containers**
```
docker-compose down
```

### 🛠️ Comandos úteis para memoriazar

* **Ver logs de um serviço**
    ```bash
    docker-compose logs -f <nome-do-serviço>
    ```
* **Reiniciar containers**
    ```bash
    docker-compose restart
    ```
* **Remover todos os containers e volumes**
    ```bash
    docker-compose down -v
    ```
* **Se ainda der "permission denied", desligue o Docker completamente**
    ```
    sudo systemctl stop docker.socket
    sudo systemctl stop docker
    ```
* **Confirme que parou:**
    ```
    systemctl status docker
    ```
* **Agora, apague os contêineres parados:**
    ```
    sudo rm -rf /var/lib/docker/containers/*
    ```
* **Depois reinicie o Docker:**
    ```
    sudo systemctl start docker
    ```
* **O mais comun para uso diário**
    ```
    sudo docker compose down
    ```
---

---
### 📚 Referências

* [Documentação oficial do Docker](https://docs.docker.com/)
* [Documentação oficial do Docker Compose](https://docs.docker.com/compose/)
---
---
### 👨‍💻 Autor

Projeto desenvolvido por [Sharlles](https://github.com/skvanderson).
---
