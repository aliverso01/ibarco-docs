# Instruções para quem edita esta documentação

Vale para pessoas e para agentes de IA. Leia antes de alterar qualquer página.

## Sobre o projeto

- Site de documentação [Mintlify](https://mintlify.com). Páginas em MDX com frontmatter YAML (`title` e `description` obrigatórios); configuração e navegação em `docs.json`.
- Toda página nova precisa entrar em `navigation.groups` do `docs.json`.
- Antes de concluir qualquer mudança, rode `npx -y mint validate` e `npx -y mint broken-links --check-anchors`. Os dois precisam passar sem erro.
- Use só componentes que existem no Mintlify (`Note`, `Tip`, `Warning`, `Danger`, `Info`, `Check`, `Tabs`/`Tab`, `Steps`/`Step`, `Card`, `Columns`, `Badge`, blocos ```mermaid). Os callouts não aceitam `title`: use uma primeira linha em negrito.
- Em MDX, chaves `{}` e `<` fora de código são interpretados como JSX. Caminhos como `/vendas/{id}` e marcadores como `<token_acesso>` vão sempre entre crases ou em bloco de código.
- Links internos são absolutos, sem extensão: `/pagamento#acesso-à-venda`. A âncora é o título em minúsculas, com acentos preservados e espaços trocados por hífens. Para ter uma âncora estável, prefira um título em texto puro e ponha o endpoint num subtítulo abaixo. Confirme com `mint broken-links --check-anchors`.

## Público e tom

- O leitor é o **parceiro que vai integrar** com a API: desenvolvedor de agência, operadora ou integrador. Escreva em pt-BR, na segunda pessoa ("você"), em frases curtas.
- Tom neutro e prático: descreva o que a API faz e o que o parceiro deve fazer ("a API responde `404` quando a busca não encontra saídas; trate como nenhum resultado"). Nunca escreva como desculpa, justificativa ou histórico.

## Limites de conteúdo

O que **nunca** entra nas páginas:

- Números de card do Jira (`IT-xx` ou "o card..."), nomes de branch, sprints ou qualquer referência ao processo interno.
- Ferramentas internas e de bastidor: ferramenta de documentação usada antes, documentações antigas, painéis internos, infraestrutura, nomes de serviços internos.
- Histórico de correções ("corrigido em relação a...", "antes funcionava assim", "valor legado", "mantido por compatibilidade", "ainda não é padronizado", "até a iBarco anunciar...").
- O que a API **não** faz quando isso não ajuda a integrar: endpoints internos ("não chame este caminho"), métodos não oferecidos ao parceiro, modelos comerciais em avaliação.
- Comparações entre a regra atual e uma regra futura que não mudam a ação do parceiro. Mantenha só a orientação prática.
- Credencial real de qualquer tipo. Exemplos usam `SUA_CHAVE_DE_API`, `<token_acesso>` e dados fictícios.

O que **sempre** fica, em tom neutro: formatos de erro por endpoint, comportamentos que o parceiro precisa tratar (busca vazia com `404`, janela de venda com HTTP `400` e `status_code: ["409"]`, valores monetários como texto ou número, cupom recusado na criação com `500`, a grafia `avaliable_seats`, `PENDING` equivalente a `CREATED`), limite de requisições, segurança da chave e LGPD.

## Selos de status

Três valores, sem número de card, sempre com este markup:

```mdx
<Badge icon="circle-check" color="green">Disponível</Badge>
<Badge icon="clock" color="orange">Em breve</Badge>
<Badge icon="calendar" color="purple">Planejado</Badge>
```

- **Disponível:** em produção.
- **Em breve:** comportamento que entra no próximo deploy.
- **Planejado:** desenho proposto. Toda seção Planejado traz os valores propostos num `<Warning>` que começa com **Valores propostos, sujeitos a confirmação**.

Ao mudar um status, atualize também a tabela "Estado da API" em `index.mdx`, a `referencia.mdx` e o `changelog.mdx`.

## URL base

Todos os exemplos (texto, `curl`, JSON, URLs de mídia, coleção Postman) usam o sandbox: `https://sandbox-api.ibarco.com.br/api`. A URL de produção não aparece na documentação: ela é informada junto com as credenciais de produção. Links para o site (`https://ibarco.com.br/...`) ficam como estão.
