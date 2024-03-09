# Java - trabalhando com exceções

Curso da alura para me aprofundar em java e exception, botarei conceitos para posterior consulta.

## Notas sobre curso

A pilha de execução em Java armazena informações sobre as chamadas de função em um formato Last In, First Out (LIFO). Cada vez que uma função é chamada, um novo quadro é adicionado ao topo da pilha. Quando a função é concluída, seu quadro é removido. A pilha de execução é fundamental para o fluxo de controle e o gerenciamento de chamadas de função no programa Java.

## O que ocorre quando quebra a pilha
Exceções, quando não tratada, retornam exceções que quebram o código, para previnir que tal ponto ocorra, pode fazer o try-catch
```Java
 Usuario usuario = null;
                try {
                    System.out.println(usuario.nome);
                }
                catch (NullPointerException e){
                    System.out.println(e.getMessage());
                }

```



