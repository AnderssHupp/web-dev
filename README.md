# Web Dev - Formulario de Utilizador

Aplicacao Vue 3 + Vite que implementa uma interface com:
- Header global
- Sidebar
- Cards de "Tipo de utilizador" e "Contacto"
- Validacoes de formulario (email, palavra-passe, telefone e tipo de utilizador)

## Requisitos

- Node.js: `^20.19.0` ou `>=22.12.0`
- npm (instalado junto com Node.js)

## Instalacao

Na raiz do projeto (`web-dev`):

```sh
npm install
```

## Como rodar localmente

```sh
npm run dev
```

Depois abra o endereco mostrado no terminal (por padrao: `http://localhost:5173`).

## Build de producao

```sh
npm run build
```

Para visualizar a build localmente:

```sh
npm run preview
```

## Como testar o projeto (manual)

### 1) Layout
- Confirmar se o header aparece no topo e a sidebar fixa a esquerda.
- Confirmar se os cards "Tipo de utilizador" e "Contacto" renderizam corretamente.

### 2) Card toggle (abrir/fechar)
- Clicar no botao `-` / `+` no header do card.
- Verificar se o conteudo do card abre/fecha sem submeter o formulario.

### 3) Validacoes do card Contacto
- **Email**:
  - Digitar email invalido (ex.: `abc`) e verificar mensagem de erro.
  - Digitar email valido e confirmar que o erro desaparece.
- **Palavra-passe**:
  - Digitar menos de 8 caracteres e verificar erro.
  - Digitar 8+ caracteres e confirmar que o erro desaparece.
- **Telefone**:
  - Deixar vazio e verificar erro de obrigatoriedade.
  - Digitar letras e verificar erro de "apenas numeros".
  - Digitar menos/mais de 9 digitos e verificar erro.
  - Digitar exatamente 9 digitos e confirmar que o erro desaparece.

### 4) Validacao de tipo de utilizador
- Tentar submeter sem marcar nenhuma opcao.
- Confirmar mensagem: "Selecione pelo menos um tipo de utilizador".
- Marcar uma ou mais opcoes e confirmar que permite submeter.

### 5) Submissao e cancelamento
- Clicar em **GUARDAR** com dados validos:
  - Formulario deve ser enviado.
  - Payload deve incluir telefone com prefixo `+351`.
  - Campos devem ser limpos apos envio.
- Clicar em **Cancelar**:
  - Campos e erros devem ser resetados.

## Scripts disponiveis

- `npm run dev` - roda em modo desenvolvimento (hot reload)
- `npm run build` - gera build de producao
- `npm run preview` - sobe servidor local para visualizar a build
