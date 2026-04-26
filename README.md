[README.md](https://github.com/user-attachments/files/27106342/README.md)
# 🌎 OrigenIA — Plataforma de Exportación Inteligente para MIPYMES

**OrigenIA** es una plataforma web impulsada por inteligencia artificial que ayuda a las micro, pequeñas y medianas empresas (MIPYMES) de Santander, Colombia, a prepararse para exportar sus productos al mercado internacional. En 5 minutos y sin registro previo, cualquier comerciante puede obtener un diagnóstico completo de su potencial exportador, un perfil multilingüe B2B, trazabilidad QR por lote y toda la documentación necesaria según el país de destino.

> **Hackathon Prototype** — Este proyecto fue desarrollado como prototipo funcional. Integra la API de Anthropic (Claude Sonnet 4) directamente desde el frontend para generar análisis, perfiles y documentación en tiempo real.

---

## Problema que Resuelve

Las MIPYMES de Santander producen cacao fino de aroma, joyería artesanal, calzado de cuero y otros productos con alta demanda internacional, pero enfrentan barreras críticas para exportar: desconocimiento de requisitos documentales, falta de perfiles comerciales en otros idiomas, ausencia de trazabilidad verificable y dificultad para identificar mercados potenciales. OrigenIA elimina esas barreras con un flujo guiado por IA que automatiza todo el proceso.

---

## Funcionalidades Principales

### Para Comerciantes (Exportadores)

**Score Exportador IA (0–100):** La empresa completa un formulario con datos básicos (sector, producto, municipio, certificaciones, experiencia) y la IA calcula un puntaje de preparación exportadora con desglose por dimensiones — producto, documentación, mercado y capacidad — más fortalezas, brechas y un plan de acción personalizado.

**Perfil Exportador Multilingüe:** Genera automáticamente una ficha técnica comercial en español, inglés y alemán lista para compartir con compradores B2B internacionales. Incluye descripción del producto, especificaciones técnicas, historia del productor y datos de disponibilidad.

**Trazabilidad QR por Lote:** Registra datos de cada lote de producción (fecha, peso, proceso, clasificación de calidad) y genera un código QR único y escaneable. El comprador internacional puede verificar origen, proceso y calidad antes de confirmar la compra.

**Documentación Automática por País:** Al seleccionar un país de destino (Alemania, Estados Unidos, Francia, Japón, entre otros), la IA genera la lista completa de documentos requeridos (certificado de origen, factura pro forma, certificado fitosanitario, etc.), identifica la entidad emisora en Colombia, detalla requisitos específicos del mercado destino y estima tiempos de gestión.

**Match de Mercados:** Análisis comparativo de países compradores con indicadores de demanda, tendencia de precios, precio estimado por unidad y notas clave por mercado para que el exportador tome decisiones informadas.

### Para Compradores Internacionales

**Dashboard del comprador** con catálogo de productos colombianos disponibles, sistema de cotizaciones, gestión de pedidos, mensajería directa con productores y perfiles verificados con trazabilidad QR.

---

## Stack Tecnológico

| Capa | Tecnología |
|---|---|
| Framework | Next.js 16 (App Router) |
| Lenguaje | TypeScript / React 19 |
| Estilos | Tailwind CSS 4 |
| Componentes UI | shadcn/ui + Radix UI |
| Gráficos | Recharts |
| IA | Anthropic Claude Sonnet 4 (API REST) |
| QR | API externa (api.qrserver.com) |
| Package Manager | pnpm |

---

## Estructura del Proyecto

```
├── app/
│   ├── bienvenida/        # Pantalla de bienvenida con animación de carga
│   ├── login/             # Inicio de sesión (comerciante o comprador)
│   ├── registro/          # Registro de nuevos usuarios
│   ├── dashboard/         # Flujo principal del comerciante (5 pasos con IA)
│   ├── buyer/             # Portal del comprador internacional
│   │   ├── auth/          # Autenticación del comprador
│   │   ├── catalog/       # Catálogo de productos colombianos
│   │   ├── dashboard/     # Panel principal del comprador
│   │   ├── messages/      # Mensajería con productores
│   │   ├── orders/        # Gestión de pedidos
│   │   ├── product/[id]/  # Detalle de producto
│   │   ├── profile/       # Perfil del comprador
│   │   └── quotes/        # Cotizaciones
│   ├── layout.tsx         # Layout raíz con providers de tema
│   ├── globals.css        # Estilos globales
│   └── page.tsx           # Página raíz (redirige a /bienvenida)
├── components/
│   ├── buyer/             # Layout y componentes del comprador
│   ├── dashboard/         # Módulos del dashboard (score, catálogo, docs, QR)
│   ├── ui/                # Componentes shadcn/ui (button, card, dialog, etc.)
│   ├── role-selector.tsx  # Selector de rol (comerciante / comprador)
│   └── theme-provider.tsx # Provider de temas (claro/oscuro)
├── hooks/                 # Custom hooks (use-mobile, use-toast)
├── lib/
│   ├── origen-ia.ts       # Lógica core con integración de Claude AI
│   └── utils.ts           # Utilidades (cn, merge de clases)
└── public/                # Assets estáticos (iconos, placeholders)
```

---

## Flujo de la Aplicación

```
Bienvenida → Registro/Login → Seleccionar rol
                                    │
                    ┌───────────────┴───────────────┐
                    ▼                               ▼
             COMERCIANTE                       COMPRADOR
          (Flujo 5 pasos)                   (Portal B2B)
                    │                               │
        1. Datos de empresa              Dashboard con catálogo
        2. Score IA (0-100)              Cotizaciones y pedidos
        3. Perfil multilingüe            Mensajería con productores
        4. Trazabilidad QR               Verificación de origen QR
        5. Docs + Match mercados
```

---

## Instalación y Ejecución

**Requisitos previos:** Node.js 18+ y pnpm instalado.

```bash
# Clonar el repositorio
git clone https://github.com/tu-usuario/origen-ia.git
cd origen-ia

# Instalar dependencias
pnpm install

# Ejecutar en modo desarrollo
pnpm dev
```

La aplicación estará disponible en `http://localhost:3000`.

### Nota sobre la API de IA

Este prototipo consume la API de Anthropic directamente desde el cliente. En un entorno de producción se recomienda mover las llamadas a un endpoint de backend (API route de Next.js o servidor independiente) para proteger las credenciales y controlar el uso.

---

## Sectores Soportados

El prototipo se enfoca en los sectores productivos clave de Santander: cacao fino de aroma, joyería artesanal, calzado, manufactura y cítricos. Los municipios cubiertos incluyen Bucaramanga, San Vicente de Chucurí, El Carmen de Chucurí, Landázuri, Lebrija, Girón, Piedecuesta y Barrancabermeja.

Los mercados de destino disponibles para análisis son Alemania, Estados Unidos, Francia, Países Bajos, Japón, Reino Unido, España, Canadá, Italia y Bélgica.

---

## Roadmap

- Autenticación real con Supabase o Auth.js
- Mover las llamadas a la API de Claude al backend (API routes)
- Persistencia de datos (base de datos para perfiles, lotes y documentos)
- Generación y descarga de documentos en PDF
- Integración con ProColombia para datos de mercado actualizados
- Notificaciones en tiempo real entre compradores y vendedores
- App móvil para escaneo QR en campo

---

## Equipo

Desarrollado durante hackathon como prototipo funcional para demostrar cómo la IA puede democratizar el acceso a la exportación para las MIPYMES colombianas.

---

## Licencia

MIT

---

<p align="center">
  <strong>Hecho en Colombia 🇨🇴 · Exportado al mundo</strong>
</p>
