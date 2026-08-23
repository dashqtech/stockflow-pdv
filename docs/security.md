# Decisão de segurança

## Por que o código não está aqui

O StockFlow será usado internamente por uma loja. Publicar o código completo mostraria migrations, regras de autorização, fluxos administrativos e detalhes do banco que não são necessários para avaliar o projeto no portfólio.

Um sistema seguro não pode depender de esconder o código. Mesmo assim, expor detalhes operacionais sem uma necessidade real facilita o trabalho de reconhecimento de terceiros. Por esse motivo, separei a apresentação pública do repositório usado no aplicativo.

## O que ficou público

- screenshots sem dados pessoais;
- identidade visual;
- tecnologias usadas;
- números do projeto e dos testes;
- arquitetura e fluxos em alto nível;
- decisões de interface e qualidade.

## O que continua privado

- código-fonte e histórico Git;
- migrations e políticas do banco;
- configurações do Supabase;
- endpoints, funções e nomes internos;
- instaladores e arquivos de atualização;
- relatórios completos de segurança;
- dados da loja e credenciais.

Essa separação permite mostrar o projeto sem transformar o repositório de portfólio em uma cópia do ambiente operacional.
