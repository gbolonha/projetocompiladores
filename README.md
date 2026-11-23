# Compilador Portugol — Fase 2: Análise Semântica e Geração de Código MEPA

Projeto desenvolvido para a disciplina de Compiladores. O objetivo deste trabalho é implementar as fases de análise semântica (com tabela de símbolos) e de geração de código intermediário MEPA, sobre o analisador léxico e sintático descendente recursivo (ASDR) da fase 1, para uma linguagem Portugol baseada em Pascal com palavras reservadas em português.

---

## Integrantes do Grupo

* **Gabriel Teixeira Bolonha** — RA: 10426937
* **Geovana Bomfim Rodrigues** — RA: 10410514

---

## Como Compilar e Executar

### Compilação
Utilize o comando exato especificado no enunciado:

```bash
gcc -Wall -Wno-unused-result -g -Og compilador.c hash_mack.o -o compilador
./compilador arquivo.txt
```

---

## `RTPR` e `DMEM` após o `CHPR`

Na Aula 7, o `RTPR n` retira os `n` parâmetros da pilha (`s <- s-(n+2)`). No interpretador `mepa` do repositório, o `RTPR` não retira os parâmetros: o valor de `n` é ignorado e os parâmetros continuam na pilha após o retorno. Testamos com `RTPR 0`, `RTPR 1` e `RTPR 5`, e o resultado foi o mesmo.

Para contornar isso, o compilador gera `RTPR n` ao final de cada rotina e um `DMEM n` logo após cada `CHPR`, onde `n` é o número de parâmetros da rotina chamada. Como o interpretador ignora o `n` do `RTPR`, é o `DMEM n` que retira os parâmetros, e a pilha fica como na definição da aula.

O `DMEM n` é impresso em dois pontos do `compilador.c`: na função `chamada_procedimento` (chamada de procedimento, linha 1284) e na função `fator` (chamada de função, linha 1662). Para seguir a notação da aula em um interpretador corrigido, basta remover esses dois `printf`.