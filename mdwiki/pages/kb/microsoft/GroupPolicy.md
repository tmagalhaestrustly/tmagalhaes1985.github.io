# Group Policy

## Sobre as Políticas de Grupo

## Resetar todas as GPOs aplicadas a um computador para o padrão

Abra um prompt de comando e execute os seguintes comandos na sequência:

1. ```secedit /configure /cfg C:\Windows\inf\defltbase.inf /db defltbase.sdb /verbose```
2. ```RD /S /Q "C:\Windows\System32\GroupPolicyUsers"```
3. ```RD /S /Q "C:\Windows\System32\GroupPolicy"```

## Resetar a Default Domain Policy para o padrão

### Sintaxe

```DCGPOFix [/ignoreschema] [/target: {Domain | DC | Both}] [/?]```

### Exemplos

```dcgpofix /ignoreschema /target:Domain```

```dcgpofix /ignoreschema /target:DC```