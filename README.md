# R.A. BOT – Assistente Inteligente de Chamados Nível 1

Este repositório contém o MVP do **R.A. BOT**, um sistema open-source para otimizar o atendimento de chamados N1, resolvendo via IA questões que normalmente travariam o suporte humano.

## Motivação

✔️ **Reduzir o volume de tickets N1** que poderiam ser solucionados com uma simples pesquisa em IA  
✔️ Acelerar o tempo de resposta e liberar a equipe de suporte para casos críticos  

## Funcionalidades do MVP

1. **Chatbot via n8n + GroqCloud**  
   - Webhook recebe a pergunta  
   - Chamada à API GroqCloud (você pode trocar de LLM depois)  
   - Persistência da pergunta+resposta em **MySQL**  
   - Memória de curto prazo: dados válidos por até 24 horas  
2. **Página Web simples (Flask + HTML/CSS)**  
   - Interface de chat para usuários  
   - Exibe histórico de conversas  
3. **Manual “fake” de suporte**  
   - Arquivo em `./docs/manual.md` com FAQs e instruções de uso  
   - Ingestão desse documento no n8n (via GroqCloud) para consultas contextuais  
4. **Containerizado em Kubernetes local (Minikube)**  
   - Tudo orquestrado via Helm Charts  
   - Ambientes isolados para n8n, web e MySQL  
5. **Infraestrutura como Código**  
   - Helm Charts para deploy  
   - Docker Compose para desenvolvimento local (opcional)  
   - Futuro provisionamento via Ansible  

## Estrutura de Pastas

.
├── ansible
│   └── playbook-init.yml
├── charts
│   └── ra-bot
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates
│           └── .gitkeep
├── docs
│   └── manual.md
├── images
├── mysql
│   └── init.sql
├── web
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── app.py
│   └── templates
│       └── index.html
├── docker-compose.yml
├── pod-hello.yaml
└── README.md


## Cronograma Sprint de 7 Dias (MVP)

| Dia | Entrega                                                                 |
|-----|-------------------------------------------------------------------------|
| 1   | Setup: VS Code, GitHub, Minikube, Pod de teste, README + Post inicial   |
| 2   | Helm Chart & deploy hello-world via Helm + webhook n8n                  |
| 3   | Workflow n8n: entrada + chamada GroqCloud LLM                           |
| 4   | Workflow n8n: nó MySQL para persistência (24h)                          |
| 5   | App Flask: página de chat e integração com webhook n8n                  |
| 6   | Deploy Flask no K8s + Service; testes ponta-a-ponta                     |
| 7   | CI/CD: GitHub Actions com `helm upgrade`; wrap-up e docs finais         |

> **Próximo passo:** Dia 2 – scaffold do Helm Chart para n8n e web, deploy de testes e publicação do Post 2 no LinkedIn!