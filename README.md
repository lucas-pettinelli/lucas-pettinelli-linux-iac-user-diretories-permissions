# Infraestrutura como Código: Script de Criação de Estrutura de Usuários, Diretórios e Permissões em Linux Ubuntu 18.04

Este projeto consiste em um script `bash` para automatizar a criação de uma estrutura básica de usuários, grupos e diretórios com permissões específicas em um sistema Linux Ubuntu 18.04. O objetivo é demonstrar os conceitos de Infraestrutura como Código (IaC) através da automatização de tarefas comuns de administração de sistemas.

![img](https://media.licdn.com/dms/image/v2/D4D12AQFMiTlCYEPkqQ/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1682381241086?e=2147483647&v=beta&t=eiOIlGopaWfWwx6kKANeHxv1SEXaHierFuWl1L0nNOk)

## Conteúdo

O script `estrutura.sh` realiza as seguintes ações:

Entendo a regra de negócio da companhia:
| /public  | /adm  | /ven  | /sec  |
|---|---|---|---|
| publico  | admnistrativo  | vendas  |  secretariado |

1.  **Criação de Diretórios:** Cria os diretórios  `/public`, `/adm`, `/ven` e `/sec`.
2.  **Criação de Grupos de Usuários:** Cria os grupos `GRP_ADM`, `GRP_VEN` e `GRP_SEC`.
3.  **Criação de Usuários:** Cria usuários específicos para cada grupo, definindo o diretório home (`-m`), o shell padrão (`-s /bin/bash`), uma senha criptografada (`-p $(openssl passwd -crypt 321)`) e adicionando-os ao grupo correspondente (`-G`).
    * **GRP_ADM:** `carlos`, `maria`, `joao`
    * **GRP_VEN:** `debora`, `sebastiana`, `roberto`
    * **GRP_SEC:** `josefina`, `amanda`, `rogerio`
4.  **Especificação de Permissões dos Diretórios:** Define o proprietário e o grupo de cada diretório, além das permissões de acesso:
    * `/adm`: Proprietário `root`, Grupo `GRP_ADM`, Permissões `770` (proprietário e grupo têm permissão total de leitura, escrita e execução; outros não têm permissão).
    * `/ven`: Proprietário `root`, Grupo `GRP_VEN`, Permissões `770`.
    * `/sec`: Proprietário `root`, Grupo `GRP_SEC`, Permissões `770`.
    * `/public`: Proprietário `root`, Grupo `root`, Permissões `777` (todos têm permissão total de leitura, escrita e execução).

## Como Utilizar

1.  **Clone o Repositório:**
    ```bash
    git clone https://github.com/lucas-pettinelli/lucas-pettinelli-linux-iac-user-diretories-permissions
    cd script
    ```

2.  **Torne o Script Executável:**
    ```bash
    chmod +x iac1.sh
    ```

3.  **Execute o Script como Superusuário (root ou com `sudo`):**
    ```bash
    sudo ./iac1.sh
    ```

    **Atenção:** Este script realiza alterações no sistema, como criação de usuários e diretórios, e modificação de permissões. Execute-o com cautela e apenas em ambientes de teste ou onde as alterações são desejadas.

## Pré-requisitos

* Sistema operacional Linux Ubuntu 18.04.
* Acesso com privilégios de superusuário (root ou `sudo`).
* O utilitário `openssl` deve estar instalado para a geração de senhas criptografadas. Caso não esteja, pode ser instalado com o comando:
    ```bash
    sudo apt update
    sudo apt install openssl
    ```
