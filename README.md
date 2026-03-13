# Mug3D Clone - 3D Mug Designer

Um clone fiel do site [mug3d.com](https://mug3d.com/), permitindo a personalização de canecas em 3D com um editor de layout 2D integrado.

## Características

- **Visualizador 3D Interativo**: Renderização de modelos de canecas em tempo real usando Three.js
- **13 Modelos de Canecas**: Diversos tipos e tamanhos disponíveis
- **Customização de Cores**: Controle de cores para aro, interior, alça e fundo
- **Editor de Layout 2D**: Adicione imagens e texto ao design usando Fabric.js
- **Controles de Animação**: Rotação automática com velocidade ajustável
- **Ângulos Estáticos**: Presets de ângulos (45°, 90°, 120°, 240°, 270°, 315°) ou customizado
- **Download de Designs**: Exporte o layout como PNG
- **Design Minimalista Industrial**: Interface moderna e funcional

## Design

O projeto segue uma filosofia de **Minimalismo Industrial Moderno** com:

- **Paleta de Cores**: Cinza escuro (#1a1a1a), branco (#f5f5f5), azul elétrico (#0066ff)
- **Layout Split-Screen**: 65% para visualizador 3D, 35% para controles
- **Tipografia**: Inter para body, Poppins para display
- **Hierarquia Visual**: Controles organizados em seções claramente demarcadas

## Stack Tecnológico

- **Frontend**: React 19 + TypeScript
- **Renderização 3D**: Three.js com OrbitControls e GLTFLoader
- **Editor 2D**: Fabric.js
- **Styling**: Tailwind CSS 4 + componentes customizados
- **Roteamento**: Wouter
- **Build**: Vite

## Instalação

```bash
# Instalar dependências
pnpm install

# Iniciar servidor de desenvolvimento
pnpm dev

# Build para produção
pnpm build

# Preview de produção
pnpm preview
```

## Estrutura do Projeto

```
client/
├── src/
│   ├── pages/
│   │   ├── Home.tsx          # Página principal com editor
│   │   └── NotFound.tsx      # Página 404
│   ├── components/
│   │   ├── MugViewer3D.tsx   # Visualizador 3D
│   │   └── LayoutEditor.tsx  # Editor de layout 2D
│   ├── App.tsx               # Roteamento
│   ├── main.tsx              # Entry point
│   └── index.css             # Estilos globais
├── public/
│   └── favicon.ico
└── index.html
```

## Componentes Principais

### MugViewer3D
Renderiza o modelo 3D da caneca com suporte para:
- Carregamento de modelos GLTF
- Iluminação dinâmica
- Controles de câmera (OrbitControls)
- Rotação automática
- Grid opcional

**Props**:
- `modelId`: ID do modelo a renderizar
- `backgroundColor`: Cor de fundo da cena
- `rimColor`: Cor do aro
- `innerColor`: Cor do interior
- `handleColor`: Cor da alça
- `animationSpeed`: Velocidade de rotação (1-10)
- `isAnimating`: Ativar rotação automática
- `isReversing`: Reverter direção de rotação
- `angle`: Ângulo de rotação (0-360)
- `showGrid`: Mostrar grid

### LayoutEditor
Editor de canvas 2D para adicionar imagens e texto ao design.

**Funcionalidades**:
- Adicionar imagens
- Adicionar texto editável
- Deletar elementos selecionados
- Download do layout como PNG
- Snapshot do modelo 3D

## Modelos Disponíveis

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

## Paleta de Cores Pré-definidas

- Vermelho: #FF0000
- Laranja: #FF6600
- Amarelo: #FFFF00
- Verde: #00FF00
- Azul Ciano: #0099FF
- Azul: #0066FF
- Roxo: #9900FF
- Magenta: #FF00FF
- Branco: #FFFFFF
- Cinza Claro: #CCCCCC
- Cinza: #999999
- Cinza Escuro: #333333
- Preto: #000000

## Recursos Externos

- Modelos 3D: `https://mug3d.com/content/models/{id}/model.gltf`
- Previews: `https://mug3d.com/content/models/{id}/preview.webp`
- Ambiente: `https://mug3d.com/content/img/env/`

## Desenvolvimento

### Adicionar Novo Modelo

1. Obter ID do modelo
2. Adicionar à lista `MUG_MODELS` em `Home.tsx`
3. O modelo será automaticamente carregado

### Customizar Cores

Editar `client/src/index.css`:
- `:root`: Cores padrão (tema claro)
- `.dark`: Cores do tema escuro

### Melhorar Visualizador 3D

Editar `client/src/components/MugViewer3D.tsx`:
- Iluminação: Ajustar intensidade em `AmbientLight` e `DirectionalLight`
- Câmera: Modificar posição e zoom
- Materiais: Adicionar propriedades de material customizadas

## Limitações Conhecidas

- Colorização de materiais simplificada (requer mapping de materiais específicos)
- Editor 2D básico (sem suporte a camadas ou efeitos avançados)
- Modelos carregados de URL externa (depende de disponibilidade)

## Próximos Passos

- [ ] Implementar colorização completa de materiais
- [ ] Adicionar suporte a upload de imagens customizadas
- [ ] Melhorar editor 2D com mais funcionalidades
- [ ] Adicionar suporte a exportação de vídeo
- [ ] Implementar sistema de salvamento de designs
- [ ] Adicionar suporte a múltiplos idiomas

## Licença

MIT

## Créditos

Baseado em [mug3d.com](https://mug3d.com/) - 3D Mug Mockup Designer
