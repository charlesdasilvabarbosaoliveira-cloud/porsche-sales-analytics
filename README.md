# Porsche Sales Analytics | Dashboard Interativo

**Projeto de análise de dados do desafio DIO — Criando Agentes de Tratamento de Dados.**

Dashboard de página única, inteiramente em **HTML + CSS + JavaScript**, com os dados incorporados no próprio `index.html`. Não exige Excel, instalação de pacotes, API, banco de dados nem servidor de aplicação. Executa no navegador e está pronto para hospedagem gratuita no GitHub Pages.

**Dashboard no GitHub Pages:** https://charlesdasilvabarbosaoliveira-cloud.github.io/porsche-sales-analytics/  
**Repositório:** https://github.com/charlesdasilvabarbosaoliveira-cloud/porsche-sales-analytics

> Após atualizar arquivos no GitHub, aguarde a nova implantação do GitHub Pages. A edição 02 inclui uma imagem ilustrativa dos veículos Porsche incorporada ao `index.html` (sem dependência de imagem externa).

## Dashboard — visão inicial, com imagem Porsche no cabeçalho

![Dashboard principal](assets/preview-dashboard.png)

### Exemplo: filtro por estado CA

![Dashboard com estado CA selecionado](assets/preview-filtro-california.png)

### Versão para celular

![Dashboard responsiva](assets/preview-mobile.png)

## Três perguntas de negócio

| Pergunta | Visualização | Por que importa? |
|---|---|---|
| **1. Quais modelos geram maior valor bruto em negociações?** | Barras horizontais: oito modelos líderes por valor registrado | Aponta concentração do mix, produtos de alto valor e oportunidades comerciais. |
| **2. Quais estados concentram maior valor bruto?** | Barras horizontais: oito estados líderes | Permite comparar mercados e direcionar a leitura de desempenho regional. |
| **3. Como os clientes pagam?** | Gráfico de rosca: participação dos métodos por quantidade | Evidencia preferências de pagamento e ajuda a orientar decisões sobre canais e meios oferecidos. |

Os três gráficos reagem aos filtros simultaneamente. As barras e a legenda dos pagamentos também funcionam como atalhos de filtragem.

## Principais indicadores

- **Negociações:** quantidade de linhas no recorte, excluindo status `Cancelled` por padrão.
- **Valor bruto registrado:** soma de `price_usd` das negociações incluídas no recorte. **Não é necessariamente faturamento, recebimento ou receita contábil reconhecida.**
- **Ticket médio:** valor bruto registrado dividido pela quantidade de negociações.
- **Entregas concluídas:** percentual dos registros com status sanitizado `Delivered`.

### Auditoria rápida do conjunto original

| Medida | Resultado |
|---|---:|
| Registros originais | 100 |
| Negociações não canceladas (padrão) | 93 |
| Registros com status `Cancelled` | 7 |
| Datas sanitizadas como `INVALID` | 24 |
| Datas válidas para seleção de ano | 76 |
| Valor bruto de **todos** os registros | US$ 12.827.800,50 |
| Valor bruto padrão, **sem canceladas** | US$ 12.202.550,50 |
| Modelos distintos | 40 |
| Estados distintos | 33 |
| Meios de pagamento distintos | 9 |

**Observação:** trata-se de uma **base didática/simulada**, incluindo datas de 2027; não é um relatório sobre vendas reais da Porsche. Os números podem incluir transações não entregues ou pendentes. A moeda original da base é USD, sem conversão cambial.

## Como a base foi tratada

1. A planilha XLSX original tem colunas cruas e colunas já sanitizadas. Foram escolhidos os campos `SaleDateSanitized`, `PorscheModelSanitized`, `ModelYearSanitized`, `SalesPriceSanitized`, `VehicleMileageSanitized`, `PayMethodSanitized`, `CitySanitized`, `StateSanitized` e `DeliveryStatusSanitized`, mais `sale_id` como identificador técnico.
2. Preços foram convertidos em **números decimais** e ano do modelo/quilometragem em **inteiros**. Os dados do HTML são valores fixos; não há fórmulas de Excel que possam quebrar.
3. Datas `INVALID` foram **preservadas** e contabilizadas. Elas só entram no filtro de ano quando a opção `Data inválida` é selecionada, porque não existe ano seguro para inferir.
4. Nomes de clientes, vendedores e as colunas cruas foram **descartados** do CSV público e do HTML, reduzindo exposição desnecessária.
5. `Cancelled` não é apagado. O status fica disponível no filtro, mas fora dos KPIs iniciais, com a opção explícita de exibir todas as situações.
6. O arquivo limpo está em [`data/vendas_porsche_sanitizadas.csv`](data/vendas_porsche_sanitizadas.csv), e os mesmos 100 registros analíticos estão embutidos no `index.html`.

