# Helpdesk AI Workflow

## Visão Geral

Este projeto demonstra uma automação completa de tratamento de chamadas de atendimento utilizando n8n, Inteligência Artificial e integração com plataformas de gestão de tickets.

O objetivo é reduzir o tempo gasto pelos analistas com atividades administrativas após um atendimento telefônico, automatizando todo o processo de interpretação, documentação e registro das informações da chamada.

Embora o exemplo tenha sido desenvolvido para um cenário de suporte técnico, a arquitetura apresentada pode ser adaptada para diversos tipos de operações que dependam de gravações de chamadas, transcrição de áudio, análise de conversas e geração automática de registros.

---

## Problema

Em muitas operações de atendimento, os analistas precisam:

* Ouvir ou revisar chamadas gravadas;
* Registrar manualmente informações do atendimento;
* Criar tickets ou históricos;
* Preencher dados operacionais;
* Documentar a solução fornecida ao cliente;
* Controlar métricas de atendimento.

Essas atividades consomem tempo e frequentemente geram inconsistências devido ao preenchimento manual.

Este workflow automatiza esse processo do início ao fim.

---

## Como Funciona

O fluxo executa periodicamente uma busca por novas gravações de chamadas.

Após localizar novos arquivos, cada gravação passa pelas seguintes etapas:

### 1. Captura da Gravação

As chamadas são obtidas de uma plataforma externa de telefonia.

No exemplo disponibilizado, o download das gravações é realizado através de um script Python responsável por consumir a API da plataforma de telefonia e armazenar os arquivos localmente.

O método de obtenção dos áudios pode ser facilmente substituído por:

* APIs REST
* FTP
* SFTP
* Armazenamento em nuvem
* Compartilhamentos de rede
* Bancos de dados
* Sistemas proprietários

---

### 2. Envio para Transcrição

Após a captura, os arquivos de áudio são enviados para um serviço especializado de transcrição.

No exemplo foi utilizada a API da AssemblyAI, responsável por:

* Converter áudio em texto;
* Identificar falantes;
* Organizar o diálogo;
* Retornar a transcrição estruturada.

Outras soluções equivalentes também podem ser utilizadas:

* OpenAI Whisper
* Google Speech-to-Text
* Azure Speech Services
* Amazon Transcribe
* Deepgram
* Speechmatics

---

### 3. Estruturação do Diálogo

Após a transcrição, o workflow organiza as falas por participante.

Essa etapa transforma a transcrição bruta em uma estrutura mais compreensível para posterior análise por Inteligência Artificial.

---

### 4. Interpretação por IA

O conteúdo da ligação é enviado para um modelo de linguagem responsável por interpretar o contexto da conversa.

A IA identifica:

* Quem é o cliente;
* Qual foi a solicitação realizada;
* Qual ação foi executada pelo suporte;
* O resultado final do atendimento;
* Categorias relacionadas ao assunto;
* Tags para classificação futura.

Além disso, a IA gera automaticamente um relatório em formato Markdown.

No exemplo foi utilizado o Google Gemini, porém a arquitetura permite utilizar qualquer modelo compatível, como:

* OpenAI GPT
* Claude
* Gemini
* Mistral
* Llama
* DeepSeek
* Modelos locais através de Ollama

---

### 5. Geração Automática do Ticket

Após a interpretação da chamada, o sistema cria automaticamente um ticket em uma plataforma de atendimento.

No exemplo foi utilizado o Zendesk, porém o mesmo conceito pode ser aplicado a:

* Freshdesk
* Jira Service Management
* ServiceNow
* GLPI
* OTRS
* Zoho Desk
* Sistemas internos

O ticket é criado já contendo:

* Resumo do atendimento;
* Descrição detalhada;
* Classificação do caso;
* Tags;
* Informações operacionais.

---

### 6. Registro de Informações Operacionais

Além do conteúdo gerado pela IA, o fluxo também registra automaticamente informações da chamada, como:

* Nome do analista;
* Horário de início;
* Horário de término;
* Duração da ligação;
* Identificação do cliente;
* Dados adicionais necessários para indicadores e relatórios.

---

### 7. Controle de Processamento

Para evitar reprocessamento de gravações já tratadas, o workflow utiliza uma base de controle.

No exemplo foi utilizada uma planilha Google Sheets devido à simplicidade de implementação.

Entretanto, qualquer solução de armazenamento pode ser utilizada, incluindo:

* PostgreSQL
* MySQL
* MariaDB
* SQL Server
* Oracle
* MongoDB
* Redis
* SQLite
* APIs externas
* Sistemas ERP
* Sistemas proprietários

A camada de persistência pode ser substituída sem impacto significativo no restante do fluxo.

---

### 8. Arquivamento da Gravação

Após o processamento completo, a gravação é movida para outra localização através de um script Python.

Esse procedimento impede que arquivos já processados sejam tratados novamente e permite manter um histórico organizado.

Dependendo da necessidade da operação, os arquivos podem:

* Ser arquivados;
* Ser movidos para outro diretório;
* Ser enviados para armazenamento em nuvem;
* Ser compactados;
* Ser excluídos após retenção definida.

---

## Arquitetura Simplificada

```text
Plataforma de Telefonia
          ↓
Download das Gravações
          ↓
        n8n
          ↓
Transcrição de Áudio
          ↓
Estruturação do Diálogo
          ↓
IA Generativa
          ↓
Geração de Relatório Markdown
          ↓
Criação de Ticket
          ↓
Registro de Métricas
          ↓
Arquivamento da Gravação
```

---

## Tecnologias Utilizadas no Exemplo

* n8n
* Python
* AssemblyAI
* Google Gemini
* Google Sheets
* Zendesk

---

## Adaptabilidade

Uma das principais vantagens deste projeto é sua flexibilidade.

Embora o fluxo tenha sido desenvolvido para uma operação de suporte técnico, a mesma estrutura pode ser aplicada em diversos cenários:

* Help Desk
* Service Desk
* SAC
* Centrais de Atendimento
* Cobrança
* Vendas
* Recursos Humanos
* Clínicas
* Escritórios
* Operações logísticas
* Centrais de relacionamento

Qualquer processo que envolva gravações de chamadas e necessidade de documentação pode se beneficiar desse modelo.

---

## Objetivo

Demonstrar como ferramentas de automação, APIs de transcrição e modelos de Inteligência Artificial podem ser combinados para transformar atendimentos telefônicos em informações estruturadas, reduzindo atividades manuais, aumentando a produtividade da equipe e melhorando a qualidade dos registros operacionais.
