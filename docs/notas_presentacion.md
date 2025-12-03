# DriveSkore - Presentación TFM
## Trabajo Fin de Máster - Máster en Informática
### Universidad de Huelva

---

## SLIDE 1: APERTURA - EL PROBLEMA
### Título: "1.3 Millones de Razones"

**Visual:** Imagen impactante de carretera con overlay de estadísticas

**Texto principal:**
> Cada año, 1.3 millones de personas mueren en accidentes de tráfico.
> 
> 50 millones más resultan heridas.
>
> ¿Cómo sabemos si conducimos bien?

**Transición (Gamaliel habla):**
"La mayoría de conductores creen que conducen por encima de la media. Es estadísticamente imposible. No tenemos feedback objetivo sobre nuestra conducción hasta que... es demasiado tarde."

---

## SLIDE 2: LA SOLUCIÓN - DRIVESKORE
### Título: "Evaluación Universal de Conducción"

**Visual:** Logo DriveSkore + mockup de la app en ambas plataformas

**Tres pilares visuales:**

```
🎯 MISIÓN
Ayudar a millones de personas 
a conducir mejor

🎨 FILOSOFÍA  
Simplicidad que no interfiere
con la seguridad

🌍 ALCANCE
Producto real, listo para
impactar globalmente
```

**Texto de apoyo:**
"DriveSkore democratiza la evaluación de conducción. Lo que antes solo estaba disponible para profesionales, ahora en el bolsillo de cualquier conductor."

---

## SLIDE 3: DEMO - PREPARACIÓN
### Título: "Tan Simple Como..."

**Visual:** Captura de pantalla de la pantalla de inicio

**Flujo visual (3 pasos):**

```
1. Abrir app          →  2. Pulsar "Iniciar"  →  3. Conducir
   [Icono app]            [Botón grande]          [Icono coche]
```

**Mensaje clave (en pantalla):**
> "Un solo botón entre tú y una conducción más segura"

**Gamaliel dice:**
"Permítanme mostrarles cómo funciona en tiempo real..."

---

## SLIDE 4: DEMO - EN ACCIÓN
### (Pantalla para compartir móvil - DEMO EN VIVO)

**Si falla, tener video backup de:**
1. Inicio de sesión (5 seg)
2. Selección de ruta (5 seg)
3. Conducción con datos en tiempo real (30 seg)
4. Finalización y resultados (20 seg)

**Narración durante demo:**
- "La app monitoriza aceleración, frenado, giros..."
- "Todo en segundo plano, sin distraer al conductor"
- "Al finalizar, análisis completo con áreas de mejora"

**Transición:**
"Esto es lo que ve el usuario. Ahora veamos qué hay detrás."

---

## SLIDE 5: METODOLOGÍA - DESARROLLO REAL
### Título: "De la Teoría a la Carretera"

**Visual:** Timeline horizontal con hitos

**Contenido:**

### Enfoque Ágil + Testeo Real

**Fase 1: Investigación** (2 semanas)
- Análisis de apps existentes
- Identificación de pain points
- Definición de arquitectura

**Fase 2: MVP** (3 semanas)
- Desarrollo core Android
- Algoritmos de evaluación
- Primera versión funcional

**Fase 3: Testing Campus UHU** (4 semanas)
- 15+ usuarios reales
- Rutas diarias reales
- Feedback continuo e iteración

**Fase 4: Expansión iOS + Producción** (3 semanas)
- Desarrollo iOS nativo
- Infraestructura escalable
- Landing page + analytics

**Mensaje clave:**
> "No es un prototipo académico. Son 12 semanas de ingeniería con usuarios reales en condiciones reales."

---

## SLIDE 6: ARQUITECTURA TÉCNICA
### Título: "Infraestructura Production-Ready"

**Visual:** Diagrama de arquitectura limpio

```
┌─────────────────────────────────────────┐
│         FRONTEND MULTIPLATAFORMA        │
├─────────────────────────────────────────┤
│  React Native + Expo                    │
│  ├── iOS (Swift interop)                │
│  │   ├── Widgets interactivos           │
│  │   └── Siri Shortcuts                 │
│  └── Android (Kotlin interop)           │
│      └── Floating overlay               │
└─────────────────────────────────────────┘
              ↕ REST API
┌─────────────────────────────────────────┐
│         BACKEND SERVERLESS              │
├─────────────────────────────────────────┤
│  Vercel Edge Functions                  │
│  └── Deploy automático desde GitHub     │
│                                          │
│  Supabase                                │
│  ├── PostgreSQL (datos conducción)      │
│  ├── Auth (seguridad)                   │
│  └── Real-time subscriptions            │
└─────────────────────────────────────────┘
              ↕
┌─────────────────────────────────────────┐
│         OBSERVABILIDAD                  │
├─────────────────────────────────────────┤
│  Firebase Analytics                     │
│  └── Métricas de uso en tiempo real     │
└─────────────────────────────────────────┘
```

