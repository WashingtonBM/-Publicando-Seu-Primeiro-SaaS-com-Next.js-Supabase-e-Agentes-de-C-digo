# Agente de Propostas de Valor | WBM ANÁLISES

Agente de IA que gera **propostas de valor** para empreendedores individuais (MEI, autônomos, freelancers) e pequenas e médias empresas. O usuário preenche um briefing curto e recebe um diagnóstico, um canvas, três versões da proposta, objeções com respostas, um teste A/B e recomendações de serviços.

Projeto da **WBM ANÁLISES**, uma startup enxuta operada por agentes de IA e um fundador, focada em tecnologia, dados e crescimento de pequenos negócios.

> **Status:** protótipo funcional (v0.1). A versão em Next.js + Supabase está planejada e ainda não foi implementada. Veja o [Roadmap](#roadmap).

---

## Sumário

- [O que o agente faz](#o-que-o-agente-faz)
- [Estado atual do projeto](#estado-atual-do-projeto)
- [Como usar o protótipo](#como-usar-o-protótipo)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Como o agente funciona](#como-o-agente-funciona)
- [Roadmap](#roadmap)
- [Arquitetura planejada (v1.0)](#arquitetura-planejada-v10)
- [Segurança e privacidade](#segurança-e-privacidade)
- [Limitações conhecidas](#limitações-conhecidas)
- [Contribuindo](#contribuindo)
- [Licença](#licença)
- [Contato](#contato)

---

## O que o agente faz

A partir de um briefing, o agente entrega, nesta ordem:

1. **Resumo do diagnóstico:** cliente ideal, dor principal, alternativa atual e diferencial real.
2. **Canvas resumido:** tarefas do cliente, dores, ganhos, aliviadores e criadores de ganho (Value Proposition Canvas).
3. **Proposta de valor em 3 versões:** frase principal (até 20 palavras), versão curta para bio ou slogan, e versão longa para site (título, subtítulo e 3 benefícios).
4. **Diferenciais e provas:** o que é verificável, o que falta comprovar e como obter.
5. **Objeções prováveis e respostas.**
6. **Teste rápido:** duas variações da frase principal para teste A/B e a métrica a observar.
7. **Como a WBM pode ajudar:** de 1 a 3 serviços do catálogo ligados a lacunas encontradas no diagnóstico.

### Princípios do agente

- **Não inventa provas.** Onde faltam números, depoimentos ou resultados, escreve `[INSERIR PROVA]` e orienta como obtê-los.
- **Específico vence genérico.** Prioriza um segmento, uma dor e uma promessa central.
- **Sem promessa de resultado financeiro** e sem clichês não comprovados.
- **Linguagem simples**, em português do Brasil, para donos de negócio sem formação em marketing.
- **Sem aconselhamento jurídico, contábil ou tributário.**

### Campos do briefing

| Campo | Obrigatório |
|---|---|
| Nome do negócio e segmento | Não |
| O que vende | **Sim** |
| Cliente ideal | **Sim** |
| Maior dor do cliente | Não |
| Como o cliente resolve hoje (concorrentes e alternativas) | Não |
| Diferencial | Não |
| Provas (números, depoimentos, cases) | Não |
| Ticket médio | Não |
| Canal principal de venda | Não |
| Objetivo | Não |

Quando faltam informações, o agente faz suposições e as lista no início da resposta.

---

## Estado atual do projeto

| Item | Situação |
|---|---|
| Formulário de briefing | Pronto |
| Geração da proposta com IA (resposta em tempo real) | Pronto |
| Copiar resultado e baixar em Markdown | Pronto |
| Histórico das últimas 15 propostas | Pronto (apenas no navegador do usuário) |
| Login e histórico por usuário | Planejado |
| Exportação em PDF | Planejado |
| Cobrança (Pix ou Stripe) | Planejado |
| Entrada do briefing por WhatsApp ou e-mail | Planejado |
| Versões por segmento (alimentação, beleza, serviços) | Planejado |

---

## Como usar o protótipo

O protótipo é **uma única página HTML** (`agente-proposta-valor.html`) publicada como Artifact no claude.ai.

1. Abra o link do Artifact, logado na sua conta do claude.ai.
2. Preencha o briefing. Ao menos **O que vende** e **Cliente ideal**.
3. Clique em **Gerar proposta de valor**.
4. Revise os trechos marcados com `[INSERIR PROVA]` antes de usar o texto.
5. Use **Copiar** ou **Baixar (.md)**.

**Link do protótipo:** https://claude.ai/artifact/Ke8eKAq8XEn1QdLVBKKa4W

> **Importante:** a geração com IA depende do ambiente de execução do claude.ai. Abrir o arquivo `.html` diretamente no navegador, fora do claude.ai, exibe o formulário, mas **não gera propostas**. Para uso independente, é preciso a versão Next.js descrita abaixo.

---

## Estrutura do repositório

```
.
├── README.md                      # este arquivo
├── agente-proposta-valor.html     # protótipo (página única)
└── docs/                          # (sugerido) system prompt, exemplos e notas
```

O system prompt do agente está na constante `SYS`, dentro do arquivo HTML. Quando o projeto migrar para Next.js, ele deve ir para um arquivo próprio (por exemplo `src/lib/prompts/proposta-valor.ts`), versionado separadamente.

---

## Como o agente funciona

1. O formulário reúne os campos do briefing.
2. O sistema monta um prompt com o system prompt da WBM e as respostas do usuário. Campos vazios entram como "(não informado)", o que aciona o comportamento de listar suposições.
3. O modelo gera a resposta em Markdown, no formato de 7 seções.
4. A página converte o Markdown em HTML (títulos, listas, citações e tabelas) e mostra o texto conforme é escrito.
5. O resultado é salvo no histórico local do navegador.

**Método:** Value Proposition Canvas e Jobs To Be Done.

**Catálogo de serviços da WBM** usado na recomendação final:

- Criação e desenvolvimento de sites e blogs
- Produtos digitais em geral
- Automações e agentes de IA
- Painéis de visualização de dados, análises e relatórios
- Gestão empresarial e financeira
- Marketing e assessoria em desenvolvimento empresarial
- Melhoria, suporte e assessoria contínua

---

## Roadmap

### Etapa 1: validação
- [ ] Testar com 3 a 5 negócios reais, incluindo a própria WBM
- [ ] Registrar erros e respostas genéricas e ajustar o system prompt
- [ ] Usar as propostas geradas como porta de entrada para obter depoimentos e cases

### Etapa 2: produto próprio (Next.js + Supabase)
- [ ] Projeto Next.js (App Router, TypeScript, Tailwind)
- [ ] Chamada à API da Anthropic em rota de servidor
- [ ] Autenticação com Supabase (e-mail e senha ou magic link)
- [ ] Tabela `proposals` com Row Level Security
- [ ] Migrações versionadas com Supabase CLI
- [ ] Validação de entrada com Zod
- [ ] Limite de uso por usuário
- [ ] Exportação em PDF
- [ ] Deploy na Vercel

### Etapa 3: escala
- [ ] Cobrança por proposta ou assinatura (Pix ou Stripe)
- [ ] Entrada do briefing por WhatsApp e e-mail
- [ ] Versões do agente por segmento
- [ ] Painel de métricas de uso

---

## Arquitetura planejada (v1.0)

| Camada | Tecnologia | Papel |
|---|---|---|
| Frontend e backend | Next.js (App Router) | Interface, Server Actions e rotas de API |
| Banco e autenticação | Supabase (Postgres, Auth, RLS) | Usuários e histórico de propostas |
| IA | API da Anthropic, chamada no servidor | Geração da proposta |
| Deploy | Vercel | Hospedagem com integração ao GitHub |
| Pagamentos | Stripe ou Pix | Cobrança |
| E-mails | Resend (sugestão) | Mensagens transacionais |
| Monitoramento | Sentry (sugestão) | Erros em produção |

### Variáveis de ambiente previstas

```bash
# .env.local (nunca versionar)
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=      # somente servidor
ANTHROPIC_API_KEY=              # somente servidor
```

### Modelo de dados inicial (proposta)

```sql
create table proposals (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  business_name text,
  briefing jsonb not null,
  result_markdown text not null,
  created_at timestamptz default now()
);

alter table proposals enable row level security;

create policy "dono acessa suas propostas"
on proposals for all
using (auth.uid() = user_id)
with check (auth.uid() = user_id);
```

---

## Segurança e privacidade

- **Chaves secretas** (`ANTHROPIC_API_KEY`, `SUPABASE_SERVICE_ROLE_KEY`) nunca vão para o cliente nem para o repositório. Mantenha `.env*` no `.gitignore`.
- **RLS ativo em todas as tabelas**, com políticas testadas. Tabela sem RLS é tabela pública.
- **Validação de entrada no servidor** antes de chamar o modelo.
- **LGPD:** o briefing pode conter dados de negócios e de pessoas. Antes de abrir ao público, publique política de privacidade e termos de uso, informe quais dados são guardados e por quanto tempo, e ofereça exclusão do histórico.
- No protótipo atual, o histórico fica apenas no navegador de quem usa e não é enviado a nenhum banco da WBM.

---

## Limitações conhecidas

- O protótipo só gera propostas dentro do claude.ai e exige que o usuário esteja logado.
- O histórico é local e se perde ao limpar os dados do navegador.
- A qualidade da proposta depende da qualidade do briefing. Briefings vagos produzem propostas genéricas, e o agente deve avisar isso.
- O agente **não substitui** validação com clientes reais. Use o teste A/B e as conversas com donos de negócio para confirmar o que funciona.
- Não há exportação em PDF nem cobrança nesta versão.

---

## Contribuindo

Sugestões e correções são bem-vindas.

1. Abra uma *issue* descrevendo o problema ou a ideia.
2. Para mudanças de código, crie um *fork*, uma branch (`feat/nome-da-mudanca`) e abra um *pull request* com commits pequenos.
3. Mudanças no system prompt devem vir acompanhadas de exemplos de briefing antes e depois.

---

## Licença

Defina a licença antes de abrir o repositório ao público (por exemplo MIT, ou "todos os direitos reservados" se o código for proprietário). Adicione o arquivo `LICENSE` na raiz.

---

## Contato

**WBM ANÁLISES**
Washington B. M. · GitHub: [@WashingtonBM](https://github.com/WashingtonBM)
