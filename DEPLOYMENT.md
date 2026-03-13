# Deployment - Mug3D Clone

Guia completo para fazer deploy do projeto Mug3D Clone em diferentes plataformas.

## Opções de Deploy

### 1. Vercel (Recomendado para Vite + React)

**Vantagens:**
- Deploy automático via Git
- Suporte nativo para Vite
- CDN global
- Preview automático de PRs

**Passos:**

1. **Prepare o repositório**
```bash
git push origin main
```

2. **Conecte no Vercel**
- Acesse [vercel.com](https://vercel.com)
- Clique em "New Project"
- Selecione seu repositório GitHub
- Vercel detectará automaticamente que é um projeto Vite

3. **Configure variáveis de ambiente**
- Na aba "Environment Variables"
- Adicione as variáveis necessárias

4. **Deploy**
- Clique em "Deploy"
- Seu site estará disponível em `seu-projeto.vercel.app`

### 2. Netlify

**Vantagens:**
- Fácil integração com GitHub
- Suporte a funções serverless
- Bom para sites estáticos

**Passos:**

1. **Conecte seu repositório**
- Acesse [netlify.com](https://netlify.com)
- Clique em "New site from Git"
- Selecione seu repositório

2. **Configure build**
- Build command: `pnpm build`
- Publish directory: `dist`

3. **Variáveis de ambiente**
- Adicione em "Site settings" > "Build & deploy" > "Environment"

4. **Deploy automático**
- Cada push para `main` fará deploy automático

### 3. GitHub Pages

**Vantagens:**
- Gratuito
- Integrado com GitHub
- Sem necessidade de servidor

**Passos:**

1. **Configure o repositório**
```bash
# No package.json, adicione:
"homepage": "https://seu-usuario.github.io/mug3d-clone"
```

2. **Configure GitHub Actions**

Crie `.github/workflows/deploy.yml`:
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup pnpm
        uses: pnpm/action-setup@v2
        with:
          version: 10
      
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'pnpm'
      
      - name: Install dependencies
        run: pnpm install
      
      - name: Build
        run: pnpm build
      
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

3. **Ative GitHub Pages**
- Vá para "Settings" > "Pages"
- Source: "Deploy from a branch"
- Branch: `gh-pages`

### 4. Railway

**Vantagens:**
- Suporte completo para Node.js
- Fácil integração com GitHub
- Bom para full-stack

**Passos:**

1. **Crie conta no Railway**
- Acesse [railway.app](https://railway.app)

2. **Conecte seu repositório**
- Clique em "New Project"
- Selecione "Deploy from GitHub repo"

3. **Configure variáveis**
- Adicione variáveis de ambiente no dashboard

4. **Deploy**
- Railway fará deploy automático

### 5. Render

**Vantagens:**
- Gratuito com limitações
- Suporte a Node.js
- Fácil de usar

**Passos:**

1. **Crie conta no Render**
- Acesse [render.com](https://render.com)

2. **Novo Web Service**
- Clique em "New +"
- Selecione "Web Service"
- Conecte seu repositório GitHub

3. **Configure**
- Build command: `pnpm install && pnpm build`
- Start command: `pnpm preview`
- Environment: Node

4. **Deploy**
- Clique em "Create Web Service"

## Checklist de Deploy

Antes de fazer deploy, verifique:

- [ ] Todas as variáveis de ambiente estão configuradas
- [ ] Build local funciona: `pnpm build`
- [ ] Sem erros de TypeScript: `pnpm check`
- [ ] Código formatado: `pnpm format`
- [ ] Testes passam (se aplicável)
- [ ] README.md está atualizado
- [ ] Versão no package.json foi incrementada
- [ ] CHANGELOG foi atualizado
- [ ] Não há segredos no código

## Variáveis de Ambiente Necessárias

```
VITE_APP_TITLE=Mug3D Clone
VITE_APP_LOGO=https://seu-dominio.com/logo.png
VITE_ANALYTICS_ENDPOINT=https://analytics.seu-dominio.com
VITE_ANALYTICS_WEBSITE_ID=seu-website-id
```

## Monitoramento Pós-Deploy

### Verificar Performance
- Use Lighthouse (Chrome DevTools)
- Verifique Core Web Vitals
- Monitore tempo de carregamento

### Logs e Erros
- Configure error tracking (Sentry, LogRocket)
- Monitore console errors
- Verifique network requests

### Analytics
- Configure Google Analytics
- Acompanhe user behavior
- Monitore conversões

## Troubleshooting

### Build falha com "Cannot find module"
```bash
# Limpe cache e reinstale
pnpm store prune
pnpm install
pnpm build
```

### Modelos 3D não carregam em produção
- Verifique CORS headers
- Confirme URLs dos modelos
- Verifique console para erros

### Performance ruim
- Use `pnpm build --analyze` para ver bundle size
- Otimize imagens
- Considere lazy loading

### Variáveis de ambiente não funcionam
- Confirme que começam com `VITE_`
- Verifique se foram adicionadas corretamente
- Reconstrua após adicionar variáveis

## Rollback

Se algo der errado após deploy:

### Vercel
- Vá para "Deployments"
- Clique em um deployment anterior
- Clique em "Promote to Production"

### Netlify
- Vá para "Deploys"
- Selecione um deploy anterior
- Clique em "Publish deploy"

### GitHub Pages
- Revert o commit: `git revert <commit-hash>`
- Push para main

## Domínio Customizado

### Vercel
1. Vá para "Settings" > "Domains"
2. Adicione seu domínio
3. Configure DNS conforme instruções

### Netlify
1. Vá para "Site settings" > "Domain management"
2. Clique em "Add custom domain"
3. Configure DNS

### GitHub Pages
1. Vá para "Settings" > "Pages"
2. Adicione domínio customizado
3. Configure DNS (CNAME ou A record)

## Certificado SSL

A maioria das plataformas fornece SSL grátis automaticamente. Se não:

- Vercel: Automático
- Netlify: Automático
- GitHub Pages: Automático
- Railway: Automático
- Render: Automático

## Backup

Sempre mantenha backups:

```bash
# Backup do repositório
git clone --mirror https://github.com/seu-usuario/mug3d-clone.git

# Backup do banco de dados (se aplicável)
# Configurar conforme seu provider
```

## Próximos Passos

1. Escolha uma plataforma
2. Siga as instruções específicas
3. Configure domínio customizado
4. Configure monitoramento
5. Teste em produção
6. Configure CI/CD

Dúvidas? Consulte a documentação da plataforma escolhida.
