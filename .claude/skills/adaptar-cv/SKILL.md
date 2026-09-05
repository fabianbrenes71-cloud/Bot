---
name: adaptar-cv
description: Adapta el CV base del usuario (en cv/cv-base.md) a una oferta de empleo específica, dada como URL o texto pegado. Usar cuando el usuario pida "adaptar mi CV", "ajustar mi CV a esta oferta", "postular a este puesto" o pegue/enlace una descripción de trabajo junto con la intención de aplicar.
---

# Adaptar CV a una oferta de empleo

Este skill toma el CV base del usuario y genera una versión adaptada (en Markdown,
convertible a PDF) resaltando la experiencia y habilidades más relevantes para
una oferta de trabajo concreta.

## Flujo

1. **Cargar el CV base**
   - Leer `cv/cv-base.md` en la raíz del repo.
   - Si no existe, pedir al usuario que pegue su CV o indique dónde está, y
     guardarlo en `cv/cv-base.md` para futuras adaptaciones. Nunca inventes
     experiencia, títulos o habilidades que no estén en el CV base.

2. **Obtener la oferta de empleo**
   - Si el usuario da una URL, usar WebFetch para extraer el texto de la
     publicación (título del puesto, empresa, requisitos, responsabilidades).
   - Si el usuario pega el texto directamente, usar ese texto.
   - Si la URL falla o el contenido no se puede extraer (login requerido,
     bloqueo, etc.), pedir al usuario que pegue el texto de la oferta.

3. **Analizar la oferta**
   - Extraer: título del puesto, empresa, requisitos obligatorios, requisitos
     deseables, palabras clave técnicas (herramientas, lenguajes, metodologías),
     y tono/seniority esperado.

4. **Adaptar el CV** (sin inventar información)
   - Reordenar/priorizar experiencias y logros del CV base que mejor calcen
     con los requisitos de la oferta.
   - Ajustar el resumen/perfil profesional (2-4 líneas) para reflejar el
     puesto y palabras clave de la oferta.
   - Usar terminología similar a la de la oferta cuando el CV base ya
     respalda esa habilidad o experiencia (para pasar filtros ATS), sin
     exagerar ni mentir.
   - Mantener formato limpio en Markdown: nombre, contacto, resumen,
     experiencia, educación, habilidades, idiomas (según lo que tenga el CV
     base).
   - Señalar al usuario, en un breve resumen aparte (no dentro del CV), qué
     requisitos de la oferta NO cumple su CV base, para que decida si quiere
     agregar algo manualmente.

5. **Guardar y entregar**
   - Guardar el CV adaptado en `cv/aplicaciones/<empresa>-<puesto>.md`
     (nombres en minúsculas, sin espacios ni tildes).
   - Ofrecer convertir el archivo a PDF (pandoc, si está disponible) o a un
     artifact para revisión visual, y mandarlo al usuario con SendUserFile.

## Notas importantes

- Nunca inventar experiencia, certificaciones, empresas o fechas que no
  estén en `cv/cv-base.md`.
- Si el usuario corrige o mejora el CV adaptado, preguntar si también quiere
  actualizar `cv/cv-base.md` con esa mejora para futuras aplicaciones.
- Idioma de salida: el mismo idioma en que está escrito el CV base, salvo
  que el usuario pida explícitamente otro idioma (por ejemplo, oferta en
  inglés).
