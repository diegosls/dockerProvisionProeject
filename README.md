# Projeto 02 - Docker com Vagrant e Ansible

## Desenvolvedores

- Diego Costa Sales - 20221380034
- Igor de Oliveira Teixeira - 20221380025

## Disciplina

Administração de Sistemas Abertos  
Professor: Leonidas Lima  
Período: 2025.1

## Sobre o Projeto

Este projeto implementa uma infraestrutura completa de containers Docker provisionada automaticamente usando Vagrant e Ansible. A stack inclui:

- Nginx com Load Balancer (imagem personalizada)
- WordPress (servidor web)
- MySQL (banco de dados)
- Provisionamento automático com Vagrant + Ansible

## Arquitetura do Sistema

```
+---------------------------------------+
|         Máquina Virtual (Vagrant)     |
|                                       |
|  +---------------------------------+  |
|  |         Containers Docker       |  |
|  |                                 |  |
|  |  +-------------+    +--------+  |  |
|  |  |  WebProxy   |    | WordPress|  |  |
|  |  |  (Nginx L4) |    | Server  |  |  |
|  |  +-------------+    +--------+  |  |
|  |       ↑8080           ↑80       |  |
|  +---------------------------------+  |
|                 ↓                     |
|  +---------------------------------+  |
|  |           Database              |  |
|  |          (MySQL)                |  |
|  +---------------------------------+  |
+---------------------------------------+
```

## Estrutura de Arquivos

```
provisionDocker/
├── Vagrantfile              # Configuração da VM
├── playbook_ansible.yml     # Provisionamento com Ansible  
├── docker-compose.yml       # Stack Docker
└── nginx-image/             # (Local apenas - não sobe para Git)
    ├── Dockerfile           # Imagem customizada do Nginx
    └── nginx.conf           # Configuração de Load Balancing
```

## Como Executar

### Pré-requisitos

- VirtualBox instalado
- Vagrant instalado
- Conta no Docker Hub (para imagem customizada)

### Passo a Passo

1. Clone o repositório:
    ```sh
    git clone https://github.com/diegosls/dockerProvisionProeject
    cd provisionDocker
    ```

2. Execute o provisionamento:
    ```sh
    vagrant up
    ```

Este comando irá:

- Criar VM Debian
- Instalar Docker via Ansible
- Baixar imagens do Docker Hub
- Subir containers WordPress + MySQL + Nginx

3. Acesse a aplicação:  
   Abra no navegador:  
   `http://192.168.56.145:8080`

4. Parar a infraestrutura:
    ```sh
    vagrant halt      # Pausa a VM
    vagrant destroy   # Remove completamente
    ```

## Tecnologias Utilizadas

| Tecnologia | Função                    |
|------------|--------------------------|
| Vagrant    | Provisionamento da VM     |
| Ansible    | Configuração automática   |
| Docker     | Containers da aplicação   |
| Nginx      | Load Balancer Layer 4     |
| WordPress  | CMS Web                   |
| MySQL      | Banco de dados            |

## Objetivos Atendidos

- Provisionamento automático com Vagrant
- Configuração via Ansible
- Imagem Docker personalizada
- Load Balancing Layer 4
- Stack WordPress completa
- Volumes persistentes
- Rede Docker isolada

## Suporte

Em caso de problemas:

- Verifique se todas as portas estão livres
- Confirme que a imagem `diegosls/nginx-l4:latest` está pública no Docker Hub
- Execute `vagrant up --debug` para logs detalhados

Desenvolvido como parte da disciplina de Administração de Sistemas Abertos - IFPB
