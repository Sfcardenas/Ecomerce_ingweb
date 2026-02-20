# Registro de Decisiones de Diseño (ADR) - eCommerce Accesible v2.0
**Estado:** Aprobado para Desarrollo  
**Referencia:** WCAG 2.2 Nivel AA / Métrica Pro Standard

---

## 1. Navegación Estructural y Global

### 1.1 Enlace de Salto (Skip to Content)
- **Decisión:** Implementar un enlace de salto nativo como el primer elemento focalizable del DOM.
- **Justificación:** Cumplimiento del criterio **WCAG 2.4.1 (Avoid Blocks)**. Permite a usuarios de teclado o *switch access* omitir la navegación repetitiva.
- **Especificación Técnica:** - Visible solo en `:focus`.
  - Destino: `<main id="main-content" tabindex="-1">`.
- **Cualidad:** Eficiencia de uso y reducción de fatiga motriz.

### 1.2 Migas de Pan (Breadcrumbs)
- **Decisión:** Navegación jerárquica con marcado semántico `<nav aria-label="Breadcrumb">`.
- **Justificación:** Criterio **2.4.8 (Location)**. Crucial para usuarios con desorientación espacial o cognitiva (TDAH).
- **Especificación Técnica:** - Uso de `aria-current="page"` en el último elemento.
  - Separadores visuales ignorados por lectores de pantalla (vía CSS o `aria-hidden="true"`).

---

## 2. Experiencia de Búsqueda Dinámica

### 2.1 Buscador con Anuncios de Estado
- **Decisión:** Integrar una región `aria-live="polite"` para feedback de resultados.
- **Justificación:** Principio de **Comprensibilidad**. Los usuarios con discapacidad visual deben conocer el éxito o fallo de la búsqueda sin mover el foco.
- **Patrón:** *Search Auto-complete*.
- **Comportamiento:** Al escribir, el sistema anuncia: *"Cargando resultados..."* y posteriormente *"8 productos encontrados"*.

---

## 3. Grilla de Productos (PLP)

### 3.1 Anatomía de la Tarjeta (Product Card)
- **Decisión:** Definir un área de interacción mínima (**Target Size**) de **44x44px**.
- **Justificación:** Criterio **2.5.8 (Target Size - Minimum)** de WCAG 2.2. Previene errores de pulsación en usuarios con temblores (Parkinson) o movilidad reducida.
- **Especificación Técnica:** - Uso de `aria-labelledby` para asociar la imagen con el título del producto.
  - Botones de "Favoritos" y "Carrito" con `aria-label` descriptivos (ej. *"Añadir [Nombre Producto] al carrito"*).

### 3.2 Adaptabilidad y Reflujo (Reflow)
- **Decisión:** Implementar Grid adaptable sin pérdida de información hasta un **400% de zoom**.
- **Justificación:** Criterio **1.4.10 (Reflow)**. Asegura que el contenido no requiera scroll horizontal en dispositivos móviles o configuraciones de baja visión.

---

## 4. Ayudas de Accesibilidad (A11y Toolbar)

### 4.1 Panel de Preferencias de Usuario
- **Decisión:** Inclusión de un widget de ajustes rápidos para la interfaz.
- **Justificación:** **Perceptibilidad personalizada**. Mejora la experiencia para usuarios con dislexia, fotosensibilidad o visión baja.
- **Funcionalidades:**
  * **Alto Contraste:** Ratio mínimo de contraste 7:1.
  * **Tipografía Legible:** Opción de fuente *Sans-Serif* con interlineado aumentado.
  * **Reducción de Movimiento:** Respetar `prefers-reduced-motion` para detener banners animados.

---

## Resumen de Impacto y Cumplimiento

| Componente | Criterio WCAG | Prioridad | Beneficiario |
| :--- | :--- | :--- | :--- |
| **Skip Links** | 2.1.1 (Teclado) | Crítica | Discapacidad motriz |
| **Buscador** | 4.1.3 (Status) | Alta | Usuarios de Screen Reader |
| **Breadcrumbs** | 2.4.8 (Ubicación) | Media | Discapacidad cognitiva |
| **Grilla** | 2.5.8 (Target Size) | Alta | Usuarios de dispositivos móviles |

---
