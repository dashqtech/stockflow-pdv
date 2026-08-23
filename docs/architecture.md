# Arquitetura

## Visão geral

O StockFlow é um aplicativo Windows feito com Electron e Next.js. Escolhi essa combinação porque já estava usando React na interface e precisava entregar um programa instalável para a loja.

O Supabase cuida da autenticação e do PostgreSQL. Assim, os dados continuam centralizados mesmo com o aplicativo rodando no computador da loja.

## Camadas do projeto

| Camada | Responsabilidade |
|---|---|
| Interface | Mostra as telas, formulários, tabelas e estados visuais. |
| Aplicação | Valida a sessão e organiza as regras de cada módulo. |
| Banco | Confere permissões e grava vendas, estoque e pagamentos. |
| Desktop | Abre a janela do programa e empacota a aplicação para Windows. |

Não coloquei nomes de tabelas, funções, endpoints ou configurações operacionais nesta versão pública da documentação.

## Caminho de uma operação

1. O usuário preenche ou confirma uma ação na interface.
2. A aplicação verifica a sessão e o tipo de usuário.
3. Os dados passam por validação antes de chegar ao banco.
4. O banco aplica as regras da operação.
5. A interface recebe o resultado e atualiza a tela.

Vendas e movimentações de estoque podem alterar vários registros. Por isso, o banco conclui essas etapas na mesma transação. Se alguma validação falhar, a operação inteira é cancelada.

## Aplicativo desktop

O Electron roda com isolamento entre a interface e o processo principal. A janela não recebe acesso direto às APIs do Node.js, e o aplicativo restringe permissões, navegação e abertura de links externos.

As chaves com privilégio administrativo não fazem parte do instalador. A comunicação com o banco usa uma sessão autenticada e respeita o papel de cada usuário.

## Banco e permissões

O sistema tem dois papéis:

- operador de caixa, voltado para vendas e consultas do dia a dia;
- administrador, usado para configurações e operações de gestão.

As permissões são conferidas fora da interface. O banco também usa políticas por linha, constraints e transações para proteger os dados.

## Interface

Criei uma base compartilhada para modais, botões, avisos e campos. Isso facilitou manter foco, teclado, rolagem e mensagens de erro com o mesmo comportamento em telas diferentes.

O sistema tem tema escuro e claro. As animações são curtas e respeitam a preferência de movimento reduzido do usuário.

## Limites da versão atual

- O instalador do MVP não possui certificado Authenticode.
- A chave fiscal da NF-e é opcional por uma decisão do produto.
- A recuperação de senha depende do serviço de e-mail configurado.
- O aplicativo foi pensado para uso interno em uma loja, não para distribuição pública em grande escala.
