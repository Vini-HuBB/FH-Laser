# Arquitetura - Mug3D Clone

Documentação detalhada da arquitetura do projeto Mug3D Clone.

## Visão Geral

O projeto é uma aplicação web estática (SPA) construída com React 19 e TypeScript, especializada em visualização e edição de modelos 3D de canecas.

```
┌─────────────────────────────────────────────────────────┐
│                    Frontend (React 19)                  │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────────┐          ┌──────────────────┐    │
│  │   MugViewer3D    │          │  LayoutEditor    │    │
│  │  (Three.js)      │          │  (Fabric.js)     │    │
│  └──────────────────┘          └──────────────────┘    │
│           ▲                              ▲              │
│           │                              │              │
│  ┌────────┴──────────────────────────────┴──────────┐  │
│  │              Home Page (React)                   │  │
│  │  - State Management (useState)                   │  │
│  │  - Event Handlers                               │  │
│  │  - Control Panel                                │  │
│  └────────────────────────────────────────────────┘  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## Estrutura de Diretórios

```
client/
├── src/
│   ├── components/
│   │   ├── MugViewer3D.tsx       # Renderizador 3D com Three.js
│   │   ├── LayoutEditor.tsx      # Editor 2D com Fabric.js
│   │   ├── ErrorBoundary.tsx     # Tratamento de erros
│   │   ├── ManusDialog.tsx       # Diálogo customizado
│   │   ├── Map.tsx               # Integração Google Maps
│   │   └── ui/                   # shadcn/ui components
│   │       ├── button.tsx
│   │       ├── card.tsx
│   │       ├── checkbox.tsx
│   │       ├── input.tsx
│   │       ├── label.tsx
│   │       ├── slider.tsx
│   │       └── ... (40+ componentes)
│   ├── pages/
│   │   ├── Home.tsx              # Página principal
│   │   └── NotFound.tsx          # Página 404
│   ├── contexts/
│   │   └── ThemeContext.tsx      # Tema (light/dark)
│   ├── hooks/
│   │   └── (custom hooks aqui)
│   ├── lib/
│   │   └── (utilitários aqui)
│   ├── App.tsx                   # Router principal
│   ├── main.tsx                  # Entry point
│   └── index.css                 # Estilos globais
├── public/
│   └── favicon.ico
├── index.html
└── vite.config.ts
```

## Componentes Principais

### MugViewer3D

**Responsabilidade:** Renderizar modelo 3D da caneca com Three.js

**Props:**
```typescript
interface MugViewer3DProps {
  modelId: number;              // ID do modelo (1-13)
  backgroundColor: string;      // Cor de fundo (#RRGGBB)
  rimColor: string;            // Cor do aro
  innerColor: string;          // Cor do interior
  handleColor: string;         // Cor da alça
  animationSpeed: number;      // Velocidade (1-10)
  isAnimating: boolean;        // Ativar rotação
  isReversing: boolean;        // Reverter direção
  angle: number;               // Ângulo (0-360)
  showGrid: boolean;           // Mostrar grid
}
```

**Funcionalidades:**
- Carregamento de modelos GLTF via URL
- Fallback para cilindro 3D em caso de erro
- Controles de câmera (OrbitControls)
- Iluminação dinâmica
- Rotação automática com velocidade ajustável
- Grid opcional

**Dependências:**
- `three` - Renderização 3D
- `three/examples/jsm/controls/OrbitControls` - Controles de câmera
- `three/examples/jsm/loaders/GLTFLoader` - Carregador de modelos

### LayoutEditor

**Responsabilidade:** Editor 2D para adicionar imagens e texto

**Funcionalidades:**
- Canvas Fabric.js para edição
- Adicionar imagens
- Adicionar texto editável
- Deletar elementos
- Download como PNG
- Snapshot do modelo 3D

**Dependências:**
- `fabric` - Editor de canvas

### Home Page

**Responsabilidade:** Orquestração da aplicação

**State:**
```typescript
const [selectedModel, setSelectedModel] = useState(1);
const [backgroundColor, setBackgroundColor] = useState('#222222');
const [rimColor, setRimColor] = useState('#00FF00');
const [innerColor, setInnerColor] = useState('#FFFFFF');
const [handleColor, setHandleColor] = useState('#00FF00');
const [showRim, setShowRim] = useState(true);
const [showInner, setShowInner] = useState(true);
const [showHandle, setShowHandle] = useState(true);
const [showGrid, setShowGrid] = useState(false);
const [animationSpeed, setAnimationSpeed] = useState(4);
const [isAnimating, setIsAnimating] = useState(false);
const [isReversing, setIsReversing] = useState(false);
const [angle, setAngle] = useState(0);
const [showExtendedColors, setShowExtendedColors] = useState(false);
const [customAngle, setCustomAngle] = useState('0');
```

**Layout:**
- Header com título
- Split-screen: 65% visualizador 3D, 35% controles
- Painel de controles com seções:
  - Cores (com picker)
  - Visibilidade de componentes
  - Velocidade de animação
  - Ângulos estáticos
  - Ângulo customizado
  - Editor de layout
  - Seletor de modelos

## Fluxo de Dados

```
Home.tsx (State)
    │
    ├─→ MugViewer3D (Props)
    │   ├─→ Three.js Scene
    │   ├─→ GLTFLoader
    │   └─→ Fallback Cylinder
    │
    ├─→ LayoutEditor (Props)
    │   ├─→ Fabric.js Canvas
    │   └─→ Image/Text Management
    │
    └─→ Control Panel (UI)
        ├─→ Color Picker
        ├─→ Checkboxes
        ├─→ Sliders
        ├─→ Buttons
        └─→ Model Selector
