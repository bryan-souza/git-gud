# Conceitos-Chave do Versionamento de Código

Vamos abordar aqui alguns termos que vimos anteriormente e detalhar como cada um contribui para o fluxo de trabalho de um repositório.

## *Branch* (ou ramificação)

`Branch` é o carro-chefe do repositório. É ele quem fica responsável por encapsular todas as mudanças feitas no código em alto nível, indicando quais mudanças (commits) foram feitos e em qual ordem.

Se você voltar na seção anterior, vai ver que usei nomes para cada ramificação: `main`, `V2.0` e `PR #1`. Esses são nomes fictícios que usei para demonstrar o funcionamento das `branches` no repositório, mas cada uma deve ser nomeada seguindo algumas regras:

* Não podem começar com `.` ou terminar com `.lock`.

* Não podem ter `..` em lugar nenhum do nome.

* Não podem conter `?`, `*` ou `[]`em nenhum lugar no nome.

* Não podem conter `~`, `^`, `espaço` ou `:` em lugar nenhum do nome.

* Não podem terminar com `.`

* Não podem conter a sequência `@{`

* Não podem ser nomeadas como `@`

* Não podem conter `\` em nenhum lugar do nome

Tais restrições se aplicam pois o próprio git usa tais caracteres para referenciar ações em sua API interna, funcionando como se fossem `palavras reservadas`.
