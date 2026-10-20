# Calculadora Vue.js — Aula 01

Atividade prática da primeira aula de Vue.js.

## Objetivo

Construir uma **calculadora funcional** usando **apenas Vue.js** (via CDN), com as quatro operações básicas (`+`, `−`, `×`, `÷`) e exponenciação (`x²` e `x^y`).

Toda a parte visual já está pronta. Você vai implementar **a lógica em Vue**.

## O que você vai praticar

- `data()` — o estado reativo da calculadora
- `methods` — as ações da calculadora
- `{{ }}` — a interpolação que mostra o visor
- `@click` — os eventos dos botões

## Como pegar o código
### Se é a primeira vez (não tem o projeto localmente)

```bash
git clone <URL_DO_REPOSITORIO>
cd <NOME_DO_REPOSITORIO>
```

### Se já tem o projeto e precisa sincronizar as novidades

```bash
git pull origin main
```

## O que falta fazer?

**Já está pronto (sugiro n mexer):**

- Toda a estrutura HTML
- Todo o visual em Tailwind CSS + DaisyUI
- Os botões da calculadora já estão ligados aos métodos (`@click`)

**Falta fazer:**

- O `data()` — o estado inicial da calculadora
- Cinco métodos — a lógica de cada operação

Abra o `index.html` e siga os comentários `TODO` dentro do `<script>`.

## Tarefas

### TODO 1 — `data()`

Declare o **estado reativo** da calculadora. Você vai precisar de quatro propriedades:

| Propriedade | Tipo | Valor inicial | Para que serve |
|---|---|---|---|
| `display` | string | `'0'` | O texto exibido no visor |
| `firstOperand` | number ou null | `null` | O primeiro número da operação |
| `operator` | string ou null | `null` | O operador pendente (`'+'`, `'-'`, `'*'`, `'/'`, `'^'`) |
| `waitingForSecond` | boolean | `false` | `true` enquanto espera o segundo número |

### TODO 2 — `appendDigit(digit)`

Digita um dígito (`0` a `9`) no visor.

**Regras:**
- Se `waitingForSecond` for `true`: substitui o visor pelo dígito e volta `waitingForSecond` para `false`.
- Se o visor for `'0'`: substitui pelo dígito (para não virar `'07'`).
- Senão: concatena o dígito ao final.

**Exemplos:**
- `display='0'`, `digit='5'` → `display='5'`
- `display='12'`, `digit='3'` → `display='123'`
- `display='12'`, `waitingForSecond=true`, `digit='7'` → `display='7'`

### TODO 3 — `appendDecimal()`

Adiciona um ponto decimal ao visor.

**Regras:**
- Se `waitingForSecond` for `true`: o visor vira `'0.'` e `waitingForSecond` volta a `false`.
- Senão, se o visor **ainda não tem** ponto: adiciona `'.'` ao final.
- Se já tem ponto: não faz nada (evita `'3.1.4'`).

### TODO 4 — `setOperator(op)`

Registra uma operação pendente.

**Regras:**
- Se já existe um `operator` **e** `waitingForSecond` for `false`: chame `this.calculate()` primeiro (encadeia operações como `5 + 3 ×`).
- Salve `firstOperand = parseFloat(display)`.
- Salve `operator = op`.
- Marque `waitingForSecond = true`.

### TODO 5 — `calculate()`

Executa a operação pendente e mostra o resultado.

**Regras:**
- Se `operator` for `null` **ou** `firstOperand` for `null`: retorne sem fazer nada.
- `a = firstOperand`
- `b = parseFloat(display)`
- Aplique a operação:
  - `'+'` → `a + b`
  - `'-'` → `a - b`
  - `'*'` → `a * b`
  - `'/'` → se `b === 0`, resultado é `'Erro'`; senão `a / b`
  - `'^'` → `Math.pow(a, b)`
- Coloque o resultado (convertido para string) no `display`.
- Volte `firstOperand` e `operator` para `null`.
- Marque `waitingForSecond = true` (o próximo dígito começa do zero).

### TODO 6 — `square()`

Eleva o número atual ao quadrado (operação unária `x²`).

**Regras:**
- Pegue `n = parseFloat(display)`.
- Substitua o `display` por `String(n * n)`.
- Marque `waitingForSecond = true`.

### Método de exemplo (já implementado)

O método `clear()` já está pronto e serve de referência para você ver como se acessa e altera o estado:

```js
clear() {
  this.display = '0';
  this.firstOperand = null;
  this.operator = null;
  this.waitingForSecond = false;
}
```

## Comportamento esperado

Use esta tabela para testar sua calculadora:

| Cliques | Visor deve mostrar |
|---|---|
| `7` `+` `5` `=` | `12` |
| `9` `×` `8` `=` | `72` |
| `1` `0` `÷` `4` `=` | `2.5` |
| `2` `^` `8` `=` | `256` |
| `1` `2` `x²` | `144` |
| `5` `÷` `0` `=` | `Erro` |
| `7` `+` `3` `=` `×` `2` `=` | `20` |
| `C` | `0` |

> **Dica:** abra o **Console** do navegador (F12) e digite `document.querySelector('div.text-3xl').textContent`. Você vai ver o valor atualizado.

## Personalização (opcional)

Depois que a calculadora estiver funcionando, customize para deixar com a sua cara:

- Troque as cores dos botões (`btn-primary` → `btn-secondary`, `btn-accent`, etc.).
- Mude o fundo da página (`bg-base-200` → `bg-base-300` ou um gradiente do Tailwind).
- Troque o título `Calculadora Vue` por outro.
- Adicione uma sombra mais forte (`shadow-2xl`) no card.
- Troque a fonte do visor (`font-mono` → outra fonte do Tailwind).

**Importante:** a calculadora precisa **continuar funcionando** depois da customização.

## Entrega no GSA

Quando terminar, siga estes passos:

### 1. Crie uma branch para a sua entrega

```bash
git checkout -b aula-01-calculadora
```

### 2. Faça commit das suas alterações

```bash
git add .
git commit -m "Aula 01 — Calculadora Vue"
```

### 3. Envie a branch para o GitHub

```bash
git push -u origin aula-01-calculadora
```

### 4. Copie o link da branch

No GitHub, abra a aba **Branches**, encontre `aula-01-calculadora` e **copie a URL** da branch. O link deve ser algo como:

```
https://github.com/<seu-usuario>/<repo>/tree/aula-01-calculadora
```

### 5. Submeta no GSA

Cole o **link da branch** no campo de entrega do GSA.