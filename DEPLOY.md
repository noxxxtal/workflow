# 🚀 Deploy para workflowbrasil.com via Cloudflare Pages

## Pré-requisitos

### 1. Obter Credenciais do Cloudflare

#### CLOUDFLARE_API_TOKEN
1. Acesse: https://dash.cloudflare.com/profile/api-tokens
2. Clique em **"Create Token"**
3. Use o template **"Edit Cloudflare Workers"** ou crie um custom com permissões:
   - `Account.Cloudflare Pages` - Edit
4. Copie o token gerado

#### CLOUDFLARE_ACCOUNT_ID
1. Acesse: https://dash.cloudflare.com/
2. Selecione seu domínio **workflowbrasil.com**
3. No menu lateral, role até o final da página
4. Copie o **Account ID** que aparece no canto inferior direito

### 2. Configurar Secrets no GitHub
1. Vá para: https://github.com/noxxxtal/workflow/settings/secrets/actions
2. Clique em **"New repository secret"**
3. Adicione os seguintes secrets:
   - Nome: `CLOUDFLARE_API_TOKEN` → Valor: (o token copiado)
   - Nome: `CLOUDFLARE_ACCOUNT_ID` → Valor: (o account ID copiado)

### 3. Criar Projeto no Cloudflare Pages
1. Acesse: https://dash.cloudflare.com/
2. Vá em **Pages** no menu lateral
3. Clique em **"Create a project"**
4. Selecione **"Connect to Git"** (opcional) ou crie um projeto vazio
5. Nomeie o projeto como: **workflow**

### 4. Configurar Domínio Customizado
1. No projeto Cloudflare Pages, vá em **"Custom domains"**
2. Clique em **"Set up a custom domain"**
3. Digite: **workflowbrasil.com**
4. Siga as instruções para configurar os registros DNS:
   - Tipo: `CNAME`
   - Nome: `@` (ou `www`)
   - Conteúdo: `workflow.pages.dev` (ou o domínio fornecido pelo Cloudflare)

## Como Funciona

1. **Push para main**: Qualquer commit na branch `main` dispara o workflow
2. **Build**: Instala dependências e executa o build
3. **Deploy**: Publica automaticamente no Cloudflare Pages
4. **Acesso**: Site disponível em https://workflowbrasil.com

## Testar o Deploy

Após configurar os secrets, faça um commit na branch `main`:

```bash
git add .
git commit -m "Configurar deploy automático"
git push origin main
```

Acompanhe o progresso em: https://github.com/noxxxtal/workflow/actions

## Troubleshooting

### Erro: "Invalid API Token"
- Verifique se o token tem as permissões corretas
- Regenere o token se necessário

### Erro: "Account ID not found"
- Confirme que o Account ID está correto
- Verifique se você tem acesso à conta

### Build falha
- Ajuste o comando `npm run build` no workflow conforme sua aplicação
- Se usar outro gerenciador (yarn, pnpm), altere os comandos

## Próximos Passos

- [ ] Configurar HTTPS/SSL (automático no Cloudflare)
- [ ] Configurar redirects (www → apex ou vice-versa)
- [ ] Adicionar variáveis de ambiente se necessário
- [ ] Configurar build específico para seu framework
