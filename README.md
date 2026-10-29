# 🏗️ ObraJá (iFood da Construção Civil)
> **O marketplace inteligente que conecta engenheiros, mestres de obras, pedreiros e consumidores finais aos depósitos e lojas de materiais de construção.**

[![CI - Backend Tests & TDD](https://github.com/Obra-ja/backend/actions/workflows/ci.yml/badge.svg)](https://github.com/Obra-ja/backend/actions)
[![CI - Web Tests & TDD](https://github.com/Obra-ja/web/actions/workflows/ci.yml/badge.svg)](https://github.com/Obra-ja/web/actions)
[![CI - Mobile Tests & TDD](https://github.com/Obra-ja/mobile/actions/workflows/ci.yml/badge.svg)](https://github.com/Obra-ja/mobile/actions)
[![Metodologia](https://img.shields.io/badge/Metodologia-TDD%20(Test--Driven%20Development)-green.svg)](https://github.com/Obra-ja/backend/blob/main/AGENTS.md)
[![Arquitetura](https://img.shields.io/badge/Arquitetura-Clean%20Architecture%20%7C%20DDD-blue.svg)](https://github.com/Obra-ja/backend/blob/main/docs/ARCHITECTURE.md)
[![Licença](https://img.shields.io/badge/Licen%C3%A7a-MIT-yellow.svg)](LICENSE)

---

## 📌 Índice
1. [Visão Geral do Produto](#-visão-geral-do-produto)
2. [Principais Desafios de Negócio & Soluções](#-principais-desafios-de-negócio--soluções)
3. [Personas Atendidas](#-personas-atendidas)
4. [Modelo de Monetização](#-modelo-de-monetização)
5. [Recomendação de Linguagens e Tecnologias](#-recomendação-de-linguagens-e-tecnologias)
6. [Fluxo de Branches & Contribuição (Git Flow)](#-fluxo-de-branches--contribuição-git-flow)
7. [Metodologia TDD (Test-Driven Development)](#-metodologia-tdd)
8. [Instruções para Agentes de IA](#-instruções-para-agentes-de-ia-agentsmd)
9. [Ecossistema de Repositórios](#-ecossistema-de-repositórios)
10. [Como Executar o Projeto & Testes](#-como-executar-o-projeto--testes)
11. [Roadmap de Desenvolvimento](#-roadmap-de-desenvolvimento)
12. [Equipe & Contribuição](#-equipe--contribuição)

---

## 🎯 Visão Geral do Produto

Na construção civil e reformas, a compra de materiais é historicamente fragmentada, analógica e desgastante. O profissional da obra ou o proprietário perde horas ligando para depósitos de bairro, enviando listas manuais pelo WhatsApp e negociando fretes e prazos de entrega.

O **ObraJá** surge como o **"iFood da Construção Civil"**:
- **Catálogo Unificado**: Lojas da mesma região anunciam seus produtos lado a lado, gerando transparência de preços e disponibilidade.
- **Carrinho Multi-Loja (Split de Pedido)**: O cliente pode comprar **areia e pedra** no depósito mais próximo (menor frete pesado) e **fios, tomadas e tintas** em uma grande loja de acabamento, pagando tudo em uma única transação.
- **Módulo Duplo: Compra Direta ou Orçamento (RFQ)**:
  - *Compra Imediata*: Adiciona ao carrinho e finaliza via Pix/Cartão.
  - *Cotação/Orçamento*: O cliente envia uma lista de materiais (ex: "Lista do Engenheiro") e as lojas locais disputam o fornecimento enviando suas melhores propostas em tempo real.

---

## 💡 Principais Desafios de Negócio & Soluções

| Desafio da Construção Civil | Como o ObraJá Resolve |
| :--- | :--- |
| **Logística Heterogênea** (Areia vs. Fiação) | Separação automática de classes de frete: frete pesado (caminhão basculante/por km) vs. frete leve (moto/furgão). |
| **Carrinho com Múltiplas Lojas** | Motor de *Order Splitting*: a transação gera sub-pedidos com status de separação independentes para cada lojista. |
| **Split de Pagamentos & Repasses** | Integração com gateways que realizam divisão automática de recebíveis (split payment) no ato da compra. |
| **Orçamentos Complexos** | Sistema de *Request For Quote (RFQ)* com upload de PDF/foto da lista da obra e resposta estruturada das lojas. |

---

## 👥 Personas Atendidas

1. **Engenheiro / Mestre de Obras**: Necessita de pontualidade na entrega para não parar a equipe na obra, emissão rápida de notas fiscais e cotação rápida para listas grandes.
2. **Pedreiro / Reformador Autônomo**: Precisa de reposição de emergência (ex: "acabou o cimento às 14h") via smartphone com entrega rápida.
3. **Consumidor Residencial (Dono da Casa)**: Quer transparência de preços, facilidade de pagamento parcelado e garantia de entrega.
4. **Lojistas de Materiais de Construção (Parceiros)**: Pequenos e médios depósitos que ganham canal digital de vendas sem custos fixos iniciais.
5. **Administrador do ObraJá**: Gestão de taxas, conciliação financeira, moderação de lojas e relatórios de comissões.

---

## 💰 Modelo de Monetização

O modelo de negócio foi desenhado para facilitar a adesão dos lojistas e garantir a sustentabilidade da plataforma:

1. **Take-Rate Progressivo (Comissão por Vendas com Limiar)**:
   - **Faixa de Atração / Carência**: 0% de comissão até que a loja atinja um volume de vendas inicial acumulado (ex: primeiros R$ 3.000,00 ou 30 primeiros dias).
   - **Faixa Padrão**: Após ultrapassar a quantia estipulada, a plataforma retém uma comissão percentual (ex: entre **5% a 10%** sobre o valor dos produtos, diferenciada por categoria de margem).
2. **Taxa de Conveniência do Comprador**: Pequena taxa fixa por pedido para cobrir custos de gateway e suporte.
3. **Destaque Patrocinado**: Lojas podem pagar para posicionar produtos no topo das buscas da sua região.

> Veja o detalhamento financeiro completo em [docs/BUSINESS_MODEL.md](https://github.com/Obra-ja/backend/blob/main/docs/BUSINESS_MODEL.md).

---

## 🛠️ Recomendação de Linguagens e Tecnologias

Para uma equipe de **3 pessoas (você, seu amigo e o professor)** com foco em **TDD rigoroso**, a melhor escolha estratégica é priorizar uma stack moderna, fortemente tipada e com alta produtividade:

### 🌟 Recomendação Principal: **Ecossistema TypeScript Fullstack**

```
┌────────────────────────────────────────────────────────┐
│                   APLICAÇÕES CLIENTES                  │
│   Web (Next.js 15)            App Mobile (React Native)│
│   (Painel Loja & Admin)       (Engenheiros & Obras)    │
└───────────────────────────┬────────────────────────────┘
                            │ REST / GraphQL
┌───────────────────────────▼────────────────────────────┐
│                    BACKEND CORE API                    │
│   Node.js / Deno + TypeScript + Clean Architecture     │
│   Testes: Vitest (TDD ultrarrápido com Red-Green)      │
└─────────────┬───────────────────────────┬──────────────┘
              │                           │
┌─────────────▼──────────────┐ ┌──────────▼──────────────┐
│       POSTGRESQL + POSTGIS │ │      REDIS + BULLMQ     │
│  - Transações ACID (Split) │ │  - Sessões de Carrinho  │
│  - Geolocalização de Lojas │ │  - Filas de Orçamentos  │
└────────────────────────────┘ └─────────────────────────┘
```

### Por que essa escolha?
1. **Mesma Linguagem em Tudo**: Não há sobrecarga de trocar de sintaxe entre Mobile, Web e Backend. Os três membros do time conseguem atuar em qualquer parte do código.
2. **TDD Impecável**: Ferramentas como **Vitest** ou **Deno Test** executam testes em milissegundos com tipagem estática do TypeScript, tornando o ciclo *Red-Green-Refactor* prazeroso e instantâneo.
3. **PostgreSQL com PostGIS**: Essencial para a construção civil, pois calcula a distância exata em quilômetros entre o depósito de areia e o endereço da obra.
4. **Split de Pagamento Nacional**: Excelente suporte em TypeScript/Node para os principais gateways brasileiros com split nativo (**Asaas**, **Pagar.me** ou **Mercado Pago**).

> Confira a comparação detalhada com Go, Python e Java/C# em [docs/TECH_STACK.md](https://github.com/Obra-ja/backend/blob/main/docs/TECH_STACK.md).

---

## 🔀 Fluxo de Branches & Contribuição (Git Flow)

Para garantir a estabilidade do marketplace e a integridade dos testes, adotamos o seguinte fluxo obrigatório:

```
(main) ─────────────────────────────────────────────────────────────● (Releases Estáveis)
                                                                   ▲
(dev)  ──────●─────────────────────────────────────●───────────────┘ (Ambiente de Integração)
              \                                   ▲ (Pull Request com CI verde)
(feat)         └───[TDD: Red -> Green -> Refactor]┘ (Nova Feature / Bugfix)
```

> [!IMPORTANT]
> **REGRA INEGOCIÁVEL**: **Nunca comite diretamente nas branches `main` ou `dev`.**  
> Sempre que for desenvolver uma nova funcionalidade (`feat`), correção (`fix`) ou refatoração:
> 1. Atualize sua branch local: `git checkout dev && git pull origin dev`
> 2. Crie uma branch específica: `git checkout -b feat/nome-da-sua-feature`
> 3. Desenvolva orientado a testes (**TDD**) garantindo 100% de cobertura.
> 4. Suba a branch e abra um **Pull Request (PR) com destino à branch `dev`**.
> 5. O PR só será mesclado em `dev` após aprovação da equipe e validação dos testes automáticos no CI.

---

## 🧪 Metodologia TDD

Neste projeto, **nenhuma regra de negócio é escrita antes do seu teste unitário correspondente falhar**:

```
 🔴 RED          Escreva um teste que expressa o comportamento esperado e veja-o FALHAR.
    │
    ▼
 🟢 GREEN        Escreva a implementação mais simples possível para fazer o teste PASSAR.
    │
    ▼
 🔵 REFACTOR     Limpe o código, elimine duplicações e melhore a arquitetura mantendo os testes VERDES.
```

### O que testamos via TDD:
- ✅ Divisão de carrinho em múltiplos sub-pedidos por loja (*Order Splitting*).
- ✅ Cálculo de comissões com limiares de isenção e taxas progressivas.
- ✅ Separação e cálculo de frete por classe de material (pesado vs. leve).
- ✅ Transição de estados dos pedidos e propostas de orçamento.

> Leia o guia prático completo em [docs/TDD_GUIDELINES.md](https://github.com/Obra-ja/backend/blob/main/docs/TDD_GUIDELINES.md).

---

## 🤖 Instruções para Agentes de IA (`AGENTS.md`)

Este repositório inclui o arquivo [AGENTS.md](https://github.com/Obra-ja/backend/blob/main/AGENTS.md), que padroniza como qualquer assistente ou agente de inteligência artificial (Antigravity, Claude Code, Cursor, Copilot) deve interagir com o código:
- Proibição estrita de criar código de domínio sem teste prévio.
- Manutenção da integridade da Arquitetura Limpa (Clean Architecture).
- Nomenclatura ubíqua em português para termos da construção civil e inglês para padrões técnicos.

---

## 📂 Ecossistema de Repositórios

O projeto está dividido nos 3 repositórios oficiais da organização:

| Repositório | Descrição | Stack | Status do CI |
| :--- | :--- | :--- | :--- |
| ⚙️ **[Obra-ja/backend](https://github.com/Obra-ja/backend)** | API REST, Regras de Domínio (DDD), Split de Pedidos e Comissões | Node/Deno + TypeScript + PostgreSQL + PostGIS | [![CI](https://github.com/Obra-ja/backend/actions/workflows/ci.yml/badge.svg)](https://github.com/Obra-ja/backend/actions) |
| 💻 **[Obra-ja/web](https://github.com/Obra-ja/web)** | Portal Web dos Lojistas e Painel Administrativo Master | Next.js 15 + React + Tailwind CSS | [![CI](https://github.com/Obra-ja/web/actions/workflows/ci.yml/badge.svg)](https://github.com/Obra-ja/web/actions) |
| 📱 **[Obra-ja/mobile](https://github.com/Obra-ja/mobile)** | Aplicativo para Engenheiros, Mestres de Obras e Reformadores | React Native + Expo + TypeScript | [![CI](https://github.com/Obra-ja/mobile/actions/workflows/ci.yml/badge.svg)](https://github.com/Obra-ja/mobile/actions) |

---

## 🚀 Como Executar o Projeto & Testes

### 1. Backend (API & Regras de Domínio)
```bash
git clone https://github.com/Obra-ja/backend.git
cd backend
git checkout dev

# Subir banco de dados PostgreSQL com PostGIS e Redis:
deno task docker:up

# Rodar a suíte completa de testes TDD:
deno test
```

### 2. Portal Web (Lojistas & Admin)
```bash
git clone https://github.com/Obra-ja/web.git
cd web
git checkout dev

deno test
# ou: npm install && npm run dev
```

### 3. App Mobile (Obras & Clientes)
```bash
git clone https://github.com/Obra-ja/mobile.git
cd mobile
git checkout dev

deno test
# ou: npm install && npx expo start
```

---

## 🗺️ Roadmap de Desenvolvimento

- [x] **Fase 0: Fundação & Arquitetura**
  - [x] Definição de domínio e regras de negócio.
  - [x] Criação da organização `Obra-ja`, repositórios e TDD setup.
  - [x] Implementação TDD do *Order Splitting* e *Cálculo de Comissões*.
- [ ] **Fase 1: MVP do Backend (API)**
  - [ ] Cadastro e autenticação de Lojistas e Clientes.
  - [ ] Catálogo de produtos com geolocalização.
  - [ ] Módulo de Carrinho Multi-Loja e checkout com split de pagamento (Pagar.me / Asaas).
  - [ ] Módulo de Solicitação de Orçamento (RFQ).
- [ ] **Fase 2: Painel Web do Lojista (Next.js)**
  - [ ] Gestão de estoque e catálogo da loja.
  - [ ] Recepção e despacho de sub-pedidos.
  - [ ] Painel para responder orçamentos recebidos.
- [ ] **Fase 3: App Mobile do Usuário (React Native / Expo)**
  - [ ] Navegação de lojas próximas por CEP/GPS.
  - [ ] Carrinho unificado e rastreamento de entregas.
  - [ ] Envio de fotos de listas de materiais para cotação.

---

## 👨‍💻 Equipe & Contribuição

Este projeto está sendo desenvolvido em colaboração acadêmica e profissional:
- **Fundadores**: Desenvolvedores e Engenheiros do projeto.
- **Orientador / Professor**: Apoio acadêmico, arquitetural e validação de engenharia de software.

Para contribuir, siga estritamente o fluxo TDD e as convenções em [AGENTS.md](https://github.com/Obra-ja/backend/blob/main/AGENTS.md).