**Puntos clave (Gamaliel explica):**
1. **Escalabilidad**: Serverless → costes marginales bajos, escala automática
2. **Desarrollo moderno**: Stack probado en producción por miles de apps
3. **Open Source**: Basado en herramientas de código abierto (guiño a Iñaki)

---

## SLIDE 7: UNIVERSALIDAD REAL
### Título: "Dos Plataformas, Una Visión"

**Visual:** Comparativa lado a lado iOS vs Android

```
╔══════════════════════════════════════════════════════╗
║              iOS                  Android            ║
╠══════════════════════════════════════════════════════╣
║  Widget Interactivo     |    Floating Overlay       ║
║  (Pantalla de bloqueo)  |    (Sobre otras apps)     ║
║                         |                            ║
║  Siri Shortcuts         |    Quick Settings Tile    ║
║  "Hey Siri, empieza     |    Acceso rápido          ║
║   DriveSkore"           |    desde panel            ║
║                         |                            ║
║  Live Activities        |    Persistent             ║
║  (Dynamic Island)       |    Notification           ║
╚══════════════════════════════════════════════════════╝
```

**Mensaje clave:**
> "No es un 'port'. Es adaptación inteligente a los paradigmas nativos de cada plataforma."

**Gamaliel explica:**
"iOS no permite overlays por seguridad → widgets interactivos
Android lo permite → aprovechamos floating overlay
Mismo objetivo, implementación específica óptima"

**Complejidad técnica:**
- Bridges nativos (Swift/Kotlin ↔ JavaScript)
- Testing en dispositivos reales de ambas plataformas
- Mantenimiento de UX consistente con código divergente

---

## SLIDE 8: IA COMO ACELERADOR
### Título: "Desarrollo Potenciado por IA"

**Visual:** Gráfico comparativo tiempo de desarrollo

```
Desarrollo Tradicional:     ████████████████  16 semanas
Desarrollo con IA:          ████████          12 semanas
                                             
                            Ahorro: 25% tiempo
```

**Casos de uso específicos:**

**1. Generación de Componentes**
```
Prompt → "Crea componente TripCard con animaciones"
Resultado → 300 líneas de código base en 2 minutos
Humano → Refinamiento y adaptación (30 min)
```

**2. Debugging Asistido**
```
Error → Crash en iOS con sensores
IA → Identifica race condition en 3 intentos
Humano → Implementa solución thread-safe
```

**3. Optimización de Queries**
```
Query lenta → 3 segundos
IA sugiere → Índices + refactor
Resultado → 0.3 segundos (10x mejora)
```

**Mensaje clave:**
> "La IA no reemplaza al ingeniero. Lo libera para enfocarse en decisiones de alto nivel."

**Gamaliel añade:**
"Sin IA, este proyecto habría sido solo Android o solo iOS. Con IA, tengo ambos con calidad production."

---

## SLIDE 9: LANZAMIENTO PROFESIONAL
### Título: "Más Allá del Prototipo Académico"

**Visual:** Checklist con ✅

### Infraestructura Completa

✅ **RGPD Compliance desde Diseño**
- Consentimiento explícito
- Derecho al olvido implementado
- Datos anonimizados en analytics
- Privacy Policy + Terms of Service

✅ **Presencia Web Profesional**
- Landing page: driveskore.org
- Responsive design
- SEO optimizado
- Contact forms operativos

✅ **Distribution Channels**
- iOS: Apple TestFlight (beta testing)
- Android: Google Play Internal Testing
- Preparado para public release

✅ **Observabilidad**
- Firebase Analytics: usuarios, retención, crashes
- Supabase Dashboard: queries, performance
- Error tracking con stack traces

✅ **CI/CD Automatizado**
```
git push → GitHub Actions → Tests → Build → Deploy
                 ↓
            Vercel (< 1 min)
```

**Mensaje clave:**
> "Un estudiante puede hacer un prototipo. Un ingeniero construye un producto. DriveSkore es un producto."

---

## SLIDE 10: INNOVACIÓN Y RETOS
### Título: "Complejidad Técnica Superada"

**Visual:** Three columns con iconos

