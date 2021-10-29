# Glossário

---

## *Version Control Software* (VCS)

É um sistema usado para controlar o versionamento do código. Alguns exemplos são **git**, **Mercurial**, **SVN** e **Subversion**.

## Canal de Distribuição

Muitos softwares adotam a estratégia de dividir os canais de distribuição de acordo com a frequência de atualização de cada um, sendo comumente usados termos como **Stable**, **Beta**, **Nightly**, **Canary**, **Staging**, **Production**, **Development** entre outros.

Em um ambiente que utiliza o versionamento de código, geralmente esses nomes estarão associados com *branches* no repositório principal, sendo (geralmente) **Production** ou **Master** o nome da *branch* principal, ou seja, que contém o código pronto para uso do cliente. **Staging** é a *branch* que possui código em fase de testes, aguardando a confirmação para entrar em produção. **Development**, **Beta**, **Nightly** e **Canary** são *branches* dedicadas ao desenvolvimento do software e por esse motivo não são recomendadas para uso do público-geral, pois apresentam instabilidade e possíveis *bugs*, dado que o código ainda não foi totalmente testado ou nem foi totalmente implementado ainda. As diferenças entre elas reside no nível de abstração que cada uma carrega. Em minha experiência, geralmente o código é *"commitado"* na *branch* **Development**, passando para **Canary** ou **Nightly** assim que uma funcionalidade é implementada. Quando essa funcionalidade é testada e passa por testes básicos, ela é transferida (através de uma PR ou *merge*) para a *branch* **Beta**.

> Nota: Há casos de softwares que disponibilizam versões beta para o público, que são distribuídos com uma série de avisos sobre a instabilidade e possíveis *bugs*. Isso ajuda os desenvolvedores à depurar melhor os erros, visto que essa versão está sendo usada por usuários reais, evitando que uma série de erros possam ser resolvidos antes que aquela funcionalidade esteja disponível para todos.

 Por fim, a funcionalidade alcança a *branch* **Master** ou **Stable** quando já foi totalmente testada e está pronta para ser lançada ao público geral.

Geralmente, esse modelo de versionamento é utilizado por grandes desenvolvedores, que possuem diversas pessoas trabalhando na mesma funcionalidade e que precisam de agilidade na hora de testar e colocar em produção essas funcionalidades. Você pode adotar esse ou outro modelo de versionamento de código, porém não é aconselhado, visto que, quanto mais e mais *branches* diferentes são adicionadas à base de código, mais e mais trabalhoso se torna para administrar a árvore.
