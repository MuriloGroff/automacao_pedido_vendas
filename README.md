![image](https://github.com/user-attachments/assets/71da29da-9411-4689-9f74-48ce46984ea7) Integração com a API do Bling para Gerenciamento de Vendas
Este repositório contém um script Python que integra a API do Bling para buscar e armazenar informações detalhadas de vendas em um banco de dados MySQL. O foco principal é a tabela vendas_detalhes, que organiza os dados de vendas de forma estruturada.

🛠️ Funcionalidades
Autenticação com a API do Bling:

Utiliza o fluxo OAuth 2.0 para autenticação.
Renova automaticamente o token de acesso quando necessário.
Busca de Vendas:

Realiza a busca de vendas em um intervalo de datas, com suporte à paginação.
Obtém informações detalhadas de cada venda, incluindo itens, taxas e transporte.
Armazenamento no Banco de Dados:

Insere ou atualiza os dados de vendas na tabela vendas_detalhes.
Garante que os dados sejam consistentes com a cláusula ON DUPLICATE KEY UPDATE.
Tratamento de Erros:

Lida com erros de requisição, como limite de requisições excedido (429) e token expirado (401).
Implementa tentativas automáticas para garantir a continuidade do processo.
🧩 Estrutura do Código
1️⃣ Autenticação
O script utiliza um arquivo JSON para armazenar os tokens de acesso e renovação. Caso o token expire, ele é renovado automaticamente.
def buscar_ids_vendas(pagina=1, limite=100):
    # Busca IDs de vendas com paginação
    ...

2️⃣ Busca de Vendas
A função buscar_ids_vendas realiza a busca de vendas em um intervalo de datas, com suporte à paginação.
def buscar_ids_vendas(pagina=1, limite=100):
    # Busca IDs de vendas com paginação
    ...
3️⃣ Detalhes de Vendas
A função buscar_detalhes_venda obtém informações detalhadas de uma venda específica, incluindo itens, taxas e transporte.
def buscar_detalhes_venda(id_venda):
    # Busca os detalhes de uma venda específica
    ...
4️⃣ Armazenamento no Banco de Dados
Os dados são armazenados na tabela vendas_detalhes com controle de duplicidade. A tabela inclui informações como número da venda, loja, itens, taxas e transporte.
cursor.execute('''
    INSERT INTO vendas_detalhes (
        numero, numeroLoja, data, situacao_desc, nome_loja, 
        item_codigo, item_unidade, item_quantidade, item_valor, 
        item_descricao, taxaComissao, custoFrete, valorBase, id, servico)
    VALUES (%s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s)
    ON DUPLICATE KEY UPDATE ...
''', (...))

🗂️ Estrutura da Tabela vendas_detalhes

![image](https://github.com/user-attachments/assets/22161dd7-62bf-42d5-b688-27ccdc7ec157)

Coluna	Tipo	Descrição
numero	VARCHAR	Número da venda
numeroLoja	VARCHAR	Número da loja
data	DATE	Data da venda
situacao_desc	VARCHAR	Situação da venda
nome_loja	VARCHAR	Nome da loja
item_codigo	VARCHAR	Código do item
item_unidade	VARCHAR	Unidade do item
item_quantidade	INT	Quantidade do item
item_valor	FLOAT	Valor total do item
item_descricao	VARCHAR	Descrição do item
taxaComissao	FLOAT	Taxa de comissão
custoFrete	FLOAT	Custo do frete
valorBase	FLOAT	Valor base da venda
id	BIGINT	ID da venda
servico	VARCHAR	Serviço de transporte


🔧 Tecnologias Utilizadas
Python: Linguagem principal para desenvolvimento do script.
MySQL: Banco de dados relacional para armazenamento das informações.
API do Bling: Fonte de dados para vendas e produtos.
Bibliotecas Python:
requests: Para realizar requisições HTTP.
mysql.connector: Para conexão e manipulação do banco de dados.
json: Para manipulação de dados JSON.
time: Para controle de tempo entre requisições.
🛡️ Tratamento de Erros
Erro 429 (Limite de Requisições):
O código aguarda 1 segundo antes de tentar novamente.
Erro 401 (Token Expirado):
O token é renovado automaticamente e a requisição é refeita.
Erros de Conexão:
São realizadas até 3 tentativas antes de abortar a operação.
📈 Resultados
Automação Completa:
Busca e armazenamento de dados de vendas de forma automatizada.
Escalabilidade:
Suporte à paginação para processar grandes volumes de dados.
Confiabilidade:
Tratamento de erros para garantir a continuidade do processo.
📌 Como Executar
Configurar o Banco de Dados:

Crie a tabela vendas_detalhes no MySQL.
Certifique-se de que as colunas estão configuradas corretamente.
Configurar Tokens de Acesso:

Salve os tokens de acesso e renovação no arquivo tokens.json.
Executar o Script:

Certifique-se de que todas as dependências estão instaladas.
Execute o script Python.
Verificar os Resultados:

Os dados serão armazenados na tabela vendas_detalhes.
🌟 Destaques
Integração com API RESTful: Demonstra como consumir APIs externas de forma eficiente.
Armazenamento Estruturado: Uso de MySQL para organizar e persistir os dados.
Automação e Escalabilidade: Processamento contínuo com suporte a grandes volumes de dados.
💡 Conclusão
Este projeto é um exemplo prático de como integrar APIs externas com bancos de dados para criar soluções automatizadas e escaláveis. Ele pode ser adaptado para diferentes cenários, como gestão de estoque, análise de vendas e muito mais.

Se você gostou deste projeto ou tem sugestões, deixe seu feedback! 🚀


  
