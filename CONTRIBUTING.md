# Contribuindo para Mug3D Clone

Obrigado por seu interesse em contribuir para o projeto Mug3D Clone! Este documento fornece diretrizes e instruções para contribuir.

## Como Contribuir

### 1. Fork e Clone
```bash
git clone https://github.com/seu-usuario/mug3d-clone.git
cd mug3d-clone
```

### 2. Crie uma Branch
```bash
git checkout -b feature/sua-feature
# ou
git checkout -b fix/seu-fix
```

### 3. Instale Dependências
```bash
pnpm install
```

### 4. Desenvolva
- Faça suas alterações
- Teste localmente com `pnpm dev`
- Siga o estilo de código existente

### 5. Commit e Push
```bash
git add .
git commit -m "feat: descrição clara da mudança"
git push origin feature/sua-feature
```

### 6. Abra um Pull Request
- Descreva as mudanças claramente
- Referencie issues relacionadas
- Aguarde revisão

## Padrões de Código

### Commits
Use o formato Conventional Commits:
- `feat:` para novas funcionalidades
- `fix:` para correções de bugs
- `docs:` para documentação
- `style:` para formatação
- `refactor:` para refatoração
- `test:` para testes
- `chore:` para tarefas de manutenção

### TypeScript
- Use tipos explícitos
- Evite `any`
- Mantenha componentes bem tipados

### React
- Use hooks modernos
- Componentes funcionais
- Prop drilling mínimo
- Memoização quando apropriado

### Styling
- Use Tailwind CSS
- Siga as convenções de classe existentes
- Mantenha consistência com o design system

## Relatando Bugs

Ao reportar bugs, inclua:
- Descrição clara do problema
- Passos para reproduzir
- Comportamento esperado
- Comportamento atual
- Screenshots/videos se aplicável
- Ambiente (navegador, SO, versão)

## Sugestões de Melhorias

Para sugerir melhorias:
- Descreva o caso de uso
- Explique o benefício
- Sugira uma implementação possível
- Considere impacto no desempenho

## Estrutura do Projeto

```
mug3d-clone/
├── client/
│   ├── src/
│   │   ├── components/     # Componentes React
│   │   ├── pages/          # Páginas
│   │   ├── contexts/       # Contextos React
│   │   ├── hooks/          # Custom hooks
│   │   ├── lib/            # Utilitários
│   │   ├── App.tsx         # Roteamento
│   │   ├── main.tsx        # Entry point
│   │   └── index.css       # Estilos globais
│   ├── public/             # Arquivos estáticos
│   └── index.html
├── server/                 # Backend (placeholder)
├── shared/                 # Código compartilhado
├── package.json
└── README.md
```

## Desenvolvimento Local

### Iniciar servidor de desenvolvimento
```bash
pnpm dev
```

### Build para produção
```bash
pnpm build
```

### Preview de produção
```bash
pnpm preview
```

### Verificar tipos
```bash
pnpm check
```

### Formatar código
```bash
pnpm format
```

## Tecnologias Principais

- **React 19** - Framework UI
- **TypeScript** - Type safety
- **Three.js** - Renderização 3D
- **Fabric.js** - Editor 2D
- **Tailwind CSS 4** - Styling
- **Vite** - Build tool
- **Wouter** - Roteamento

## Código de Conduta

Esperamos que todos os contribuidores:
- Sejam respeitosos e inclusivos
- Aceitem críticas construtivas
- Focarem no que é melhor para a comunidade
- Respeitem as diferenças de opinião

## Dúvidas?

- Abra uma issue para discussão
- Consulte a documentação existente
- Verifique issues fechadas para soluções anteriores

Obrigado por contribuir! 🎉
