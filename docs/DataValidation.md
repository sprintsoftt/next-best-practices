# Validación y Seguridad de Datos

## Principios Fundamentales

1. **Single Source of Truth (SoT)**

   - Mantener esquemas de validación centralizados
   - Reutilizar los mismos esquemas tanto en cliente como servidor
   - Definir tipos TypeScript a partir de los esquemas

2. **Puntos de Validación Críticos**
   - Entrada de datos del cliente (forms)
   - Endpoints de API
   - Antes de almacenar en base de datos
   - Al recibir datos de APIs externas

## Implementación con Zod

### 1. Definición de Esquemas

```typescript
import { z } from "zod";

// Esquema base que puede ser reutilizado
export const userSchema = z.object({
  email: z.string().email("Correo electrónico inválido").toLowerCase(), // Sanitización
  name: z.string().min(2, "Nombre muy corto").trim(), // Sanitización
  age: z.number().min(18, "Debe ser mayor de edad").int(), // Sanitización
});
```

### 2. Validación en API Routes

```typescript
async function POST(req: Request) {
  try {
    // Validación y sanitización en un solo paso
    const data = userSchema.parse(await req.json());

    // Continuar con la lógica de negocio
    await saveToDatabase(data);

    return Response.json({ success: true });
  } catch (error) {
    if (error instanceof z.ZodError) {
      return Response.json({ errors: error.errors }, { status: 400 });
    }
  }
}
```

## Sanitización de Datos

### 1. Datos de Texto

- Eliminar espacios innecesarios
- Normalizar formatos (emails en minúsculas)
- Escapar caracteres especiales
- Remover HTML/scripts maliciosos

### 2. Datos Numéricos

- Convertir strings a números
- Redondear cuando sea necesario
- Establecer límites mínimos/máximos

### 3. Fechas

- Normalizar formatos
- Validar rangos válidos
- Convertir a UTC cuando sea necesario

## Mejores Prácticas

1. **Validación en Capas**

   - Frontend: Mejor experiencia de usuario
   - API: Seguridad y consistencia
   - Base de datos: Última línea de defensa

2. **Manejo de Errores**

   - Mensajes de error claros y útiles
   - Respuestas de error estructuradas
   - Logging apropiado de errores de validación

3. **Seguridad**
   - Prevención de inyección SQL
   - Validación contra XSS
   - Límites en tamaños de datos
   - Validación de tipos MIME para archivos

## Ejemplo Completo

```typescript
// Esquema con sanitización
const contactFormSchema = z.object({
  email: z.string().email().toLowerCase().trim(),
  message: z
    .string()
    .min(10)
    .max(1000)
    .transform((str) => sanitizeHtml(str)), // Sanitización de HTML
  attachments: z
    .array(
      z.object({
        type: z
          .string()
          .refine((type) => ["image/jpeg", "image/png"].includes(type)),
        size: z.number().max(5 * 1024 * 1024), // 5MB máx
      })
    )
    .optional(),
});
```

La validación y sanitización son cruciales para:

- ✅ Seguridad de la aplicación
- ✅ Integridad de datos
- ✅ Experiencia de usuario
- ✅ Mantenibilidad del código
