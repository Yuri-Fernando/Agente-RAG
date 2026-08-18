# Agente-RAG

### Agente RAG Multicanal · n8n · Telegram · Google Drive · Supabase · IA Generativa

## Status

🔵 **Pesquisa / P&D — Projeto experimental de pesquisa aplicada**

Projeto desenvolvido como parte de uma linha contínua de **Pesquisa e Desenvolvimento em n8n, RAG, IA generativa, automação e arquitetura de soluções SaaS**.

O projeto explora a construção de um agente inteligente capaz de integrar **documentos, memória, canais de comunicação, busca semântica e automação de agenda** em um único workflow.

A arquitetura foi desenvolvida para investigar como workflows em n8n podem evoluir de automações isoladas para **sistemas reutilizáveis de IA, agentes multimodais e componentes aplicáveis a produtos SaaS**.

---

## Sobre o Projeto

O **Agente-RAG** implementa um agente baseado em **Retrieval-Augmented Generation (RAG)** utilizando n8n como camada de orquestração, Google Drive como fonte documental, Supabase como armazenamento vetorial e Telegram como canal de interação.

O sistema também integra OpenAI para geração de embeddings, processamento de linguagem, transcrição de áudio e análise de imagens.

Além das consultas sobre documentos, o agente possui integração com **Google Calendar**, permitindo consultar disponibilidade e gerenciar eventos por meio de conversação.

```text
Google Drive
     ↓
Ingestão
     ↓
Extração de conteúdo
     ↓
Embeddings
     ↓
Supabase Vector Store
     ↓
RAG Agent
     ↓
Telegram / API / Chat
     ↓
Resposta contextual
```

---

## Objetivo

O projeto foi desenvolvido para investigar aplicações de:

- Retrieval-Augmented Generation;
- Agentes conversacionais;
- Automação com n8n;
- Busca semântica;
- Integração entre múltiplas APIs;
- Processamento multimodal;
- Automação de documentos;
- Automação de agenda;
- Arquiteturas reutilizáveis para SaaS;
- IA aplicada a workflows e processos.

---

## Funcionalidades

### 1. Ingestão e Indexação de Documentos

O workflow monitora uma pasta do **Google Drive** para identificar arquivos novos ou atualizados.

Processo:

```text
Google Drive
     ↓
Detectar novo / atualizado
     ↓
Remover versão anterior
     ↓
Download
     ↓
Extração do conteúdo
     ↓
Geração de embeddings
     ↓
Supabase Vector Store
```

### Recursos

- Monitoramento de arquivos;
- Atualização de documentos;
- Remoção de versões antigas;
- Download automático;
- Extração de conteúdo;
- Geração de embeddings com OpenAI;
- Armazenamento vetorial no Supabase;
- Busca semântica.

O objetivo é manter a base documental atualizada e disponível para recuperação contextual pelo agente.

---

### 2. Agente de IA com RAG

O agente utiliza **GPT-4o-mini** integrado ao Supabase Vector Store.

O fluxo combina:

- Prompt;
- Memória de conversação;
- Busca semântica;
- Contexto dos documentos;
- Geração de respostas.

```text
Pergunta
   ↓
Retriever
   ↓
Supabase Vector Store
   ↓
Documentos relevantes
   ↓
Contexto
   ↓
GPT-4o-mini
   ↓
Resposta
```

O agente pode ser acessado por:

- Webhook/API;
- Chat;
- Telegram.

---

### 3. Interação Multicanal no Telegram

O bot suporta diferentes formatos de entrada.

#### Texto

Consulta diretamente o agente RAG.

#### Áudio

```text
Áudio
  ↓
OpenAI Whisper
  ↓
Transcrição
  ↓
RAG Agent
  ↓
Resposta
```

#### Imagem

```text
Imagem
  ↓
GPT-4o-mini Vision
  ↓
Análise
  ↓
Agente
  ↓
Resposta
```

#### Fallback

Mensagens não reconhecidas recebem uma resposta apropriada ao contexto do workflow.

---

### 4. Memória Conversacional

O agente utiliza memória para manter o contexto das interações realizadas durante a conversa.

A memória permite que perguntas relacionadas possam ser interpretadas considerando o histórico anterior.

```text
Mensagem Atual
      ↓
Memória
      ↓
Contexto da Conversa
      ↓
RAG
      ↓
Resposta
```

---

### 5. Integração com Google Calendar

Além da recuperação de conhecimento, o agente pode executar operações relacionadas à agenda.

### Operações disponíveis

- Buscar compromissos;
- Verificar disponibilidade;
- Criar eventos;
- Atualizar eventos existentes;
- Solicitar informações faltantes;
- Trabalhar com `eventID` para atualização.

Exemplo de fluxo:

