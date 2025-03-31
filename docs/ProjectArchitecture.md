# Arquitectura del Proyecto Next.js

Esta estructura de carpetas está diseñada para mantener una organización clara y escalable en proyectos Next.js, siguiendo las mejores prácticas de desarrollo y el patrón de diseño modular.

## Descripción General

La estructura se organiza principalmente en las siguientes secciones:

### Carpeta Principal (`app/`)

- Utiliza el App Router de Next.js
- Organiza las características (features) en grupos lógicos
- Cada feature mantiene su propia estructura modular con componentes, hooks y utilidades específicas

### Características (Features)

Cada feature dentro de `(dashboard)/` contiene:

- `components/`: Componentes específicos del feature
- `hooks/`: Hooks personalizados para el feature
- `lib/`: Funciones utilitarias sin estado
- `types/`: Definiciones de tipos específicos
- `styles/`: Estilos específicos del feature
- `constants.ts`: Configuraciones y constantes

### Carpetas Globales

- `assets/`: Recursos estáticos (imágenes, fuentes)
- `components/`: Componentes reutilizables a nivel global
- `db/`: Conexiones y consultas a base de datos
- `i18n/`: Configuración de internacionalización
- `lib/`: Utilidades compartidas por toda la aplicación
- `public/`: Archivos públicos accesibles directamente
- `styles/`: Estilos globales
- `types/`: Tipos de datos globales
- `constants.tsx`: Constantes y configuraciones globales

Esta estructura facilita:

- La escalabilidad del proyecto
- La separación de responsabilidades
- La reutilización de código
- El mantenimiento a largo plazo
- La organización modular de características

├── app/ # Folder of routes (Next.js App Router)
│ ├── (dashboard)/ # Group of routes of the dashboard
│ │ ├── Feature1/ # Feature 1
│ │ │ ├── components/ # Components specific for the feature
│ │ │ ├── hooks/ # Hooks locales or specific for the feature
│ │ │ ├── lib/ # Functions that dont need a react state for the feature
│ │ │ ├── types/ # Types of data for the feature
│ │ │ ├── styles/ # Styles for the feature
│ │ │ └── constants.ts # Constants and configurations for the feature
│ │ ├── Feature2/ # Feature 2
│ │ ├── Feature3/ # Feature 3
│ │ ├── ... / # Other feature
├─ assets/ # Static resources (images, fonts, etc.)
├─ components/ # Reusable components globally
├─ db/ # Database connection and queries
├─ i18n/ # Internationalization Translation rules (i18n)
├─ lib/ # Functions or utilities shared by the app
├─ public/ # Public files (favicon, robots.txt, etc.)
├─ styles/ # Global styles (CSS, SCSS, etc.)
├─ types/ # Types of data for the app
└─ constants.tsx # Global constants (configurations, fixed values, etc.)
