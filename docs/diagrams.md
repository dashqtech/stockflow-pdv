# Diagramas

## Partes principais

```mermaid
flowchart LR
    U[Usuário] --> E[Electron]
    E --> W[Next.js e React]

    W --> A[Autenticação]
    W --> B[Banco de dados]
    W --> F[Arquivos]

    subgraph Supabase
        A
        B
        F
    end
```

O Electron entrega a aplicação como programa Windows. O Next.js monta as telas, e o Supabase mantém as contas e os dados.

## Registro de uma venda

```mermaid
sequenceDiagram
    actor O as Operador
    participant P as PDV
    participant A as Aplicação
    participant B as Banco

    O->>P: Confirma o carrinho
    P->>A: Envia itens e pagamentos
    A->>A: Verifica sessão e dados
    A->>B: Solicita a venda
    B->>B: Confere preços e estoque
    B->>B: Grava tudo em uma transação
    B-->>A: Retorna o resultado
    A-->>P: Atualiza a interface
```

A venda só é concluída depois que o banco confere os valores e o estoque. Os registros relacionados são gravados juntos.

## Testes e entrega

```mermaid
flowchart LR
    C[Alteração] --> L[Lint e TypeScript]
    L --> T[Testes automatizados]
    T --> B[Build do Next.js]
    B --> E[Teste no Electron]
    E --> V[Revisão visual]
    V --> P[Instalador e portátil]
    P --> H[Hash SHA-256]
```

Os testes que podem alterar dados são separados dos testes de leitura. O instalador só é gerado depois das verificações do código e da interface.
