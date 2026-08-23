# Qualidade e testes

## Baseline usado

Os resultados abaixo foram registrados no QA interno da versão 1.0.25, em 22 de agosto de 2026.

| Verificação | Resultado registrado |
|---|---:|
| ESLint | aprovado sem erros ou avisos |
| TypeScript | aprovado |
| Vitest | 472 testes em 57 arquivos |
| Playwright | 19 de 19 cenários |
| Smoke no Electron | 12 de 12 rotas autenticadas |
| Matriz visual | 5 de 5 configurações |
| `npm audit` | 0 vulnerabilidades conhecidas |
| Gitleaks | 223 commits verificados |

## O que foi testado

Os testes automatizados cobrem regras de cálculo, validações, ações do servidor, componentes e fluxos da interface. O Playwright foi usado no login, catálogo, PDV, clientes, fiado, inventário e outras rotas principais.

Também conferi:

- navegação por teclado e controle de foco;
- temas claro e escuro;
- resoluções de 360, 853 e 1440 pixels;
- diferentes escalas de tela do Windows;
- abertura do aplicativo empacotado;
- recuperação de senha no executável;
- bloqueio do PDV quando o caixa está fechado.

## Segurança revisada

O QA incluiu dependências, busca de segredos, configuração do Electron, autenticação, permissões, transações, upload de XML e pacote final do Windows.

Os relatórios completos, nomes internos e configurações permanecem no repositório privado. A versão pública informa apenas o resultado necessário para apresentar o trabalho.

## Pontos que acompanho

- O instalador ainda não tem assinatura digital, algo aceitável para o MVP de uso interno.
- Os testes de permissão precisam ser repetidos quando novos tipos de usuário forem criados.
- Backup e restauração devem continuar sendo testados durante o uso real.
- Uma distribuição maior exigiria um processo de assinatura e atualização mais completo.
