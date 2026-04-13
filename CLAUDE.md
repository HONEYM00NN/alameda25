# Alameda25 Store — Sistema de Gestão

## O que é este projeto
SPA (Single Page Application) de gestão para loja de moda masculina **Alameda25** (Fortaleza/CE).
Arquivo único: `index.html` — contém todo o HTML, CSS e JavaScript inline.

## Stack
- **Frontend:** HTML + CSS + JavaScript puro (sem frameworks)
- **Banco de dados:** Firebase Firestore (SDK compat v10.12.0 via CDN)
- **Hospedagem:** Netlify — https://alameda25.netlify.app/
- **Fontes:** Bebas Neue, Syne, JetBrains Mono
- **Paleta:** fundo `#080808`, dourado `#d4a84b` / `#f0c96a`

## Firebase (produção)
```js
const firebaseConfig = {
  apiKey: "AIzaSyAMcxHXIwkTS_Mos4v2CM9DVrhshN3w89Q",
  authDomain: "alameda25-669df.firebaseapp.com",
  projectId: "alameda25-669df",
  storageBucket: "alameda25-669df.firebasestorage.app",
  messagingSenderId: "36010699946",
  appId: "1:36010699946:web:b6d4b4ce7e24ebb14d74d3"
};
```
- **Collection:** `a25` / **Document:** `estado`
- Sincronização em tempo real via `onSnapshot` (fbListen)
- Fallback offline via localStorage

## Usuários
- `admin` / senha a definir → perfil Titular
- `socia` / senha a definir → perfil Sócia

## Funcionalidades implementadas
- Cadastro de produtos (nome, SKU, categoria, custo, preço varejo/atacado, estoque, alerta)
- Registro de vendas com carrinho (varejo/atacado, desconto, forma de pagamento, fiado)
- Controle de gastos (fixos e variáveis, categorias customizáveis)
- Reposições de estoque (gera gasto tipo "investimento" automaticamente)
- Cadastro de clientes
- Dashboard financeiro (receita, CMV, lucro, margem, ROI)
- Histórico/timeline de eventos com filtros (log[])
- Exportação CSV por seção
- Backup completo em JSON
- Sincronização Firebase em tempo real (indicador visual piscante)
- Sistema de alertas de estoque mínimo

## Lógica financeira
- CMV = custo ATUAL do produto × qtd vendida (não histórico)
- `gInv` = gastos tipo "investimento" no período
- `lucroLiq` = lucroOp - gInv - proLabore
- `ROI` = gInv > 0 ? lucroLiq / gInv * 100 : null

## Regras críticas de edição
- **SEMPRE** reler o trecho exato do arquivo antes de qualquer substituição
- **NUNCA** encadear substituições sem verificar o estado real intermediário
- Confirmar resultado com grep/python após cada fix
- Verificar JS com `node index.html` ou equivalente antes de salvar
- Cuidado com strings HTML dentro de funções JS (ex: `printRelatorio` contém `&lt;/style&gt;` dentro de template string)

## Melhorias pendentes (backlog)
1. Adicionar mais de 1 item na tela de troca
2. Busca de produto por texto (além de select)
3. Personalizar número de itens por página
4. Exclusão em massa com múltiplos cliques
5. Adicionar colunas configuráveis nas tabelas
6. Permitir registrar venda/produto com quantidade 0

## Deploy
- Netlify via drag-and-drop do `index.html` em: **Deploys → drag and drop**
- Os dados ficam no Firebase — o deploy só atualiza o código, nunca os dados

## Versão atual
v5.0 — Firebase integrado, histórico com timeline, sincronização em tempo real