```text
Usuário:
"Agende uma reunião amanhã às 15h"

        ↓

Agente
        ↓
Verifica informações
        ↓
Google Calendar
        ↓
Verifica disponibilidade
        ↓
Cria evento
        ↓
Confirmação pelo Telegram
```

Quando faltam informações, o agente pode solicitar dados como:

- Nome;
- Data;
- Horário;
- Descrição.

---

# Arquitetura

```text
                        ┌───────────────────┐
                        │    Google Drive   │
                        │  Document Sources │
                        └─────────┬─────────┘
                                  │
                                  ▼
                        ┌───────────────────┐
                        │       n8n         │
                        │   Ingestion Flow  │
                        └─────────┬─────────┘
                                  │
                                  ▼
                        ┌───────────────────┐
                        │ Embeddings OpenAI │
                        └─────────┬─────────┘
                                  │
                                  ▼
                        ┌───────────────────┐
                        │ Supabase Vector   │
                        │      Store        │
                        └─────────┬─────────┘
                                  │
                                  ▼
                        ┌───────────────────┐
                        │    RAG Agent      │
                        │   GPT-4o-mini     │
                        └─────────┬─────────┘
                                  │
                 ┌────────────────┼────────────────┐
                 ▼                ▼                ▼
          ┌─────────────┐  ┌─────────────┐  ┌──────────────┐
          │  Telegram   │  │ Webhook/API │  │ Google       │
          │   Channel   │  │             │  │ Calendar     │
          └─────────────┘  └─────────────┘  └──────────────┘
```

---

# Fluxo Geral

```text
1. Documento é criado ou atualizado no Google Drive
        ↓
2. n8n detecta a alteração
        ↓
3. Documento é baixado
        ↓
4. Conteúdo é extraído
        ↓
5. Embeddings são gerados
        ↓
6. Vetores são armazenados no Supabase
        ↓
7. Usuário envia mensagem
        ↓
8. Telegram / API recebe a solicitação
        ↓
9. Agente interpreta a entrada
        ↓
10. Busca semântica recupera documentos relevantes
        ↓
11. GPT-4o-mini gera a resposta
        ↓
12. Quando necessário, Google Calendar executa ações
        ↓
13. Resposta retorna ao usuário
```

---

# Tecnologias Utilizadas

| Categoria | Tecnologias |
|---|---|
| Orquestração | **n8n** |
| LLM | **OpenAI GPT-4o-mini** |
| Embeddings | **OpenAI Embeddings** |
| Speech-to-Text | **OpenAI Whisper** |
| Vision | **GPT-4o-mini Vision** |
| Vector Store | **Supabase** |
| Documentos | **Google Drive API** |
| Chat | **Telegram Bot API** |
| Agenda | **Google Calendar API** |
| Integração | **Webhook / REST API** |

---

# Arquitetura RAG

O pipeline segue a estrutura clássica de Retrieval-Augmented Generation:

```text
Documents
    ↓
Chunking / Processing
    ↓
Embeddings
    ↓
Vector Store
    ↓
Semantic Retrieval
    ↓
Relevant Context
    ↓
LLM
    ↓
Generated Answer
```

A diferença é que o fluxo utiliza o **n8n como camada de orquestração**, conectando as etapas de ingestão, armazenamento, recuperação e interação.

---

# Integração com Google Drive

O Google Drive atua como fonte documental do sistema.

O workflow pode:

- Monitorar uma pasta;
- Detectar arquivos novos;
- Detectar alterações;
- Remover versões anteriores;
- Atualizar embeddings;
- Manter a base vetorial sincronizada.

Isso permite utilizar uma coleção documental dinâmica como fonte de conhecimento para o agente.

---

# Integração com Supabase

O Supabase atua como camada de armazenamento vetorial.

Responsabilidades:

- Armazenamento dos embeddings;
- Persistência dos documentos processados;
- Busca semântica;
- Manutenção da base de conhecimento.

```text
Documento
   ↓
Embedding
   ↓
Supabase
   ↓
Semantic Search
   ↓
Context
```

---

# Integração com Telegram

O Telegram funciona como principal interface conversacional.

O agente suporta:

- Texto;
- Áudio;
- Imagem;
- Conversas contextualizadas;
- Consultas RAG;
- Operações de agenda.

---

# Casos de Uso

### FAQ Inteligente

Criar uma base de perguntas e respostas utilizando documentos armazenados no Google Drive.

### Consulta Documental

Permitir consultas sobre:

- Relatórios;
- Contratos;
- Documentos;
- Procedimentos;
- Materiais internos.

### Assistente Multimodal

Permitir que usuários enviem:

- Texto;
- Áudio;
- Imagens.

### Agendamento Inteligente

