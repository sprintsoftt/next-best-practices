# Patrones para Server Components y Pages en Next.js

## Principios Fundamentales

1. **Separación Server/Client:**

   - Los componentes de página (page.tsx) se mantienen como componentes del servidor
   - No usar "use client" en las páginas principales
   - Delegar la interactividad a componentes cliente específicos

2. **Estructura Recomendada:**
   - Las páginas se encargan de:
     - Obtención de datos
     - Validaciones
     - Control de acceso
     - Manejo de errores
   - Los componentes cliente manejan:
     - Interactividad
     - Estados locales
     - Eventos del usuario

## Ejemplos de Implementación

1. **Página de Listado (list/page.tsx):**

```typescript
async function ListPage() {
  // 1. Obtención de datos
  const data = await fetchData()

  // 2. Validaciones y transformaciones
  if (!data) handleError()

  // 3. Renderizado del contenedor cliente
  return <ListContainer initialData={data} />
}
```

2. **Página de Detalle (detail/[id]/page.tsx):**

```typescript
async function DetailPage({ params }) {
  // 1. Validación de parámetros
  const { id } = params

  // 2. Obtención de datos
  const item = await fetchItemById(id)

  // 3. Manejo de casos especiales
  if (!item) notFound()

  // 4. Renderizado del contenedor cliente
  return <DetailContainer item={item} />
}
```

## Beneficios

- ✅ Mejor rendimiento inicial (Server-Side Rendering)
- ✅ Clara separación de responsabilidades
- ✅ Mejor manejo de errores y estados de carga
- ✅ Optimización de recursos del cliente
- ✅ Mayor seguridad al mantener lógica sensible en el servidor

## Consideraciones

- Mantener la lógica de negocio en el servidor
- Pasar solo los datos necesarios a los componentes cliente
- Implementar manejo de errores adecuado
- Utilizar patrones de carga y estados de error consistentes

---
