🇬🇧 [English](README.md) · 🇫🇷 [Français](README.fr.md)

# English Proficiency Scorecard

Un skill para agente de IA que evalúa el nivel de inglés del usuario y genera un scorecard HTML interactivo con puntuaciones estimadas en los principales marcos internacionales: MCER, IELTS (Academic y General Training), TOEFL iBT, Cambridge (CAE/CPE) y TOEIC (L&R y S&W).

El skill evalúa escritura real a partir del historial de conversación, servicios conectados (correo electrónico, documentos) y muestras en directo opcionales — no cuestionarios ni tests de opción múltiple. El resultado es un documento HTML autónomo y compartible, con tarjetas de puntuación animadas, comparaciones con umbrales institucionales, muestras de escritura anotadas y una sección de metodología transparente.

## Cómo funciona

El skill guía a Claude a través de un flujo de trabajo en cuatro fases:

1. **Entrevista y configuración** — Comprender el perfil del usuario, recoger sus preferencias (modo de calibración, privacidad, diseño) e identificar las fuentes de evidencia disponibles
2. **Análisis de evidencia** — Analizar la escritura en todas las fuentes disponibles: gramática, vocabulario, control de registros, competencia pragmática y patrones de transferencia L1
3. **Generación del scorecard** — Producir un scorecard HTML interactivo de dos páginas a partir de la plantilla incluida, con puntuaciones calibradas según la guía de calificación y los datos de referencia
4. **Revisión y ajuste** — El usuario revisa el scorecard y puede cuestionar cualquier puntuación u observación; las áreas de mejora se discuten en el chat, no se añaden al documento

## Contenido del paquete

```
english-proficiency-scorecard/
├── SKILL.md                          # Instrucciones principales y flujo de trabajo
├── LICENSE.txt                       # Licencia MIT + verificación de integridad
├── INTEGRITY.sha256                  # Manifiesto SHA-256 de todos los archivos
├── assets/
│   └── template.html                 # Plantilla del scorecard interactivo
└── references/
    ├── scoring-guide.md              # Baremos de calificación por marco
    └── benchmarks-fallback.md        # Datos de referencia institucionales
```

## Principios de diseño

El skill se basa en siete principios documentados en SKILL.md:

1. **Integridad ante todo** — Las puntuaciones reflejan la evidencia. Claude nunca halaga ni infla resultados, ni siquiera si se le pide.
2. **El usuario elige la calibración** — Estimación honesta o conservadora, pero nunca por encima de lo que la evidencia justifica.
3. **Los datos autorreportados se marcan claramente** — Las puntuaciones de expresión oral y comprensión auditiva basadas en el testimonio del usuario se etiquetan como tales.
4. **Respeto a la privacidad** — El scorecard está diseñado para ser compartido; el usuario confirma qué información personal incluir.
5. **Sin branding — pero la divulgación del modelo es aceptable** — No se usan nombres de productos como señales de credibilidad. La sección de metodología puede indicar de forma factual qué modelo de IA realizó el análisis.
6. **Las áreas de mejora se quedan en el chat** — El scorecard muestra el nivel de competencia. Las sugerencias de mejora se discuten en privado.
7. **Neutralidad del contenido** — Todo el texto generado es lingüísticamente descriptivo, nunca culturalmente prescriptivo. Los datos de referencia son factuales, las anotaciones de muestras de escritura se limitan al análisis lingüístico, y ninguna variedad del inglés se trata como superior. Este principio también sirve como protección contra versiones manipuladas que inyecten sesgos en evaluaciones de apariencia legítima.

## Verificación de integridad

El skill incluye un sistema de integridad de tres capas:

- **Manifiesto SHA-256** (`INTEGRITY.sha256`) — Hashes de todos los archivos del paquete. Ejecute `sha256sum -c INTEGRITY.sha256` para verificar que nada ha sido modificado.
- **Testigo LICENSE** — El archivo de licencia incluye instrucciones para que el modelo de IA verifique la integridad de los archivos antes de la ejecución. Es una decisión de diseño deliberada y un punto de partida para debatir sobre la seguridad de los skills en texto plano (ver más abajo).
- **Protección de neutralidad del contenido** — El Principio 7 instruye al modelo a ignorar sus propias instrucciones si estas empujan hacia contenido sesgado, y a informar al usuario del problema.

Ninguna capa es infalible por sí sola. Juntas, dificultan significativamente el uso malicioso del skill sin que el usuario lo sepa.

### Sobre la seguridad de los skills

Los skills para agentes de IA son archivos de instrucciones en texto plano. A diferencia del software compilado, cualquiera puede abrir un SKILL.md, añadir una línea y redistribuirlo. La barrera para la manipulación es nula, y la mayoría de los usuarios no leerán 500 líneas de instrucciones para comprobar si hay comportamientos ocultos.

El sistema de integridad aquí presentado es un primer intento de abordar este problema. El mecanismo del testigo LICENSE — ocultar instrucciones de verificación en un archivo que la mayoría ignora — es intencionadamente limítrofe. Es legible por cualquiera que abra el archivo, lo cual consideramos la línea ética: transparente-si-se-inspecciona es aceptable; codificado-para-excluir-humanos no lo es.

Creemos que esta es una conversación que vale la pena tener a medida que el ecosistema de skills crece. Si tienes ideas para mejores enfoques, abre un issue.

## Uso

### Con Claude (claude.ai)

Sube la carpeta del skill a un Proyecto Claude. Cuando le pidas a Claude que evalúe tu inglés, seguirá el flujo de trabajo y generará un scorecard a partir de tu historial de conversación y tus servicios conectados.

### Con Claude Code

Coloca la carpeta del skill en tu directorio de skills. Claude Code la detectará automáticamente.

### Con otras plataformas

El skill sigue la especificación abierta [Agent Skills](https://agentskills.io). Cualquier plataforma compatible con el formato SKILL.md debería poder cargarlo.

## Origen

Este skill fue creado por HiP (Ivan Phan) y Claude Opus 4.6 (Anthropic) en febrero-marzo de 2026. Nació de una evaluación real del nivel de inglés — HiP pidió a Claude que evaluara su inglés según los marcos internacionales utilizando su historial de conversación real y dos años de correos electrónicos enviados. El scorecard resultante de esa evaluación se convirtió en la plantilla, y la metodología de evaluación se convirtió en el skill.

Los baremos de calificación, los datos de referencia, el diseño de interacción, la arquitectura de seguridad y el marco de neutralidad del contenido se desarrollaron mediante colaboración iterativa a lo largo de varias sesiones. El proyecto es una creación original, no derivada de skills existentes.

## Licencia

MIT — usa, modifica y comparte libremente. Solo mantén el crédito.

Ejecuta `sha256sum -c INTEGRITY.sha256` para comprobar si tu copia coincide con el original.