Permitir criar e consultar compromissos pelo Telegram.

### Knowledge Assistant

Utilizar documentos como fonte de conhecimento para um agente conversacional.

### SaaS

A arquitetura pode servir como base experimental para produtos SaaS de:

- Assistentes corporativos;
- Knowledge Bases;
- Atendimento automatizado;
- Document Intelligence;
- Consultas internas;
- Agentes especializados.

---

# Pesquisa em n8n, RAG e SaaS

Este projeto faz parte da mesma linha de **Pesquisa e Desenvolvimento em automação inteligente** utilizada em outros experimentos com n8n.

A investigação busca combinar:

```text
n8n
 +
RAG
 +
LLMs
 +
Memória
 +
APIs
 +
Automação
 +
SaaS
```

A intenção é construir componentes reutilizáveis que possam ser incorporados em diferentes agentes e produtos baseados em IA.

O projeto explora especialmente como o n8n pode funcionar como uma camada de **orquestração de agentes**, conectando dados, ferramentas, canais e serviços externos sem acoplar toda a solução a uma única aplicação.

---

# O que este projeto demonstra

- Implementação de RAG;
- Engenharia de workflows com n8n;
- Integração de LLMs;
- Embeddings;
- Busca semântica;
- Vector Stores;
- Memória conversacional;
- Processamento multimodal;
- Speech-to-Text;
- Vision;
- Integração com Google Drive;
- Integração com Telegram;
- Integração com Google Calendar;
- Integração com APIs REST;
- Automação orientada a eventos;
- Construção de agentes de IA;
- Arquitetura reutilizável para SaaS;
- Pesquisa aplicada em Agentic AI.

---

# Como Executar

## 1. Clonar o repositório

```bash
git clone https://github.com/seu-usuario/seu-repo.git
cd seu-repo
```

## 2. Configurar o n8n

Disponibilize uma instância do n8n e configure as credenciais necessárias.

## 3. Configurar integrações

Configure:

- Google Drive;
- Google Calendar;
- Supabase;
- OpenAI;
- Telegram Bot.

## 4. Importar o workflow

Importe o arquivo:

```text
AGENTE_RAG.json
```

para o n8n.

## 5. Configurar credenciais

Associe as credenciais aos respectivos nodes do workflow.

## 6. Ativar o workflow

Após a configuração das integrações, ative o workflow e utilize o Telegram para interagir com o agente.

---

# Segurança e Configuração

Nunca publique:

- API Keys;
- Tokens;
- Credenciais de bots;
- Credenciais do Google;
- Chaves do Supabase;
- Secrets de Webhooks.

Utilize variáveis de ambiente e as credenciais internas do n8n.

---

# Limitações

- O sistema depende dos serviços externos utilizados;
- A qualidade do RAG depende da qualidade e atualização dos documentos;
- A qualidade das respostas depende do modelo LLM;
- Processamento de áudio depende da qualidade da transcrição;
- Análise de imagens depende das capacidades do modelo utilizado;
- A arquitetura depende da disponibilidade do n8n e das APIs integradas;
- A versão atual é uma aplicação de pesquisa e portfólio, não uma plataforma SaaS comercial completa.

---

# Melhorias Futuras

- Interface web própria;
- Multi-tenant;
- Autenticação de usuários;
- Dashboard de utilização;
- Analytics de consultas;
- Avaliação automática de respostas;
- Reranking de documentos;
- Hybrid Search;
- RAG multimodal mais avançado;
- Memória de longo prazo;
- Agent routing;
- Integração com Slack;
- Integração com Notion;
- Integração com Microsoft Teams;
- API própria;
- Containerização;
- Observabilidade;
- Versionamento da base de conhecimento;
- Painel SaaS para gerenciamento de agentes.

---

# Status Final

🔵 **Pesquisa / P&D — Projeto experimental de pesquisa aplicada**

O projeto está concluído em sua versão atual e documentado como uma implementação funcional de **RAG multimodal com n8n**, integrando documentos, busca semântica, LLMs, memória, Telegram e Google Calendar.

Ele faz parte de uma linha contínua de pesquisa aplicada em **n8n, Agentic AI, RAG, automação, marketing e SaaS**, servindo como base para novos experimentos e componentes reutilizáveis em futuras soluções de IA.

---

# Licença

MIT License.

---

# Autor

**Yuri Fernando Dubbern**

AI/ML Engineer · Generative AI · Agentic AI · Intelligent Automation · n8n · RAG · SaaS

[LinkedIn](https://www.linkedin.com/in/yuridubbern) · [GitHub](https://github.com/Yuri-Fernando) · [Lattes](http://lattes.cnpq.br/7151392692642166) · [Linktree](https://linktr.ee/yuri.f.dubbern)