**Campos publicados:** `sale_id`, `date`, `model`, `model_year`, `price_usd`, `mileage_miles`, `payment_method`, `city`, `state`, `delivery_status`.

## Funcionalidades

- Filtros por **modelo**, **estado**, **ano da venda** (inclusive datas inválidas), **método de pagamento** e **situação da venda**.
- Atualização imediata dos KPIs, gráficos, insights e tabela.
- Barras de modelos/estados e legenda de pagamentos clicáveis para aplicar filtros.
- Botão para limpar filtros e restaurar o comportamento inicial.
- Indicadores formatados em **US$** e percentuais em padrão brasileiro.
- Tabela de microdados com **paginação** e sem nomes pessoais.
- **Exportação CSV** apenas do recorte selecionado.
- Layout responsivo para computador e celular, com navegação por teclado e estados vazios tratados.
- Fotografia automotiva **ilustrativa, gerada por IA**, incorporada ao HTML, sem carregar imagens externas ou alterar os indicadores.
- Execução offline de `index.html`; nenhuma dependência externa.

## Processo com IA: prompt e refinamentos

Ferramenta utilizada: **ChatGPT para criação direta do HTML/CSS/JavaScript**, sem Canvas e sem agente especializado. O trabalho incluiu revisão da base, especificação de perguntas, tratamento de casos inválidos, validação de indicadores e testes reais do arquivo no navegador.

O prompt-base documentado e as mudanças aplicadas até a versão final estão em **[`prompts/prompt-dashboard.md`](prompts/prompt-dashboard.md)**. Os refinamentos mais importantes foram remover vendas canceladas da visão padrão, não adivinhar datas inválidas e usar o valor bruto na moeda correta.

## Estrutura

```text
porsche-sales-analytics/
├── index.html                         # dashboard completa, arquivo único
├── README.md                          # documentação do desafio
├── .nojekyll                          # publicação estática via GitHub Pages
├── assets/
│   ├── preview-dashboard.png          # evidência visual inicial
│   ├── preview-filtro-california.png  # evidência com filtro aplicado
│   └── preview-mobile.png             # evidência de responsividade
├── data/
│   └── vendas_porsche_sanitizadas.csv # dados analíticos públicos
└── prompts/
    └── prompt-dashboard.md            # prompt e evolução das instruções
```

## Como executar

**Localmente:** abra o arquivo `index.html` no navegador. Como os dados estão dentro do HTML, não é necessário um servidor HTTP para carregar arquivos auxiliares.

**Publicar gratuitamente no GitHub Pages:**

1. Crie um repositório público chamado `porsche-sales-analytics` na sua conta do GitHub.
2. Envie `index.html`, `README.md`, `.nojekyll` e as pastas `assets/`, `data/` e `prompts/` na raiz do repositório, preservando a estrutura.
3. Em **Settings → Pages**, na seção **Build and deployment**, escolha **Deploy from a branch**.
4. Selecione a branch principal do repositório (neste projeto, **principal**), a pasta **/(root)** e clique em **Save**.
5. Aguarde a implantação e clique em **Visit site** quando o GitHub informar que a página está publicada.
6. Teste um filtro na página pública e confira os gráficos. O link enviado à DIO deverá ser o **repositório**, e o link da dashboard deverá constar neste README.

Documentação oficial: <https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site>.

## Evidências e testes de funcionamento

Na edição 02, a fotografia incorporada foi testada nas versões para desktop e celular, sem alterar a aplicação dos filtros. Os testes no Chromium verificaram: dashboard inicial com **93 negociações ativas**, os três gráficos preenchidos, filtro `CA` com **16 registros**, opção de ano `Data inválida`, botão de redefinição, status `Todos` com **100 registros**, status `Cancelled` com **7**, ausência de erros JavaScript, responsividade em dispositivo móvel e exportação CSV.

## Créditos

- Base educacional: **DIO — desafio Porsche**, com base disponibilizada no material do curso.
- Desenvolvimento e apoio à análise: ChatGPT, revisão das regras de negócio e testes de navegador.
- Projeto didático **não afiliado à Porsche AG**.
