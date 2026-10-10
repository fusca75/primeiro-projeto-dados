# Dashboard de vendas

Dashboard educacional para a disciplina de Fundamentos de IA e Análise de Dados, feito apenas com HTML, CSS e JavaScript. A demonstração inicial tem 200 vendas fictícias em 12 meses e está incorporada em `public/script.js`, portanto funciona ao abrir o HTML diretamente.

## Como executar

1. Abra `public/index.html` no navegador. É necessário acesso à internet para carregar Chart.js 4.4.4 e Papa Parse 5.4.1 por CDN.
2. Use **Importar CSV** para selecionar uma base local. O arquivo não é enviado a servidor.
3. Combine período, categoria e região/canal; pesquise na tabela; use **Exportar CSV** para baixar o recorte.

## Dados e regras

`public/dados-exemplo.csv` é a base fictícia correspondente à demonstração. Colunas obrigatórias: `id_venda`, `data` (AAAA-MM-DD), `produto`, `categoria`, `regiao`, `quantidade` e `preco_unitario`. Também são aceitos arquivos com `canal` no lugar de `regiao`.

O arquivo original `vendas_hamburgueria.csv` foi preservado na raiz. Ele não possui `regiao`, mas possui `canal`; ao importá-lo, o painel adapta os rótulos para “Canal”. A coluna `avaliacao` possui ausências, mas não participa dos indicadores.

- Faturamento da linha = `quantidade × preco_unitario`.
- Faturamento total = soma do faturamento das linhas filtradas.
- Quantidade de vendas = quantidade de `id_venda` únicos.
- Unidades vendidas = soma de `quantidade`.
- Ticket médio = faturamento total ÷ quantidade de vendas; com zero vendas, o resultado é R$ 0,00.
- Planejamento diário = média geral de unidades por dia menos a média da combinação região/canal + produto. O cálculo usa os dias distintos com registros no recorte filtrado; resultados negativos são mostrados como zero, pois a combinação já alcança a média.

Linhas com ID, data, produto, categoria, região/canal, quantidade ou preço ausentes/inválidos são descartadas e contabilizadas após a importação. Valores iguais a zero são aceitos e não são tratados como ausentes. Não há remoção automática de duplicatas.

## Publicar no Render

Envie o projeto para um repositório no GitHub e crie um novo serviço **Static Site** no Render:

- Branch: a branch que contém o projeto.
- Root Directory: vazio.
- Build Command: `echo "Site pronto"`
- Publish Directory: `public`

O Render publicará `public/index.html` como página inicial. Como as bibliotecas vêm de CDN, o site publicado também precisa de internet para exibir os gráficos.
