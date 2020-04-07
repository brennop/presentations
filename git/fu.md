# CJR Class #2

Dominando o Git Fu

# Objetivos

- Reforçar uso de boas práticas
- Introduzir conceitos para devs e gerentes
- Despertar um interesse em git

# porquê estudamos história? 🤔

> Pensar o passado para compreender o presente e idealizar
> o futuro

# estudando a nossa história 🔎

```bash
git log
git reflog
```

- conteúdo
- mensagem
- arquivo

# achando o culpado 🕵

```bash
git blame
```

# usando esse conhecimento

```bash
git bisect start/bad/good
```

# Escrevendo uma boa história 📝

# Git Flow 🌊

```bash
git switch -c feature
# coda coda coda
git commit -m "codei"
git switch develop
git merge develop
```

1. Nomeie suas branches
2. Delete suas branches

# Commitando bem

# Commits atômicos ⚛

> Commite cedo, Commite com frequência

- Baby steps
- Checkpoint salvo
- Bem documentado

# you've got a message 📧

- Siga tudo que eu já disse 🙏
- Limite a quantidade de tipos
  - tarefa: Adiciona chave da API para build
  - docs: Documenta método show das mensagens
  - feat: Adiciona listagens de mensagens
  - fix: Remove validação desnecessária de idade
  - ui: Implementa grid na listagem de mensagens
  - test: Certifica que a listagem não quebra vazia
- Use emojis e não :emojis:

# Polindo a história 🧹

```bash
git rebase --interactive
```

- Juntar commits relevantes
- Corrigir e repensar mensagens

# Mantenha-se atualizado

# Mantenha-se atualizado 📼


```bash
git pull --rebase
```

- merge
- rebase
