# Setup e Instalação - Mug3D Clone

Guia completo para configurar o projeto Mug3D Clone em seu ambiente local.

## Pré-requisitos

- **Node.js**: v18 ou superior
- **pnpm**: v10 ou superior (ou npm/yarn como alternativa)
- **Git**: para controle de versão

### Verificar Versões

```bash
node --version    # v18.0.0 ou superior
pnpm --version    # 10.0.0 ou superior
git --version     # qualquer versão recente
```

## Instalação Rápida

### 1. Clone o Repositório

```bash
git clone https://github.com/seu-usuario/mug3d-clone.git
cd mug3d-clone
```

### 2. Instale Dependências

```bash
pnpm install
# ou
npm install
# ou
yarn install
```

### 3. Inicie o Servidor de Desenvolvimento

```bash
pnpm dev
```

O servidor estará disponível em `http://localhost:5173`

## Configuração Detalhada

### Variáveis de Ambiente

O projeto usa variáveis de ambiente para configuração. As principais variáveis já estão pré-configuradas pelo Manus, mas você pode customizar:

**Variáveis Disponíveis:**
- `VITE_APP_TITLE` - Título da aplicação
- `VITE_APP_LOGO` - URL do logo
- `VITE_ANALYTICS_ENDPOINT` - Endpoint de analytics
- `VITE_ANALYTICS_WEBSITE_ID` - ID do website para analytics

### Estrutura de Diretórios

```
mug3d-clone/
├── client/                 # Frontend React
│   ├── src/
│   │   ├── components/    # Componentes reutilizáveis
│   │   │   ├── MugViewer3D.tsx      # Visualizador 3D
│   │   │   ├── LayoutEditor.tsx     # Editor 2D
│   │   │   ├── ui/                  # shadcn/ui components
│   │   │   └── ErrorBoundary.tsx
│   │   ├── pages/         # Páginas da aplicação
│   │   │   ├── Home.tsx
│   │   │   └── NotFound.tsx
│   │   ├── contexts/      # React Contexts
│   │   │   └── ThemeContext.tsx
│   │   ├── hooks/         # Custom Hooks
│   │   ├── lib/           # Utilitários e helpers
│   │   ├── App.tsx        # Roteamento principal
│   │   ├── main.tsx       # Entry point
│   │   └── index.css      # Estilos globais
│   ├── public/            # Arquivos estáticos
│   ├── index.html
│   └── vite.config.ts
├── server/                # Backend (placeholder)
├── shared/                # Código compartilhado
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── README.md
├── CONTRIBUTING.md
├── LICENSE
└── .gitignore
```

## Scripts Disponíveis

### Desenvolvimento

```bash
# Iniciar servidor de desenvolvimento com hot reload
pnpm dev

# Verificar tipos TypeScript
pnpm check

# Formatar código com Prettier
pnpm format
```

### Build e Deploy

```bash
# Build para produção
pnpm build

# Preview do build de produção localmente
pnpm preview

# Build completo (frontend + backend)
pnpm build
```

## Dependências Principais

### Frontend
- **React 19** - Framework UI
- **TypeScript** - Type safety
- **Tailwind CSS 4** - Styling
- **Vite** - Build tool e dev server

### 3D e Gráficos
- **Three.js** - Renderização 3D
- **Fabric.js** - Editor de canvas 2D

### UI Components
- **shadcn/ui** - Componentes UI de alta qualidade
- **Radix UI** - Primitivos acessíveis
- **Lucide React** - Ícones

### Utilitários
- **Wouter** - Roteamento leve
- **Framer Motion** - Animações
- **Sonner** - Toasts/notificações

## Troubleshooting

### Erro: "Cannot find module 'three'"

```bash
# Reinstale dependências
pnpm install

# Limpe cache
pnpm store prune
```

### Porta 5173 já em uso

```bash
# Use uma porta diferente
pnpm dev -- --port 3001
```

### Problemas com TypeScript

```bash
# Verifique tipos
pnpm check

# Regenere tipos
pnpm check --force
```

### Modelos 3D não carregam

- Verifique conexão com internet
- Confirme que `https://mug3d.com` está acessível
- Verifique console do navegador para erros de CORS
- Use o fallback (cilindro verde) que aparece em caso de erro

## Performance

### Otimizações Implementadas

1. **Code Splitting** - Vite automaticamente faz split de código
2. **Lazy Loading** - Componentes carregados sob demanda
3. **Image Optimization** - Imagens comprimidas
4. **Tree Shaking** - Remoção de código não utilizado

### Dicas de Performance

- Use `pnpm build` para verificar tamanho final
- Monitore bundle size com `npm run build -- --analyze`
- Prefira componentes shadcn/ui para melhor performance

## Desenvolvimento

### Adic