```

## Paleta de Cores

### Design System (Tailwind CSS)

```css
/* Light Theme */
--background: oklch(1 0 0);           /* Branco */
--foreground: oklch(0.235 0.015 65);  /* Cinza escuro */
--accent: oklch(0.967 0.001 286.375); /* Azul elétrico */
--card: oklch(1 0 0);                 /* Branco */
--border: oklch(0.92 0.004 286.32);   /* Cinza claro */

/* Dark Theme */
--background: oklch(0.141 0.005 285.823);  /* Cinza muito escuro */
--foreground: oklch(0.85 0.005 65);        /* Branco */
--accent: oklch(0.967 0.001 286.375);      /* Azul elétrico */
```

### Cores de Modelos (Presets)

```
Vermelhos:    #FF0000, #FF3333
Laranja:      #FF6600
Amarelo:      #FFFF00
Verdes:       #00FF00, #00CC00
Azuis:        #0099FF, #0066FF, #0033FF
Roxo:         #9900FF
Magenta:      #FF00FF
Neutros:      #FFFFFF, #CCCCCC, #999999, #333333, #000000
```

## Modelos 3D

### Fonte de Dados

- **URL Base:** `https://mug3d.com/content/models/`
- **Formato:** GLTF (.gltf)
- **Padrão:** `{id}/model.gltf`

### Lista de Modelos

| ID | Nome | Tamanho |
|----|------|---------|
| 1 | Classic mug | 330 ml |
| 2 | Coffee cup | 170 ml |
| 3 | Big mug | 420 ml |
| 4 | Enamel cup | 330 ml |
| 5 | Travel mug | 480 ml |
| 6 | Big mug | 450 ml |
| 7 | Beer mug | 500 ml |
| 8 | Mug | 270 ml |
| 9 | Mug with a spoon | 350 ml |
| 10 | Full print mug | 330 ml |
| 11 | Heart Handle Mug | 330 ml |
| 12 | Can | 473 ml |
| 13 | Tin can | 330 ml |

## Tecnologias e Versões

### Frontend
- **React:** 19.2.1
- **TypeScript:** 5.6.3
- **Vite:** 7.1.7
- **Tailwind CSS:** 4.1.14

### 3D e Gráficos
- **Three.js:** 0.183.2
- **Fabric.js:** 7.2.0

