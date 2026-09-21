# Pele como Jóia

O despertar da matéria. Apresentação do jantar em site estático.

Site: https://pele-como-joia.vercel.app

- `index.html`: a apresentação inteira (capa, tema, mapa e cada etapa com referências)
- `media/`: imagens e vídeos de referência

Sem build: a Vercel publica os arquivos como estão.

## Trabalhar em outro computador

Baixar o projeto:

```bash
git clone https://github.com/theforcex-code/pele-como-joia.git
```

Publicar no mesmo site, sem depender de nenhuma ligação com o GitHub:

```bash
npm i -g vercel
```

```bash
vercel login
```

```bash
vercel link --yes --project pele-como-joia
```

```bash
vercel deploy --prod --yes
```

O `vercel link` liga a pasta ao projeto que já existe na Vercel, então o
`deploy` atualiza https://pele-como-joia.vercel.app. Se em vez disso você
criar um projeto novo na Vercel, ele nasce com outro endereço: o nome
`pele-como-joia.vercel.app` já pertence ao projeto atual.

## Atualizar de qualquer computador

Cada push na branch `main` publica o site sozinho, pelo fluxo
`.github/workflows/publicar.yml` (GitHub Actions roda `vercel deploy --prod`).
Dá para editar o `index.html` pelo próprio site do GitHub, sem instalar nada.

Para isso funcionar, o repositório precisa de um segredo `VERCEL_TOKEN`:

1. criar o token em https://vercel.com/account/settings/tokens
   (escopo: o time `asjhkqlzwv`, validade sem prazo)
2. guardar em **Settings → Secrets and variables → Actions → New repository
   secret**, com o nome `VERCEL_TOKEN`:
   https://github.com/theforcex-code/pele-como-joia/settings/secrets/actions/new

Enquanto o segredo não existir, o fluxo falha logo no começo avisando isso.
O identificador do projeto e do time já estão no próprio fluxo, não são segredo.

## Ligar a Vercel ao GitHub (alternativa ao fluxo acima)

Hoje a Vercel não está ligada ao GitHub, e por isso qualquer tentativa de
importar ou conectar o repositório falha com:

> Failed to link theforcex-code/pele-como-joia. You need to add a Login
> Connection to your GitHub account first.

Isso se resolve na conta da Vercel, não no repositório:

1. vercel.com → foto do perfil → **Account Settings** → **Authentication**
2. em **Login Connections**, conectar o **GitHub** (`theforcex-code`)
3. no projeto **pele-como-joia** → **Settings** → **Git** → **Connect Git
   Repository** → `theforcex-code/pele-como-joia`
   (ou rodar `vercel git connect` dentro da pasta)

Depois disso, todo `git push` na branch `main` publica sozinho.
