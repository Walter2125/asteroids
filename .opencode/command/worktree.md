---
description: Crea un git worktree en .worktrees/<nombre> a partir del argumento dado
---

El usuario quiere crear un git worktree local.

Argumento recibido: $ARGUMENTS

1. Analiza el argumento (puede contener espacios) y genera a partir de él un nombre de worktree válido:
   - Todo en minúsculas.
   - Espacios reemplazados por guiones (`-`).
   - Elimina caracteres inválidos para nombres de rama de git (`~`, `^`, `:`, `?`, `*`, `[`, `\`, secuencias `..`).
   - Colapsa guiones repetidos; sin guiones ni puntos al inicio o al final.
   - Si el argumento está vacío o no aporta contexto suficiente, pide un nombre al usuario antes de continuar.
   - Si los argumentos son muy largos simplificalos a un nombre significativo
   
2. Ejecuta EXACTAMENTE este comando, desde el directorio actual:

   git worktree add .worktrees/<nombre-del-worktree>

No hagas nada más: no cambies de directorio, no ejecutes ningún otro comando, no crees ni modifiques archivos.
