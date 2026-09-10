# ADR-0001: Usar React + TypeScript con TanStack Query, Zustand y Tailwind para el frontend
<!-- docs/adr/0001-usar-react-typescript-tanstack-query-zustand-tailwind.md -->

## Autores:

- Justin David Vargas Vasquez
- Cristian Andrés Díaz Ortega

## Contexto
La plataforma debe permitir a los usuarios descubrir, filtrar y reservar actividades personalizadas según tiempo, ubicación, intereses y disponibilidad. El flujo incluye formularios complejos
(fechas, horarios, número de personas, preferencias), listados dinámicos de actividades y estados transaccionales (disponibilidad, confirmación, pago). El equipo no conoce la mayoría de las
tecnologías del stack, por lo que la curva de aprendizaje es una fuerza restrictiva. Adicionalmente, el producto está en fase de definición, lo que exige velocidad de iteración y bajo costo de
pivote. React es un requisito explícito del proyecto.

## Decisión
Vamos a construir el frontend con React 19 + TypeScript + Vite, apoyándonos en TanStack Query para estado remoto y caché, Zustand para estado global ligero, React Hook Form + Zod para formularios
y validación, y Tailwind CSS para estilos.

## Alternativas consideradas

- Next.js (React + SSR/SSG): Se descarta por ahora. Ofrece mejor SEO y renderizado del servidor, deseable para descubrimiento orgánico de actividades, pero añade complejidad (rutas, servidor, despliegue)
que el equipo no está preparado para absorber en el MVP. La migración futura es viable porque el núcleo React se mantiene.

- Vue.js / Nuxt: Curva de aprendizaje comparable a React, pero el equipo ya tiene React como requisito explícito y la demanda de mercado de React es mayor.

- Angular: Mayor estructura, pero curva de aprendizaje pronunciada y más verboso; no se alinea con la velocidad requerida para el MVP.

- Redux Toolkit en lugar de Zustand: Más estructurado pero con mayor boilerplate; se descarta por costo de aprendizaje frente al beneficio en un MVP.

- CSS Modules / styled-components en lugar de Tailwind: Se descartan por velocidad de iteración; Tailwind reduce el cambio de contexto entre HTML y CSS.

## Consecuencias

### Positivas:

- Un solo lenguaje (TypeScript) en frontend y backend, reduciendo la carga cognitiva del equipo.

- TanStack Query resuelve caché, reintentos, invalidación y estados de carga del servidor sin necesidad de código manual.

- Los esquemas Zod pueden compartirse con el backend (NestJS) para validación consistente.

- Vite acelera el ciclo de desarrollo con HMR casi instantáneo.

### Negativas / costos aceptados:

- Pérdida de SEO: sin SSR, las páginas de actividades no se renderizan en el servidor. Se acepta como deuda consciente; si el SEO orgánico se vuelve crítico, se evaluará migrar a Next.js.

- Fragmentación del ecosistema: el equipo debe aprender React + TanStack Query + Zustand + RHF + Zod + Tailwind (6 piezas). Riesgo de inconsistencia si no se establecen convenciones desde el inicio.

- Tailwind: HTML denso y dependencia de disciplina para mantener un sistema de diseño coherente.
