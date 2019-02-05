# Groselha Tokens Kickstart

## Instalação do projeto

### 1. Inicie o projeto clonando o repositório de tokens:
`$ git clone https://github.com/thiagokpelo/groselha-tokens.git`

### 2. Entre no diretório

`$ cd groselha-tokens`

### 3. Instale as dependências:
`$ npm install`

---

## Como executar

```
$ node theo src/tokens.yml --transform web --format scss --dest dist"
```

---

## Explicação do projeto
O projeto de Token tem como dependencia o [THEO - SalesforceUx](https://github.com/salesforce-ux/theo). O THEO converte um arquivo `.yaml` para diversos tipos de arquivos. Por exemplo: `.json`, `.xml`, `.css`, `.sass`, `.less`, `.js`, entre outros.

Para funcionar corretamente, precisamos seguir uma estrutura base que foi determinada pela ferramenta. Você pode ver todos os detalhes no [Readme.md](https://github.com/salesforce-ux/theo) que é uma mini documentação.

Através desta estrutura o THEO consegue identificar os tipos dos valores e converter para cada particularidade de linguagem.

---

## Árvore de diretórios
A estrutura do projeto é bem simples, ele é divido em 3 partes principais.


```
groselha-tokens/
├── src/
│   ├── border/
│   ├── color/
│   ├── opacity/
│   ├── radius/
│   ├── shadow/
│   ├── spacing/
│   ├── typography/
│   └── tokens,.yml
├── dist/
└── [additional files]
```

### 1. src/
É o diretório principal, aqui esta todas as categorias de tokens que você pode gerar. O ponto de entrada para o `THEO` é o arquivo `tokens.yml`.

### 2. dist/
Diretório dos tokens compilados. É aqui que ficam todos os arquivos de tokens versionados.

---

## Exemplos

### 1. Arquivo principal
Arquivos que importamos todas as categorias de Tokens.
```yml
# src/tokens.yml
imports:
  - ./border/index.yml
  - ./radius/index.yml
  - ./color/index.yml
  - ./opacity/index.yml
  - ./shadow/index.yml
  - ./spacing/index.yml
  - ./typography/index.yml
global:
  category: tokens
```

### 2. Arquivo de tokens
São os arquivos de categorias. Esses arquivos são os que são lidos pelo THEO e através deles a ferramenta cria os nomes e os valores dos tokens.

```yml
# claro/color/brand.yml
---
global:
  type: color # Com esse valor o THEO converte as unidades
  category: category-color

imports:
  - ./aliases.yml # Importando variaveis de apelido

props:
  - name: color-brand-primary-darkest # Nome do token
    value: '{!color-red-darkest}' # Valor do token em variável
    meta:
      friendlyName: Color Brand Primary Darkest
    category: brand-color

  - name: color-brand-secondary-dark # Nome do token
    value: '{!color-yellow-dark}' # Valor do token em variável
    meta:
      friendlyName: Color Brand Secondary Dark
    category: brand-color
```

### 3. Arquivo de variáveis
Nesse arquivo criamos variáveis separadas por grupo. Podemos ter diversos arquivos desses. Cada um na raíz da sua categoria.

```yml
# src/color/aliases.yml
---
global:
  type: aliases # Atribui o valor do tipo do arquivo
  category: pallete-color

aliases:
  color-red:                '#DA291C' # Criacao da variável
  color-red-dark:           '#A61F16'
  color-red-darkest:        '#70150F'
  color-red-light:          '#E35C53'
  color-red-lightest:       '#FFB2AC'
```

### 4. Arquivo de Saída

```less
//  groselha-tokens-0.0.1.less

@color-brand-primary = #DA291C
@color-brand-secondary = #F5B921
@color-support-success = #87D3A2
@color-support-danger = #E7574D
[...]
```

---

## Tabela de valores

#### 1. format
Nome            | Valor do formato
-------------------- | ----------------------
CSS (Variáveis)      | `custom-properties.css`
CSS (Módulos)        | `cssmodules.css`
SCSS                 | `scss`
SCSS (Map)           | `map.scss`
SCSS (Map Variables) | `map.variables.scss`
SCSS (List)          | `list.scss`
SASS                 | `sass`
LESS                 | `less`
STYLUS               | `styl`
JS (Module)          | `module.js`
JS (Common)          | `common.js`

#### 2. transform
Nome    | Valor de Transformação
------- | ----------------------
raw     | `[]`
web     | `['color/rgb']`
ios     | `['color/rgb', 'relative/pixelValue', 'percentage/float']`
android | `['color/hex8argb', 'relative/pixelValue', 'percentage/float']`

#### 3. dest
Esse parâmetro escolhe qual o nome do diretório de saída dos tokens. Por padrão seu valor é `dist`.

---

## Licença
MIT
