## Basics
Commands executed on Linux command line either produce output, require input or throw an error message.

There are two kinds of output:
- **`stdout`** standard output messages;
- **`stderr`** standard error messages.
## Output Redirection
There is a certain notation that allows a command to redirect its output to a file.

- **`>`** redirects stdout to a file;
- - **`>>`** saves stdout to a file;
- **`2>`** redirects stderr to a file;
- **`&>`** redirects them both.

## Tail
```bash
# PIPES
ls | head -2
# Mostra os dois primeiros arquivos do diretório
ls | head -2 | tail -1
# Passa o stdout do head para o tail, o tail mostra o último arquivo


```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3ODc3MTczMTJdfQ==
-->