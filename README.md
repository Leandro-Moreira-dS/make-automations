# make-automations

Coleção de automações profissionais construídas no **Make.com** (antigo Integromat).

Cada cenário resolve um problema real de negócio — geração de conteúdo com IA, gestão de e-commerce, marketing no LinkedIn e monitoramento de performance de anúncios. Os blueprints estão prontos para importar diretamente no Make.com.

---

## Automações

| # | Nome | Integrações | O que faz |
|---|------|-------------|-----------|
| 01 | [Blogs Automatizados](#01---blogs-automatizados) | WooCommerce · Gemini AI · OpenAI · WordPress · Google Sheets | Gera e publica posts de blog automaticamente a partir de produtos da loja |
| 02 | [PAAI — Produto Automatizado com IA](#02---paai--produto-automatizado-com-ia) | WooCommerce · Gemini AI · Google Sheets | Reescreve descrições de produtos com IA e atualiza direto no WooCommerce |
| 03 | [LinkedIn Auto Post](#03---linkedin-auto-post) | OpenAI · DALL-E · LinkedIn · Google Sheets | Gera e publica posts com imagem no LinkedIn automaticamente |
| 04 | [Atualização de Saldos — Meta Ads](#04---atualização-de-saldos--meta-ads) | Facebook Ads API · AI Agent · Google Sheets | Monitora saldo de contas de anúncio e atualiza planilha de clientes |
| 05 | [Atualiza Produtos na Planilha](#05---atualiza-produtos-na-planilha) | WooCommerce · Google Sheets | Sincroniza catálogo de produtos do WooCommerce com Google Sheets |
| 06 | [Generate LinkedIn Post (AI Agent)](#06---generate-linkedin-post-ai-agent) | AI Agent · Make Datastore | Gera posts para LinkedIn usando AI Agent com memória entre execuções |

---

## Como importar um blueprint

1. Acesse [make.com](https://make.com) e abra sua organização
2. Clique em **Scenarios → Create a new scenario**
3. Clique nos três pontos `···` no canto superior direito → **Import Blueprint**
4. Selecione o arquivo `.json` da pasta correspondente
5. Reconecte as credenciais (Google Sheets, WooCommerce, OpenAI, etc.)
6. Ajuste os IDs de planilha e configurações específicas do seu ambiente
7. Ative o cenário

---

## 01 — Blogs Automatizados

**Versões:** v3.0 (Gemini AI) · v4.0 (OpenAI GPT)

Lê produtos pendentes de uma planilha Google Sheets, busca os detalhes do produto no WooCommerce, gera um post de blog completo com IA (título, conteúdo, categorias e tags) e publica automaticamente no WordPress — marcando o item como processado na planilha.

**Fluxo:**

```
Google Sheets (filtro: status = pendente)
  → WooCommerce (busca dados do produto)
    → Gemini AI / OpenAI (gera post completo)
      → WordPress (cria post com categoria e tag)
        → Google Sheets (marca como publicado)
```

**Integrações:**
![Make](https://img.shields.io/badge/Make.com-6D00CC?style=flat-square&logo=make&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat-square&logo=googlesheets&logoColor=white)
![WooCommerce](https://img.shields.io/badge/WooCommerce-96588A?style=flat-square&logo=woocommerce&logoColor=white)
![WordPress](https://img.shields.io/badge/WordPress-21759B?style=flat-square&logo=wordpress&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini%20AI-4285F4?style=flat-square&logo=google&logoColor=white)

**Blueprints:** [`blueprint-v3.json`](./01-blogs-automatizados/blueprint-v3.json) · [`blueprint-v4.json`](./01-blogs-automatizados/blueprint-v4.json)

---

## 02 — PAAI — Produto Automatizado com IA

Lê produtos com descrição pendente numa planilha, busca os dados originais no WooCommerce, usa o **Gemini AI** (com AI Agent) para reescrever a descrição de forma otimizada para SEO e conversão, e atualiza o produto direto no WooCommerce.

**Fluxo:**

```
Google Sheets (filtro: descrição = pendente)
  → WooCommerce (busca produto por ID)
    → AI Agent + Gemini Pro (reescreve descrição)
      → WooCommerce (atualiza produto)
        → Google Sheets (marca como concluído)
```

**Integrações:**
![Make](https://img.shields.io/badge/Make.com-6D00CC?style=flat-square&logo=make&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat-square&logo=googlesheets&logoColor=white)
![WooCommerce](https://img.shields.io/badge/WooCommerce-96588A?style=flat-square&logo=woocommerce&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini%20AI-4285F4?style=flat-square&logo=google&logoColor=white)

**Blueprint:** [`blueprint.json`](./02-paai-produto-automatizado/blueprint.json)

---

## 03 — LinkedIn Auto Post

Lê uma lista de temas de uma planilha Google Sheets, gera um post profissional com **OpenAI GPT**, cria uma imagem de capa com **DALL-E**, publica tudo no **LinkedIn** e registra o post na planilha com data e status.

**Fluxo:**

```
Google Sheets (filtro: status = aguardando)
  → OpenAI GPT (gera texto do post)
    → DALL-E (gera imagem de capa)
      → LinkedIn (publica post com imagem)
        → Google Sheets (registra publicação)
```

**Integrações:**
![Make](https://img.shields.io/badge/Make.com-6D00CC?style=flat-square&logo=make&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat-square&logo=googlesheets&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white)
![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)

**Blueprint:** [`blueprint.json`](./03-linkedin-auto-post/blueprint.json)

---

## 04 — Atualização de Saldos — Meta Ads

Consulta o saldo de contas de anúncio no **Facebook Ads API**, usa um **AI Agent** para interpretar e formatar os dados, e atualiza automaticamente a planilha de controle de clientes no Google Sheets. Ideal para agências gerenciando múltiplas contas de anúncio.

**Fluxo:**

```
Trigger (agendado)
  → Facebook Ads API (consulta saldo e dados da conta)
    → AI Agent (interpreta e formata resposta)
      → Google Sheets (atualiza célula do cliente)
```

**Integrações:**
![Make](https://img.shields.io/badge/Make.com-6D00CC?style=flat-square&logo=make&logoColor=white)
![Meta Ads](https://img.shields.io/badge/Meta%20Ads-0866FF?style=flat-square&logo=meta&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat-square&logo=googlesheets&logoColor=white)
![AI Agent](https://img.shields.io/badge/AI%20Agent-412991?style=flat-square&logo=openai&logoColor=white)

**Blueprint:** [`blueprint.json`](./04-atualizacao-saldos/blueprint.json)

---

## 05 — Atualiza Produtos na Planilha

Sincroniza o catálogo de produtos do **WooCommerce** com uma planilha **Google Sheets**. Percorre todos os produtos, verifica se já existem na planilha e adiciona os novos automaticamente com nome, descrição, preço e status.

**Fluxo:**

```
WooCommerce (busca todos os produtos)
  → Aggregator (agrupa resultados)
    → Feeder (itera produto a produto)
      → Google Sheets (verifica se existe)
        → Google Sheets (adiciona se novo)
```

**Integrações:**
![Make](https://img.shields.io/badge/Make.com-6D00CC?style=flat-square&logo=make&logoColor=white)
![WooCommerce](https://img.shields.io/badge/WooCommerce-96588A?style=flat-square&logo=woocommerce&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=flat-square&logo=googlesheets&logoColor=white)

**Blueprint:** [`blueprint.json`](./05-atualiza-produtos-planilha/blueprint.json)

---

## 06 — Generate LinkedIn Post (AI Agent)

Usa um **AI Agent com memória** (Make Datastore) para gerar posts de LinkedIn com contexto acumulado entre execuções. O agente consulta posts anteriores no Datastore para evitar repetição de temas e garantir variedade de conteúdo.

**Fluxo:**

```
Datastore (busca posts anteriores)
  → AI Agent (gera novo post evitando repetições)
    → JSON Parser (estrutura o output)
      → Datastore (salva o novo post)
```

**Integrações:**
![Make](https://img.shields.io/badge/Make.com-6D00CC?style=flat-square&logo=make&logoColor=white)
![AI Agent](https://img.shields.io/badge/AI%20Agent-412991?style=flat-square&logo=openai&logoColor=white)
![Datastore](https://img.shields.io/badge/Make%20Datastore-6D00CC?style=flat-square&logo=make&logoColor=white)

**Blueprint:** [`blueprint.json`](./06-generate-linkedin-post/blueprint.json)

---

## Estrutura do Repositório

```
make-automations/
├── 01-blogs-automatizados/
│   ├── blueprint-v3.json       # Versão com Gemini AI
│   └── blueprint-v4.json       # Versão com OpenAI GPT
├── 02-paai-produto-automatizado/
│   └── blueprint.json
├── 03-linkedin-auto-post/
│   └── blueprint.json
├── 04-atualizacao-saldos/
│   └── blueprint.json
├── 05-atualiza-produtos-planilha/
│   └── blueprint.json
└── 06-generate-linkedin-post/
    └── blueprint.json
```

---

## Autor

**Leandro Moreira**
[LinkedIn](https://www.linkedin.com/in/leandro-moreira-dos-santos/) · [WhatsApp](https://wa.me/5592991743165) · lemodosantos@gmail.com