```
╔════════════════════════════════════════════════════════╗
║    🔧 TÉCNICO    │   📱 PLATAFORMA   │   🚀 PRODUCTO   ║
╠════════════════════════════════════════════════════════╣
║ Sincronización  │  Soluciones       │  De concepto    ║
║ multi-sensor    │  nativas sin      │  a usuarios     ║
║ en tiempo real  │  comprometer UX   │  reales en      ║
║                 │                   │  12 semanas     ║
║                 │                   │                 ║
║ • GPS accuracy  │  • iOS widgets    │  • Testing      ║
║ • Acelerómetro  │  • Android overlay│    real campus  ║
║ • Giroscopio    │  • Bridges nativos│  • Feedback     ║
║ • Fusión datos  │  • Code sharing   │    continuo     ║
║   50Hz          │    maximizado     │  • Iteración    ║
║                 │                   │    ágil         ║
║                 │                   │                 ║
║ Reto: Precisión │  Reto: Mantener   │  Reto: Calidad  ║
║ bajo condiciones│  una codebase     │  production con ║
║ variables       │  para dos mundos  │  timeline académico ║
║ (túneles, etc.) │  diferentes       │                 ║
╚════════════════════════════════════════════════════════╝
```

**Gamaliel detalla cada columna:**

**Técnico:**
"Los sensores de móviles no son perfectos. Un GPS puede tener error de 5-10 metros. Implementé filtro de Kalman para fusionar múltiples fuentes y obtener precisión submétrica."

**Plataforma:**
"React Native da el 80% gratis. El 20% que marca la diferencia requiere código nativo. Escribí bridges Swift y Kotlin manteniendo arquitectura compartida."

**Producto:**
"Conseguir usuarios reales dispuestos a probar tu app en su vida diaria, recoger feedback honesto, e iterar rápidamente es tan difícil como el código mismo."

---

## SLIDE 11: IMPACTO Y ESCALABILIDAD
### Título: "Del Campus al Mundo"

**Visual:** Roadmap visual con fases

### Situación Actual
```
📊 Métricas Beta (Campus UHU)
├─ 15 usuarios activos
├─ 200+ viajes evaluados  
├─ 1,500 km analizados
└─ 4.6/5 rating promedio
```

### Roadmap de Crecimiento

**Q1 2025: Local Expansion**
- Lanzamiento público Huelva/Sevilla
- Partnership con autoescuelas locales
- Target: 500 usuarios activos

**Q2 2025: Gamificación**
- Sistema de logros y challenges
- Leaderboards por ciudad
- Social features: compartir scores

**Q3 2025: Monetización**
- Freemium model: básico gratis, análisis avanzados premium
- Partnership con aseguradoras: descuentos por buen scoring
- B2B: flotas empresariales

**Q4 2025: Internacional**
- Localización multi-idioma
- Adaptación a normativas locales
- Target: 10,000 usuarios en 3 países

### Potencial Global

**Mercado direccionable:**
- 1,400 millones de conductores en el mundo
- Si capturamos el 0.1% → 1.4 millones de usuarios
- A $2/usuario/mes → $33.6M ARR potencial

**Mensaje clave:**
> "La infraestructura está lista. La tecnología funciona. El producto existe. Ahora toca escalar."

---

## SLIDE 12: CIERRE MEMORABLE
### Título: "DriveSkore: Salvando Vidas, Un Conductor a la Vez"

**Visual:** Imagen inspiracional de carretera al atardecer + logo DriveSkore

**Texto principal (grande, centrado):**

```
1.3 millones de muertes al año.

No podemos prevenir todas.

Pero si DriveSkore ayuda a evitar UNA,
ya habrá valido la pena.
```

**Call to Action:**
```
🌐 driveskore.org
📱 Disponible en TestFlight y Play Store
💬 gamaliel@driveskore.org

¿Preguntas?
```

**Gamaliel cierra con:**
"DriveSkore comenzó como mi Trabajo Fin de Máster. Pero no termina aquí. Es una herramienta que puede cambiar cómo el mundo conduce. Y está lista para hacerlo. Gracias."

---

## NOTAS PARA GAMALIEL - PREPARACIÓN DEFENSA

### Timing por Slide (Total: 20 minutos)
1. Apertura problema: 1.5 min
2. La solución: 1.5 min
3-4. Demo: 5 min (crítico practicar)
5. Metodología: 2 min
6. Arquitectura: 2 min
7. Universalidad: 2 min
8. IA como acelerador: 1.5 min
9. Lanzamiento profesional: 1.5 min
10. Retos técnicos: 2 min
11. Impacto: 1 min
12. Cierre: 0.5 min

**Buffer: 0.5 min para ajustes**

