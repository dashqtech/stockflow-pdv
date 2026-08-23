# StockFlow

![Logotipo do StockFlow](assets/stockflow-logo.png)

![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=next.js&logoColor=white)
![React](https://img.shields.io/badge/React-19-149ECA?logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL%2017-3ECF8E?logo=supabase&logoColor=white)
![Electron](https://img.shields.io/badge/Electron-43-47848F?logo=electron&logoColor=white)

O StockFlow é um sistema desktop que desenvolvi para organizar a operação de uma pequena loja. Ele reúne frente de caixa, produtos, estoque, clientes, fiado, trocas, inventário e entrada de NF-e no mesmo aplicativo Windows.

Este repositório serve apenas para apresentar o projeto no meu portfólio. O código-fonte, o instalador, as configurações do banco e os dados da loja ficam em um repositório privado. As imagens desta página usam campos vazios ou textos de exemplo.

## O que o sistema faz

- abre e fecha o caixa de cada dia;
- registra vendas com mais de uma forma de pagamento, desconto e troco;
- controla produtos vendidos por unidade ou de forma fracionada;
- importa produtos e custos a partir de XML de NF-e;
- calcula margem de lucro e permite alterar a meta em lote;
- registra clientes, compras, fiado e pagamentos;
- acompanha trocas, devoluções, inventário e movimentações de estoque;
- separa o acesso do administrador e do operador de caixa;
- gera instalador e versão portátil para Windows.

## Tecnologias que usei

| Parte | Tecnologia |
|---|---|
| Aplicativo desktop | Electron 43 |
| Interface | Next.js 16, React 19 e TypeScript 5 |
| Banco e autenticação | Supabase e PostgreSQL 17 |
| Validação | Zod |
| Estado local | Zustand |
| Animações | Framer Motion |
| Gráficos | Recharts |
| Testes | Vitest, Testing Library e Playwright |
| Empacotamento | electron-builder |

## Como organizei a arquitetura

```mermaid
flowchart LR
    U[Usuário no Windows] --> E[Aplicativo Electron]
    E --> N[Interface Next.js]
    N --> A[Autenticação]
    N --> D[Banco PostgreSQL]
    N --> S[Armazenamento de arquivos]

    subgraph Supabase
        A
        D
        S
    end
```

O Electron abre a aplicação em uma janela desktop, enquanto o Next.js monta as telas e trata as ações do usuário. O Supabase fica responsável pelas contas, permissões e dados. As operações que alteram venda ou estoque são concluídas em transações para evitar registros pela metade.

Deixei uma explicação mais completa em [docs/architecture.md](docs/architecture.md) e outros desenhos em [docs/diagrams.md](docs/diagrams.md).

## Alguns números do projeto

Os números abaixo pertencem ao baseline interno da versão 1.0.25.

| Item | Resultado |
|---|---:|
| Arquivos TypeScript e TSX | 209 |
| Linhas TypeScript e TSX sem testes | cerca de 26,8 mil |
| Server Actions exportadas | 61 |
| Telas no App Router | 16 |
| Testes Vitest | 472 em 57 arquivos |
| Cenários Playwright | 19 |
| Rotas autenticadas no smoke do Electron | 12 |
| Configurações da matriz visual | 5 |
| Migrations aplicadas | 14 |
| Vulnerabilidades conhecidas no `npm audit` | 0 |
| Commits verificados no QA com Gitleaks | 223 |

## Telas

Capturei as telas abaixo no aplicativo desktop da versão 1.0.25. Os estados vazios e os dados demonstrativos evitam expor informações da loja.

| Dashboard | PDV com caixa fechado |
|---|---|
| ![Dashboard do StockFlow](screenshots/dashboard.png) | ![PDV com caixa fechado](screenshots/pdv-caixa-fechado.png) |

| Catálogo | Precificação e margens |
|---|---|
| ![Catálogo de produtos](screenshots/catalogo.png) | ![Tela de precificação](screenshots/precificacao.png) |

| Entrada por NF-e | Inventário e movimentações |
|---|---|
| ![Importação de NF-e](screenshots/entradas-nfe.png) | ![Balanço e inventário](screenshots/inventario.png) |

| Clientes | Fiados |
|---|---|
| ![Gestão de clientes](screenshots/clientes.png) | ![Gestão de fiados](screenshots/fiados.png) |

| Histórico de vendas | Trocas e devoluções |
|---|---|
| ![Histórico de vendas](screenshots/historico-vendas.png) | ![Trocas e devoluções](screenshots/trocas.png) |

| Perfil | Configurações da loja |
|---|---|
| ![Perfil do usuário](screenshots/perfil.png) | ![Configurações da loja](screenshots/configuracoes.png) |

### Componente em temas e tamanhos diferentes

| Tema escuro | Tema claro |
|---|---|
| ![Modal de cliente no tema escuro](screenshots/modal-cliente-escuro.png) | ![Modal de cliente no tema claro](screenshots/modal-cliente-claro.png) |

| Janela compacta | Tela ampla |
|---|---|
| ![Modal em janela compacta](screenshots/modal-cliente-compacto.png) | ![Modal em tela ampla](screenshots/modal-cliente-tela-ampla.png) |

A pasta [screenshots](screenshots/) também contém a validação em escala de 150% e a folha de identidade visual.

## Decisões que tomei durante o projeto

- Mantive preço, estoque e pagamentos validados no banco, sem depender apenas da interface.
- Usei transações para as operações que alteram vários registros.
- Criei componentes compartilhados para botões, formulários, alertas e modais.
- Adicionei tema claro e escuro, navegação por teclado, controle de foco e movimento reduzido.
- Separei as permissões por papel e mantive as verificações no servidor e no banco.
- Empacotei o Next.js junto com o Electron para entregar uma experiência de aplicativo Windows.

## Testes

Na versão 1.0.25, o projeto passou por lint, TypeScript, build, testes unitários, testes de componentes e cenários no Playwright. Também testei as rotas autenticadas dentro do Electron e conferi a interface em resoluções, escalas e temas diferentes.

O resumo está em [docs/quality.md](docs/quality.md). Os detalhes operacionais e as evidências completas continuam no repositório privado.

## Documentação

- [Arquitetura](docs/architecture.md)
- [Diagramas](docs/diagrams.md)
- [Interface e design system](docs/design-system.md)
- [Qualidade e testes](docs/quality.md)
- [Decisão de segurança](docs/security.md)

## Sobre este repositório

Não há código executável, credenciais, migrations, instaladores ou dados reais aqui. O material foi separado para mostrar o processo e as decisões técnicas sem expor a operação da loja.

O projeto é proprietário. As imagens, a marca e a documentação não possuem licença de reutilização.
