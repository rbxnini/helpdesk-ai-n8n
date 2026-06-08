# 🤖 Helpdesk AI Workflow

## 🚀 Visão Geral

Este projeto demonstra uma automação completa para tratamento de chamadas de atendimento utilizando n8n, Inteligência Artificial e integração com plataformas de gerenciamento de tickets.

O objetivo é eliminar tarefas repetitivas executadas após um atendimento telefônico, transformando gravações de chamadas em informações estruturadas de forma totalmente automatizada.

Embora este exemplo tenha sido criado para uma operação de suporte técnico, a arquitetura foi projetada para ser altamente adaptável e pode ser utilizada em diversos cenários de negócio.

---

## 🎯 Objetivo

Em muitas empresas, após finalizar uma ligação, o analista ainda precisa executar diversas tarefas manuais:

* 📝 Registrar o atendimento
* 🎫 Abrir tickets
* 👨‍💻 Informar quem realizou o atendimento
* ⏱️ Registrar duração da chamada
* 📊 Atualizar indicadores
* 📚 Criar documentação do ocorrido
* 📞 Relacionar a ligação ao cliente correto

Essas atividades consomem tempo e aumentam o risco de erros operacionais.

Este workflow automatiza todo esse processo, desde a obtenção da gravação até a criação do ticket final.

<img width="1154" height="657" alt="image" src="https://github.com/user-attachments/assets/d6493efa-d9b3-4405-b720-4e96304c0ef5" />

---

## ⚙️ Como Funciona

### 📞 1. Captura das Gravações

O fluxo realiza periodicamente a busca por novas gravações de chamadas.

Neste exemplo, a obtenção dos arquivos é realizada através de um script Python responsável por consumir uma API de telefonia e armazenar os arquivos localmente para processamento.

A origem das gravações pode ser facilmente substituída por:

* 🌐 APIs REST
* ☁️ Armazenamento em nuvem
* 📂 Compartilhamentos de rede
* 🔐 SFTP
* 📥 FTP
* 🗄️ Bancos de dados
* 🏢 Sistemas proprietários

---

### 🎙️ 2. Transcrição do Áudio

Após localizar uma gravação, o workflow envia o arquivo para uma plataforma de Speech-to-Text.

Neste projeto foi utilizada a AssemblyAI para:

* Converter áudio em texto
* Identificar participantes da conversa
* Estruturar o diálogo
* Melhorar a qualidade da transcrição

Outras alternativas possíveis incluem:

* OpenAI Whisper
* Google Speech-to-Text
* Azure Speech Services
* Amazon Transcribe
* Deepgram
* Speechmatics

---

### 🔄 3. Organização da Conversa

Após a transcrição, o workflow reorganiza as falas por participante.

Essa etapa transforma a transcrição bruta em um formato estruturado, facilitando a interpretação posterior pela Inteligência Artificial.

---

### 🧠 4. Interpretação por Inteligência Artificial

O conteúdo da ligação é enviado para um modelo de linguagem responsável por compreender o contexto do atendimento.

A IA identifica automaticamente:

* 👤 Cliente
* 🏢 Empresa
* ❓ Solicitação realizada
* 💬 Resposta fornecida
* 🏷️ Categorias
* 📌 Tags
* 📊 Status do atendimento

Além disso, a IA gera automaticamente um relatório em Markdown contendo um resumo estruturado da ligação.

Neste exemplo foi utilizado o Google Gemini, mas o fluxo pode utilizar qualquer modelo compatível, como:

* OpenAI GPT
* Claude
* Gemini
* DeepSeek
* Mistral
* Llama
* Ollama (Modelos Locais)

---

### 📝 5. Geração Automática de Relatório

Com base na interpretação da conversa, é criado um documento estruturado contendo:

* 👤 Identificação do cliente
* 🏢 Empresa
* ❓ Solicitação realizada
* 💬 Resposta do suporte
* 📌 Resumo detalhado
* 🏷️ Tags
* 📚 Categoria
* 📊 Status final

Esse conteúdo pode ser utilizado para auditoria, documentação ou atendimento ao cliente.

---

### 🎫 6. Criação Automática de Tickets

Após gerar o relatório, o workflow cria automaticamente um ticket em uma plataforma de atendimento.

Neste exemplo foi utilizado o Zendesk.

Entretanto, a integração pode ser facilmente adaptada para:

* Zendesk
* Jira Service Management
* ServiceNow
* Freshdesk
* GLPI
* OTRS
* Zoho Desk
* Sistemas internos

---

### 📊 7. Registro de Dados Operacionais

Além do relatório gerado pela IA, o sistema também registra informações operacionais importantes.

Exemplos:

