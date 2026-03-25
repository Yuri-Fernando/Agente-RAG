# Agente-RAG
#  Agente RAG Multicanal com Telegram, Google Drive e Supabase

Este projeto implementa um **Agente RAG (Retrieval-Augmented Generation)** no **n8n**, integrado ao **Google Drive**, **Supabase** e **Telegram**, para consultas inteligentes em documentos e gerenciamento de agenda com suporte a **texto, áudio e imagens**.

---

##  Funcionalidades

### 1. 📂 Ingestão e Indexação de Documentos
- Monitora uma pasta no **Google Drive** em busca de novos ou atualizados arquivos.
- Remove versões antigas no **Supabase** para evitar duplicação.
- Faz o **download e extração** do conteúdo.
- Gera **embeddings com OpenAI**.
- Armazena os vetores semânticos no **Supabase** (Vector Store).

 Resultado: todos os documentos ficam disponíveis para **busca semântica** pelo agente.

---

### 2.  Agente de IA (RAG)
- Baseado no **GPT-4o-mini (OpenAI)** com memória de conversação.
- Conectado ao **Supabase Vector Store** para **responder perguntas com base nos documentos**.
- Pode ser acessado via:
  - Webhook/API
  - Chat
  - **Telegram**

---

### 3.  Interação no Telegram
O bot no Telegram entende e responde a múltiplos formatos:

- **Texto** → consulta direta ao agente.
- **Áudio** → transcrição com **OpenAI Whisper** + resposta do agente.
- **Imagem** → análise via GPT-4o-mini com visão.
- **Fallback** → mensagens não reconhecidas recebem aviso amigável.

---

### 4.  Integração com Google Calendar
O agente também é capaz de gerenciar eventos:

- Buscar compromissos existentes.
- Criar novos eventos (checando disponibilidade).
- Atualizar eventos existentes (`eventID` necessário).
- Perguntar informações faltantes (nome, data, hora, descrição).

Tudo isso de forma **conversacional pelo Telegram**.

---

##  Tecnologias Utilizadas
- [n8n](https://n8n.io/) → orquestração dos fluxos
- [Google Drive API](https://developers.google.com/drive) → ingestão de arquivos
- [Supabase](https://supabase.com/) → armazenamento vetorial (Vector Store)
- [OpenAI](https://openai.com/) → GPT-4o-mini, Embeddings e Whisper
- [Telegram Bot API](https://core.telegram.org/bots/api) → interface de chat
- [Google Calendar API](https://developers.google.com/calendar) → gerenciamento de eventos

---

##  Casos de Uso
-  Criar um **FAQ inteligente** a partir de documentos no Google Drive.
-  Consultar informações específicas de relatórios e contratos via chat.
-  Permitir que usuários falem por voz e recebam respostas naturais.
-  Analisar imagens enviadas por usuários.
-  Agendar reuniões e eventos diretamente pelo Telegram.

---

##  Como Rodar

1. Clone este repositório:
   ```bash
   git clone https://github.com/seu-usuario/seu-repo.git


Configure as credenciais no n8n:
Google Drive
Google Calendar
Supabase
OpenAI
Telegram Bot
Importe o fluxo AGENTE_RAG.json no n8n.

Ative o workflow e comece a interagir pelo Telegram 🎉

 Observações

O fluxo foi pensado para aulas de NoCode + IA, servindo como um template completo de RAG multimodal.
Pode ser facilmente expandido para integrar novas fontes (Notion, Slack, etc).

💡 Sinta-se à vontade para contribuir com melhorias, issues ou novas ideias!
