# PoC CI/CD com Harness, Bitbucket e Concourse

Este repositório contém a configuração para uma Prova de Conceito (PoC) de um pipeline de CI/CD, utilizando as seguintes tecnologias:

*   **Harness:** Para orquestração de deploy e CI/CD.
*   **Bitbucket:** Como repositório de código-fonte.
*   **Concourse:** Para automação de pipelines.

## Arquitetura

A arquitetura desta PoC é baseada em contêineres Docker, orquestrados pelo `docker-compose.yml`. Os principais serviços são:

*   **Bitbucket:** Uma instância do Atlassian Bitbucket para gerenciamento de repositórios Git.
*   **Concourse:** Uma instância do Concourse CI, com seu respectivo banco de dados PostgreSQL, para automação de pipelines.
*   **Harness On-Premise:** Um conjunto completo de serviços da plataforma Harness, incluindo:
    *   **`manager` e `ng-manager`:** Serviços principais da plataforma Harness.
    *   **`pipeline-service`:** Serviço para gerenciamento de pipelines.
    *   **`platform-service`:** Serviço para gerenciamento da plataforma.
    *   **`mongo` e `redis`:** Bancos de dados utilizados pela plataforma Harness.
    *   **`proxy` (Nginx):** Um reverse proxy que expõe os serviços da plataforma Harness em uma única porta.
    *   Outros microserviços que compõem a plataforma.

## Estrutura de Pastas

*   **`config/`**: Contém os arquivos de configuração para os serviços.
    *   **`mongo/`**: Arquivo de configuração do MongoDB.
    *   **`nginx/`**: Arquivo de configuração do Nginx, que atua como reverse proxy para os serviços do Harness.
*   **`environment/`**: Contém os arquivos de variáveis de ambiente para os serviços do Harness.
*   **`scripts/`**: Contém scripts utilitários.
    *   **`wait-for-it.sh`**: Script para aguardar a inicialização de um serviço antes de iniciar outro.

## Como Utilizar

1.  **Pré-requisitos:**
    *   Docker
    *   Docker Compose

2.  **Inicialização:**
    *   Clone este repositório.
    *   Execute o seguinte comando na raiz do projeto para iniciar todos os serviços:
        ```bash
        docker-compose up -d
        ```

3.  **Acessando os Serviços:**
    *   **Bitbucket:** [http://localhost:7990](http://localhost:7990)
    *   **Concourse:** [http://localhost:8080](http://localhost:8080)
        *   **Usuário:** `test`
        *   **Senha:** `test`
    *   **Harness:** [http://localhost:8088](http://localhost:8088)

## Observações

*   A inicialização de todos os serviços pode levar alguns minutos.
*   Os dados do Bitbucket e do MongoDB são persistidos em volumes do Docker (`bitbucket_home` e `mongo_data`, respectivamente).
