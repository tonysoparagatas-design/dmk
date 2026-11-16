# DMK Motors — site estático para GitHub Pages

Projeto estático com duas páginas principais:

- `index.html` — página inicial institucional e catálogo de veículos.
- `admin.html` — painel protegido por autenticação Supabase para gerenciar veículos.

A marca usa o logotipo fornecido e uma paleta de preto, branco e amarelo.

## Arquivos

```text
DMK-Motors/
├── index.html
├── admin.html
├── supabase.sql
└── assets/
    ├── config.js
    ├── styles.css
    ├── site.js
    ├── admin.js
    └── dmk-logo.png
```

## 1. Configurar o Supabase

1. Crie um projeto no Supabase.
2. Abra **SQL Editor** e execute todo o arquivo `supabase.sql`.
3. Vá a **Authentication → Users → Add user** e crie o usuário administrador.
4. Copie o UUID desse usuário e execute no SQL Editor:

```sql
insert into public.admin_users(user_id)
values ('COLE_O_UUID_DO_ADMIN_AQUI');
```

5. Abra `assets/config.js` e substitua os dois valores de exemplo:

```js
window.DMK_CONFIG = {
  SUPABASE_URL: 'https://SEU-PROJETO.supabase.co',
  SUPABASE_ANON_KEY: 'SUA_CHAVE_ANON_PUBLIC'
};
```

Use apenas a chave pública `anon`/`publishable`. **Nunca** coloque `service_role`, senha de banco ou segredo privado no GitHub.

## 2. Testar localmente

Não abra os HTMLs por `file://`. Use um servidor local. Uma opção simples, com Python instalado:

```bash
python -m http.server 8000
```

Depois abra `http://localhost:8000`.

## 3. Publicar no GitHub Pages

1. Crie um repositório no GitHub, por exemplo `dmk-motors`.
2. Envie todos os arquivos e a pasta `assets` para a raiz do repositório.
3. No GitHub, abra **Settings → Pages**.
4. Em **Build and deployment**, escolha **Deploy from a branch**.
5. Selecione a branch `main` e a pasta `/ (root)`, depois salve.
6. Aguarde o GitHub Pages publicar o endereço exibido nessa tela.

O endereço da página inicial será algo como `https://SEU-USUARIO.github.io/dmk-motors/` e o painel ficará em `https://SEU-USUARIO.github.io/dmk-motors/admin.html`.

## 4. Como usar o painel

1. Acesse `admin.html`.
2. Entre com o e-mail e a senha cadastrados no Supabase Auth e autorizados na tabela `admin_users`.
3. Cadastre marca, modelo, anos, preço, quilometragem, câmbio, combustível, cor, opcionais e descrição.
4. Selecione as fotos e publique.
5. Os veículos com status **Disponível** aparecem no site. Reservados e vendidos ficam ocultos do catálogo público.
6. Use Editar para atualizar dados e Excluir para remover um anúncio.

## 5. Dados comerciais utilizados

- Empresa: DMK Motors
- Atividade: compra, venda e troca de veículos
- Endereço informado: Rua Campos Salles, 2276 — Vila Faustina II, Valinhos/SP
- WhatsApp Diogo: +55 19 99163-2058
- WhatsApp Igor: +55 19 99307-4852
- Instagram: https://www.instagram.com/dmkmotors/

Confirme os dados e condições comerciais com a empresa antes da publicação definitiva.

## Observações importantes

- GitHub Pages hospeda arquivos estáticos; o Supabase faz autenticação, banco de dados e armazenamento de fotos.
- A chave pública Supabase é visível no navegador por natureza. A segurança depende das políticas RLS incluídas no SQL e da autorização na tabela `admin_users`.
- Não cadastre veículos de exemplo como se fossem estoque real.
- O catálogo e painel precisam das credenciais e do SQL configurados para operar com dados persistentes.
- A página utiliza uma fotografia automotiva ilustrativa no banner. Troque-a por uma foto autorizada da DMK Motors quando disponível.
- A página inicial tem catálogo dinâmico e consulta via WhatsApp; esta versão de duas páginas não cria uma URL exclusiva por veículo.
