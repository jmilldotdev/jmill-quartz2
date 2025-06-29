# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Quartz v4 is a static site generator designed for publishing digital gardens and notes as websites. It transforms Markdown content into a fully-featured website with search, graph visualization, and wiki-style linking.

**Documentation**: For detailed framework documentation and specific questions, refer to https://quartz.jzhao.xyz/

## Development Commands

### Essential Commands
- `npm install` - Install dependencies (requires Node.js >= 22, npm >= 10.9.2)
- `npx quartz build --serve --watch` - Start development server with hot reload on port 8080
- `npm run check` - Run TypeScript type checking and Prettier format check
- `npm run format` - Auto-format code with Prettier
- `npm test` - Run test suite using Node.js built-in test runner

### Build Commands
- `npx quartz build` - Build static site (input: content/, output: public/)
- `npx quartz build --bundleInfo` - Build with bundle size information
- `npx quartz build --concurrency=N` - Control parsing thread count

### Other CLI Commands
- `npx quartz sync` - Sync content with GitHub
- `npx quartz update` - Update Quartz to latest version
- `npx quartz create` - Initialize new Quartz project

## Architecture Overview

### Plugin System
Quartz uses a three-phase plugin architecture:

1. **Transformers** (`quartz/plugins/transformers/`) - Process markdown content during build
2. **Filters** (`quartz/plugins/filters/`) - Determine which content to publish
3. **Emitters** (`quartz/plugins/emitters/`) - Generate output files (HTML, RSS, etc.)

Plugins are configured in `quartz.config.ts`.

### Component System
- Components are in `quartz/components/` using Preact
- Each component can bundle CSS and JavaScript
- Components receive `QuartzComponentProps` with file data and build context
- Factory pattern for configurable components

### Content Processing Pipeline
1. Raw markdown files from `content/` directory
2. Parsed to AST using remark/rehype (unified ecosystem)
3. Transformed by plugins
4. Emitted as static HTML to `public/` directory

Processing uses worker pools for parallelization with chunking for optimal performance.

### Key Configuration Files
- `quartz.config.ts` - Main site configuration (plugins, theme, analytics)
- `quartz.layout.ts` - Page layout structure
- `tsconfig.json` - TypeScript configuration with Preact JSX

### SPA Router
Quartz includes a lightweight SPA router (`quartz/components/scripts/spa.inline.ts`) that:
- Uses morphing for smooth transitions
- Preserves elements marked with `spa-preserve`
- Manages component cleanup functions
- Falls back gracefully without JavaScript

### File Structure
```
quartz/
├── components/     # UI components (Preact)
│   ├── scripts/   # Client-side JavaScript
│   └── styles/    # Component SCSS files
├── plugins/       # Transform/filter/emit plugins
├── processors/    # Core content processing
├── util/         # Shared utilities
├── i18n/         # Internationalization (30+ languages)
└── static/       # Static assets
```

## Development Guidelines

### Adding New Components
1. Create component in `quartz/components/`
2. Export factory function returning `QuartzComponent`
3. Include CSS via `css` property and scripts via `beforeDOMLoaded`/`afterDOMLoaded`
4. Add to layout configuration in `quartz.layout.ts`

### Creating Plugins
1. Implement appropriate interface: `QuartzTransformerPlugin`, `QuartzFilterPlugin`, or `QuartzEmitterPlugin`
2. Place in corresponding directory under `quartz/plugins/`
3. Add to plugin configuration in `quartz.config.ts`

### Working with Styles
- SCSS files in `quartz/components/styles/`
- Use CSS variables for theming (see `quartz/util/theme.ts`)
- Styles are processed with LightningCSS

### Testing
- Tests use Node.js built-in test runner
- Test files follow `*.test.ts` pattern
- Run specific test: `npx tsx path/to/file.test.ts`

### Type Safety
- Strict TypeScript configuration
- Key types: `QuartzConfig`, `ProcessedContent`, `QuartzComponent`
- Build context available via `BuildCtx` type

## Important Notes

- The build system uses ESBuild for fast compilation
- Incremental builds supported in watch mode
- Worker pool architecture for parallel markdown processing
- All paths in build context are POSIX-style (forward slashes)
- Component scripts can use `document.addEventListener("nav", ...)` for SPA navigation events