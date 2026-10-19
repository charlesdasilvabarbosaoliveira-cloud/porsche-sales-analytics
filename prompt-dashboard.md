# Prompts e iterações — Porsche Sales Analytics

## 1. Especificação utilizada

> Atue como especialista em análise de dados, experiência do usuário e desenvolvimento front-end. Com base na planilha Porsche da DIO, construa um dashboard de vendas em português com **um único arquivo HTML**, contendo todos os dados, CSS e JavaScript, sem CDNs, bibliotecas externas ou backend. Use somente os campos sanitizados de data, modelo, ano do modelo, preço, quilometragem, método de pagamento, cidade, estado e situação da entrega. Converta preço e ano em números e preserve `INVALID` nas datas sem inventar valores. Não inclua nomes de clientes ou de vendedores no HTML público.
>
> Responda claramente a três questões: (1) Quais modelos geram maior valor bruto de negócios? (2) Quais estados concentram maior valor bruto? (3) Quais métodos de pagamento são mais utilizados? Apresente gráficos de barras ordenados e um gráfico de rosca, além de KPIs de negócios, valor bruto, ticket médio e entregas concluídas. Acrescente filtros de modelo, estado, ano da venda, pagamento e status, com atualização em tempo real. O design deve ser premium, inspirado em uma direção visual automotiva: grafite, branco quente, vermelho escuro, tipografia limpa e espaçamento editorial. Garanta funcionamento no celular e publicação direta no GitHub Pages.

## 2. Refinamentos adotados

1. **Tratamento do status:** excluir `Cancelled` dos indicadores por padrão, mas permitir visualizar cancelamentos ou todas as situações. Isso evita confundir valor registrado com receita reconhecida.
2. **Integridade temporal:** oferecer a opção `Data inválida` no filtro de ano e manter os registros de data inválida nos indicadores gerais, sem atribuir a eles um ano inventado.
3. **Moeda correta:** formatar todos os valores em `USD` e deixar explícito que a coluna representa valor de venda da planilha demonstrativa.
4. **Privacidade:** incorporar somente campos analíticos sanitizados, sem nome de cliente, nome de vendedor ou outros dados pessoais.
5. **Usabilidade:** permitir clicar em uma barra ou em um meio de pagamento para aplicar o filtro, redefinir os filtros, paginar e baixar o subconjunto em CSV.
6. **Independência técnica:** usar JavaScript nativo e CSS embutido para que a dashboard funcione mesmo sem acesso à internet.
7. **Verificação:** testar no Chromium os filtros, a paginação, as contagens e a exportação, além de registrar capturas da tela inicial e de um estado filtrado.
8. **Edição 02 — identidade visual:** após publicar a primeira versão, incorporar uma imagem ilustrativa Porsche ao cabeçalho, mantendo os dados, fórmulas, interatividade e visualização offline intactos. Embutir o arquivo WebP comprimido diretamente no HTML para não exigir upload de arquivos complementares. Registrar uma nova captura de tela em desktop e celular.

## 3. Ferramenta e contexto

O projeto foi produzido por interação com **ChatGPT**, com geração direta de código HTML, CSS e JavaScript, sem usar Canvas e sem criar um agente com skill. A especificação acima registra as decisões funcionais da implementação; o tratamento da planilha foi executado programaticamente e os testes foram feitos no navegador.

A decisão de não usar Canvas não impede a entrega pedida pelo desafio: `index.html` é o artefato final e funciona com GitHub Pages sem bibliotecas externas.