* 👨‍💻 Analista responsável
* 📞 Telefone
* ⏰ Horário inicial
* ⏰ Horário final
* ⌛ Tempo de duração
* 🏢 Cliente relacionado
* 📈 Dados para indicadores

Essas informações podem ser utilizadas posteriormente em dashboards e relatórios gerenciais.

---

### 🗄️ 8. Controle de Processamento

Para evitar que uma mesma gravação seja processada mais de uma vez, o workflow utiliza uma camada de persistência.

Neste exemplo foi utilizado o Google Sheets devido à simplicidade de implementação.

Entretanto, qualquer banco de dados ou mecanismo de armazenamento pode ser utilizado.

Exemplos:

* PostgreSQL
* MySQL
* MariaDB
* SQL Server
* Oracle Database
* MongoDB
* Redis
* SQLite
* APIs externas
* Sistemas ERP
* Sistemas proprietários

A substituição dessa camada exige pouca ou nenhuma alteração no restante do fluxo.

---

### 📁 9. Arquivamento das Gravações

Após o processamento completo, a gravação é movida para outra localização através de um segundo script Python.

Esse procedimento evita reprocessamentos e mantém o ambiente organizado.

Dependendo da necessidade da operação, os arquivos podem ser:

* 📦 Arquivados
* ☁️ Enviados para a nuvem
* 🗃️ Movidos para outra pasta
* 🧹 Removidos após retenção
* 🔐 Armazenados para auditoria

---

## 🏗️ Arquitetura Simplificada

```text
📞 Plataforma de Telefonia
            ↓
📥 Download das Gravações
            ↓
⚡ n8n Workflow
            ↓
🎙️ Transcrição de Áudio
            ↓
🔄 Organização do Diálogo
            ↓
🧠 Inteligência Artificial
            ↓
📝 Geração de Markdown
            ↓
🎫 Criação de Ticket
            ↓
📊 Registro de Métricas
            ↓
📁 Arquivamento da Gravação
```

---

## 🛠️ Tecnologias Utilizadas

* ⚡ n8n
* 🐍 Python
* 🎙️ AssemblyAI
* 🧠 Google Gemini
* 📊 Google Sheets
* 🎫 Zendesk

---

## 📋 Funcionalidades

* ✅ Download automático de gravações
* ✅ Transcrição automática de chamadas
* ✅ Separação dos participantes da conversa
* ✅ Interpretação utilizando IA
* ✅ Geração automática de documentação
* ✅ Criação automática de tickets
* ✅ Registro de indicadores operacionais
* ✅ Controle de gravações processadas
* ✅ Arquivamento automático de arquivos

---

## 🔗 Possíveis Substituições

A arquitetura foi criada para ser modular.

### 🧠 Inteligência Artificial

* OpenAI GPT
* Claude
* Gemini
* DeepSeek
* Llama
* Ollama

### 🎙️ Speech-to-Text

* AssemblyAI
* Whisper
* Deepgram
* Google Speech-to-Text
* Azure Speech

### 🗄️ Banco de Dados

* PostgreSQL
* MySQL
* SQL Server
* Oracle
* MongoDB
* Redis

### 🎫 Sistemas de Ticket

* Zendesk
* Jira Service Management
* ServiceNow
* Freshdesk
* GLPI

---

## 🌎 Possíveis Aplicações

Este fluxo pode ser adaptado para diversos tipos de operação:

* 👨‍💻 Help Desk
* 🛠️ Service Desk
* 📞 SAC
* 💰 Cobrança
* 🛒 Vendas
* 🚚 Logística
* 🏥 Clínicas
* 🏢 Atendimento Corporativo
* 👥 Recursos Humanos
* 📋 Auditorias

---

## 📈 Benefícios

* ⏱️ Redução do tempo gasto com documentação
* 📚 Padronização dos registros
* 🎯 Menor risco de erros manuais
* 📊 Melhor qualidade dos indicadores
* 🚀 Maior produtividade operacional
* 🤖 Uso eficiente de Inteligência Artificial
* 🔄 Processo totalmente automatizado

---

## 🏁 Conclusão

Este projeto demonstra como ferramentas modernas de automação podem transformar gravações de chamadas em informações estruturadas e acionáveis.

Ao combinar automação, transcrição de áudio, Inteligência Artificial e integração com plataformas de atendimento, é possível reduzir atividades manuais, acelerar processos internos e melhorar significativamente a qualidade dos registros operacionais.

Abaixo mostro um exemplo concluido de uma ligação analisada, transcrita e adicionada a plataforma de tickets ja direcionado ao cliente contendo todos os dados do atendimento e o tempo que o analista levou para concluir o atendimento.