### UI Components
- **shadcn/ui:** Latest
- **Radix UI:** Multiple packages
- **Lucide React:** 0.453.0

### Utilitários
- **Wouter:** 3.3.5 (Roteamento)
- **Framer Motion:** 12.23.22 (Animações)
- **Sonner:** 2.0.7 (Toasts)
- **React Hook Form:** 7.64.0 (Formulários)
- **Zod:** 4.1.12 (Validação)

## Performance

### Otimizações Implementadas

1. **Code Splitting**
   - Vite automaticamente faz split de código
   - Componentes lazy-loaded quando necessário

2. **Asset Optimization**
   - Imagens comprimidas
   - Modelos GLTF otimizados
   - Tree-shaking de dependências

3. **Rendering Optimization**
   - Three.js com antialias habilitado
   - Shadow mapping otimizado
   - LOD (Level of Detail) para modelos

4. **Memory Management**
   - Cleanup de event listeners
   - Dispose de geometrias e materiais
   - Garbage collection otimizado

## Tratamento de Erros

### Estratégias

1. **ErrorBoundary**
   - Captura erros em componentes React
   - Mostra fallback UI

2. **Try-Catch em Loaders**
   - Carregamento de modelos GLTF
   - Fallback para cilindro 3D

3. **Validação de Props**
   - TypeScript para type safety
   - Runtime validation com Zod (se necessário)

## Segurança

### Práticas Implementadas

1. **Content Security Policy**
   - Restringir origens de scripts
   - Prevenir XSS

2. **CORS**
   - Configuração apropriada para modelos externos
   - Fallback em caso de erro

3. **Input Validation**
   - Validação de cores
   - Validação de ângulos
   - Validação de IDs de modelos

## Escalabilidade

### Considerações para Crescimento

1. **Backend Integration**
   - Adicionar API para salvar designs
   - Autenticação de usuários
   - Persistência de dados

2. **Database**
   - Armazenar designs de usuários
   - Histórico de modificações
   - Compartilhamento de designs

3. **Real-time Collaboration**
   - WebSockets para colaboração
   - Sincronização de estado
   - Presença de usuários

4. **Advanced Features**
   - Upload de modelos customizados
   - Exportação de vídeo
   - Integração com e-commerce
   - Print-on-demand

## Deployment

### Build Process

```bash
pnpm build
# Saída: dist/
```

### Arquivos Gerados

- `dist/index.html` - HTML principal
- `dist/assets/*.js` - JavaScript bundles
- `dist/assets/*.css` - CSS bundles
- `dist/assets/*.woff2` - Fonts

### Requisitos de Servidor

- Suporte para SPA (rewrite para index.html)
- GZIP compression
- Cache headers apropriados
- HTTPS recomendado

## Monitoramento

### Métricas Importantes

1. **Performance**
   - Time to First Byte (TTFB)
   - First Contentful Paint (FCP)
   - Largest Contentful Paint (LCP)
   - Cumulative Layout Shift (CLS)

2. **Errors**
   - JavaScript errors
   - Network errors
   - CORS errors
   - Model loading failures

3. **User Behavior**
   - Page views
   - Model selections
   - Color changes
   - Downloads

## Contribuindo

Ao contribuir, mantenha:

1. **Estrutura de Componentes**
   - Um componente por arquivo
   - Props bem tipadas
   - Documentação clara

2. **Estilos**
   - Use Tailwind CSS
   - Siga convenções existentes
   - Mantenha design system

3. **Performance**
   - Evite re-renders desnecessários
   - Use useMemo/useCallback apropriadamente
   - Otimize bundle size

4. **Testes**
   - Teste componentes isoladamente
   - Teste integração
   - Teste performance

## Referências

- [React 19 Docs](https://react.dev)
- [Three.js Docs](https://threejs.org/docs)
- [Fabric.js Docs](http://fabricjs.com)
- [Tailwind CSS Docs](https://tailwindcss.com)
- [Vite Docs](https://vitejs.dev)