### Preparación Demo (CRÍTICO)
- [ ] Testar proyección 30 minutos antes
- [ ] Móvil en modo avión (sin notificaciones)
- [ ] Video backup en portátil por si falla
- [ ] Batería móvil al 100%
- [ ] Cerrar todas las apps excepto DriveSkore
- [ ] Practicar narración de la demo 10 veces mínimo

### Transiciones Clave
- Problema → Solución: "DriveSkore nace para resolver esto"
- Demo → Técnica: "Esto es lo que ve el usuario. Veamos qué hay detrás"
- Técnica → Impacto: "Tenemos la tecnología. Ahora hablemos de escala"

### Preguntas Anticipadas y Respuestas

**Iñaki (Sistemas/Open Source):**
- P: "¿Por qué Vercel/Supabase y no self-hosted?"
- R: "Free tier aguanta primeros 1000 usuarios. Costes marginales <$100/mes hasta 10k usuarios. Migración posible si necesaria, pero prioridad es velocidad de iteración."

**Victoria (Lenguaje Natural):**
- P: "¿Cómo validaste los algoritmos de evaluación?"
- R: "Comparamos con estándares DGT para examen de conducción. Calibramos con datos de 200+ viajes. Error promedio <5% vs evaluación humana."

**Raúl (Subdirector/Viabilidad):**
- P: "¿Qué te diferencia de apps existentes?"
- R: "Simplicidad extrema + datos precisos + multiplataforma real. Competidores son o muy complejos o solo Android o con accuracy pobre."

**Cualquiera:**
- P: "¿Y la privacidad de datos de localización?"
- R: "RGPD by design. Datos procesados on-device siempre que posible. Backend solo recibe datos agregados. Usuario puede borrar todo con un click."

### Lenguaje Corporal y Delivery
- Contacto visual rotativo con los 3 evaluadores
- Manos visibles, gestos naturales para enfatizar
- Velocidad: 140-160 palabras/minuto (ni lento ni acelerado)
- Pausas estratégicas después de datos impactantes
- Sonreír en apertura y cierre (confianza)

### Emergency Protocols
- Si demo falla: "Tengo un video backup que muestra exactamente esto" → switch sin pánico
- Si te quedas sin tiempo: saltar slides 8 o 10 (menos críticos)
- Si pregunta difícil: "Excelente pregunta. No tengo la respuesta exacta ahora pero puedo investigarlo y compartirlo después de la defensa"

### Último Recordatorio
**No leas los slides. Cuenta la historia.**
Los slides son tu apoyo visual, no tu guion.
Conoces DriveSkore mejor que nadie en esa sala.
Confía en tu trabajo. Es excepcional.

---

## ELEMENTOS PARA REVEAL.JS

### Theme Sugerido
```javascript
// Custom theme basado en 'black' con ajustes
{
  background: '#1a1a2e',
  primary: '#16213e',
  accent: '#0f3460',
  highlight: '#e94560',
  text: '#f1f1f1'
}
```

### Transiciones
- Entre slides principales: 'slide'
- Para la demo: 'fade'
- Para datos/cifras: 'convex'

### Plugins Recomendados
- RevealNotes (para notas del ponente)
- RevealHighlight (para código)
- RevealMarkdown
- RevealMath (si incluyes fórmulas del filtro de Kalman)

### Tipografía
- Títulos: Montserrat Bold, 48pt
- Texto: Inter Regular, 24pt
- Código: Fira Code, 18pt
- Énfasis: Montserrat SemiBold

---

**FIN DEL DOCUMENTO**
Preparado por: Jose (Director TFM) & Claude
Para: Gamaliel (Defensa TFM DriveSkore)
Fecha: Diciembre 2025

¿Qué diferencia a DriveSkore de otros proyectos de fin de master?
1. Objetivo: Crear una herramienta para ayudar a las personas del mundo a conducir mejor
2. Simplicidad: Crear una herramienta que sea fácil de utilizar y que no interfiera con la conducción
3. Metodología: Etapa de testeo real
4. Universalidad: Versión de Android y iPhone
5. Tiempo de desarrollo: Desarrollado en menos tiempo gracias al uso inteligente de la IA
6. Enfoque de lanzamiento real: Que incluye aspectos como la ley de proyección de datos, sistema escalable (Vercel, Supabase, React EAS Build, Apple Test Flight,
   Landing Page (driveskore.org), Analíticas de uso de la Aplicación a través de FireBase
7. Herramientas de desarrollo colaborativo: Git, GitHub
8. Desarrollo continuo: Despliegue automático en Vercel tras realizar un commit en el repositorio de GitHub
 
   
