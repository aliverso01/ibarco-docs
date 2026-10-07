# ibarco-docs

Documentação pública da API iBarco para parceiros integradores (agências, operadoras e outros canais de venda): busca, compra, pagamento e cancelamento de passagens fluviais. Feita com [Mintlify](https://mintlify.com): páginas em MDX (pt-BR) e configuração em `docs.json`.

## Rodar localmente

Requer Node.js 20 ou mais novo.

```bash
npx mint dev            # prévia em http://localhost:3000, recarrega a cada arquivo salvo
npx mint validate       # build estrito: falha em qualquer erro ou aviso
npx mint broken-links --check-anchors   # links internos e âncoras quebrados
```

Antes de abrir merge, `mint validate` e `mint broken-links` precisam passar sem erro.

## Estrutura

| Caminho | O que é |
|---|---|
| `docs.json` | Nome, cores, logos, navbar e navegação (grupos Começar, Guias, Referência). |
| `*.mdx` | Páginas. Cada uma tem `title` e `description` no frontmatter. |
| `postman/ibarco-api.postman_collection.json` | Coleção Postman v2.1, apontando para o sandbox e sem credenciais. |
| `logo/`, `favicon.svg` | Identidade visual. |
| `AGENTS.md` | Regras de conteúdo e de edição, para pessoas e agentes. |
| `.github/workflows/build.yml` | CI: `mint validate`, `mint broken-links` e `gitleaks`. Não publica nada. |

## Selos de status

Toda página ou seção leva um selo logo abaixo do título. São três valores, sempre neste formato:

```mdx
<Badge icon="circle-check" color="green">Disponível</Badge>
<Badge icon="clock" color="orange">Em breve</Badge>
<Badge icon="calendar" color="purple">Planejado</Badge>
```

- **Disponível:** em produção.
- **Em breve:** comportamento que entra no próximo deploy.
- **Planejado:** desenho proposto. Os valores ainda não decididos (prazos, percentuais, códigos) ficam num `<Warning>` que começa com **Valores propostos, sujeitos a confirmação**.

Ao entregar um recurso, troque o selo, remova o aviso de valores propostos, atualize a tabela "Estado da API" em `index.mdx`, a `referencia.mdx` e o `changelog.mdx`.

## Credenciais

Nunca coloque credencial real (chave de API, token, senha, segredo de webhook) em página, exemplo ou na coleção Postman. Use os marcadores `SUA_CHAVE_DE_API`, `<token_acesso>` e similares. O CI roda `gitleaks` em todo push.

## Publicação

A hospedagem é do Mintlify. O repositório GitHub `aliverso01/ibarco-docs` fica conectado no dashboard do Mintlify, com a branch de publicação `main`: cada merge na `main` publica o site. A `develop` serve de prévia dos cards em andamento.

## Fluxo de branches

- `main`: o que está publicado. Só recebe merge de um humano, depois do teste.
- `develop`: integração e prévia. Recebe o merge das branches de card.
- `IT-xxx-resumo`: uma branch por card, criada a partir da `develop` atualizada.
