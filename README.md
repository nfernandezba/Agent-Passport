# Agent Passport

**Una herramienta bilingüe del CoE Toolkit para idear, documentar, gobernar y operar agentes durante todo su ciclo de vida.**

Agent Passport transforma la definición inicial de un agente en un registro de gobierno vivo. La solución permite documentar su identidad, propósito, audiencia, zona de gobierno, riesgo, conocimiento, datos, acciones, integraciones, responsables, observabilidad, revisiones y criterios de ciclo de vida.

La aplicación está implementada como una **SPA estática contenida en un único archivo HTML**, sin backend ni base de datos.

## Características principales

- Interfaz bilingüe en **español de Argentina (`es-AR`)** e **inglés de Estados Unidos (`en-US`)**.
- Navegación guiada mediante ocho etapas.
- Diseño responsive para escritorio, tablet y dispositivos móviles.
- Preguntas simples y bloques compuestos visualmente agrupados.
- Registros repetibles con identificadores consistentes para fuentes, acciones, integraciones y KPIs.
- Clasificación conforme al modelo de zonas del libro: **Z1, Z2, Z3 y Z3+**.
- Registro independiente de la zona de gobierno de Microsoft.
- Revisiones compuestas para seguridad, privacidad, compliance, arquitectura, Responsible AI y otros controles.
- Resumen ejecutivo con porcentaje de completitud.
- Exportación e importación del pasaporte en formato JSON.
- Generación local de un reporte PDF en formato A4.
- Integración con LinkedIn para compartir el uso de la herramienta.
- Apartado dedicado a los libros de Nicolás Fernández.
- Acceso a otras herramientas del CoE Toolkit.

## Etapas del pasaporte

La solución organiza la información en las siguientes secciones:

1. **Identidad y propósito**  
   Define el nombre, identificador, propósito, problema de negocio, caso de uso, audiencia, criterios de éxito, sponsors y otros datos fundacionales.

2. **Gobierno y riesgo**  
   Registra las zonas de gobierno, sensibilidad de los datos, capacidad de acción, autonomía, impacto, criticidad, riesgo inherente y residual, canales y obligaciones regulatorias.

3. **Conocimiento y datos**  
   Permite agregar múltiples fuentes de conocimiento y relacionar cada una con sus owners, ubicación, método de grounding, autenticación, sensibilidad, frecuencia de actualización y estado de verificación.

4. **Acciones e integraciones**  
   Documenta las operaciones que el agente puede ejecutar y cada sistema conectado, junto con permisos, identidad de ejecución, límites, aprobaciones, riesgos y mecanismos de rollback.

5. **Ownership**  
   Identifica las responsabilidades de negocio, producto, construcción, arquitectura, seguridad, privacidad, Responsible AI, operaciones, soporte y gobierno del CoE.

6. **Observabilidad y ciclo de vida**  
   Registra KPIs, monitoreo, transcripciones, auditoría, señales de degradación, alertas, costes, incidentes, soporte, promoción, revisión y retiro.

7. **Revisiones**  
   Agrupa los controles formales mediante bloques compuestos que incluyen estado, reviewer, rol, fecha, vigencia, próxima revisión, condiciones, evidencia y comentarios.

8. **Resumen**  
   Presenta una vista consolidada del pasaporte, sus principales clasificaciones, registros, revisiones y nivel de completitud.

## Modelo de registros repetibles

Agent Passport evita mantener listas paralelas que puedan perder consistencia. Cada elemento repetible se almacena como un registro independiente con un identificador estable.

| Entidad | Formato de ID | Ejemplo |
|---|---|---|
| Fuente de conocimiento | `KS-NNN` | `KS-001` |
| Acción | `AC-NNN` | `AC-001` |
| Integración | `DEP-NNN` | `DEP-001` |
| KPI | `KPI-NNN` | `KPI-001` |

Por ejemplo, cada fuente de conocimiento contiene sus propios owners. Esto garantiza que el owner, la fecha de verificación, la sensibilidad y el método de acceso permanezcan relacionados con la fuente correcta.

## Revisiones compuestas

Las validaciones no se presentan como preguntas independientes del tipo “Sí/No + fecha + reviewer”. Cada revisión se representa como un único componente visual con los siguientes atributos:

- Requerida: sí, no o por determinar.
- Estado.
- Reviewer y rol.
- Fecha de revisión.
- Vigencia.
- Próxima revisión.
- Condiciones.
- Evidencia.
- Comentarios.

Los estados disponibles son:

- No requerido.
- No iniciado.
- En curso.
- En revisión.
- Aprobado.
- Aprobado con condiciones.
- Rechazado.
- Vencido.

## Requisitos

La solución no requiere instalación, compilación ni servidor de aplicaciones.

Para utilizar todas sus capacidades se recomienda:

- Un navegador moderno con JavaScript habilitado.
- Conexión a Internet para cargar Google Fonts, jsPDF y las portadas de los libros.
- Permitir descargas de archivos para exportar JSON y PDF.

Navegadores recomendados:

- Microsoft Edge.
- Google Chrome.
- Mozilla Firefox.
- Safari en versiones recientes.

## Uso local

### Opción 1: abrir directamente

1. Descargá `agent-passport.html`.
2. Abrí el archivo con un navegador moderno.
3. Seleccioná el idioma.
4. Elegí **Crear pasaporte** o **Importar JSON**.

### Opción 2: usar un servidor local

Aunque no es obligatorio, un servidor local ofrece un comportamiento más cercano al de un sitio publicado.

Con Python:

```bash
python -m http.server 8000
```

Luego abrí:

```text
http://localhost:8000/agent-passport.html
```

Con Node.js y `npx`:

```bash
npx serve .
```

## Publicación en GitHub Pages

1. Creá un repositorio de GitHub.
2. Copiá `agent-passport.html` en la raíz del repositorio.
3. Opcionalmente, renombralo como `index.html`.
4. Abrí **Settings > Pages**.
5. En **Build and deployment**, seleccioná **Deploy from a branch**.
6. Elegí la rama principal y la carpeta raíz.
7. Guardá la configuración.

La aplicación no necesita ajustes específicos de redirect URI ni configuración de autenticación, ya que esta versión no consume APIs protegidas ni utiliza MSAL.

## Persistencia y privacidad

Los datos del pasaporte permanecen en memoria durante la sesión del navegador.

- La información introducida **no se envía a ningún servidor**.
- El pasaporte **no se guarda automáticamente**.
- El único dato persistido en `localStorage` es el idioma seleccionado.
- Para conservar el trabajo se debe utilizar **Exportar JSON**.
- El archivo JSON puede importarse posteriormente para continuar la edición.

El JSON exportado incluye:

```json
{
  "meta": {
    "schema": "agent-passport",
    "version": "1.0",
    "createdOn": "YYYY-MM-DD",
    "modifiedOn": "YYYY-MM-DD",
    "exportedOn": "ISO-8601",
    "language": "es"
  }
}
```

Durante la importación, la aplicación verifica que `meta.schema` sea igual a `agent-passport`.

> No cargues información real sensible, secretos, contraseñas, tokens, certificados ni datos personales regulados en equipos o navegadores no administrados.

## Exportación a PDF

La generación de PDF se realiza localmente mediante **jsPDF 2.5.1**.

El reporte incluye:

- Portada ejecutiva.
- Nombre e ID del agente.
- Zona del libro y etapa del ciclo de vida.
- Identidad y propósito.
- Gobierno y riesgo.
- Fuentes de conocimiento.
- Acciones.
- Ownership.
- Observabilidad y KPIs.
- Estado de las revisiones.
- Libros relacionados.
- Herramientas adicionales del CoE Toolkit.
- Enlace al perfil de LinkedIn del autor.

El archivo se genera con el siguiente patrón:

```text
Agent-Passport-<nombre-o-id>-<idioma>-<fecha>.pdf
```

## Estructura técnica

La solución se distribuye como un único archivo:

```text
agent-passport.html
```

El archivo contiene:

- HTML semántico.
- CSS responsive.
- Recursos SVG embebidos para logo y banderas.
- Diccionarios completos para `es-AR` y `en-US`.
- Estado de la aplicación en JavaScript.
- Componentes para registros repetibles.
- Importación y exportación JSON.
- Generación del PDF.
- Enlaces a libros, LinkedIn y herramientas relacionadas.

### Dependencias externas

| Dependencia | Uso |
|---|---|
| Google Fonts | Tipografías Space Grotesk e Inter |
| jsPDF 2.5.1 | Generación del reporte PDF |
| Amazon Images | Portadas de libros |

No utiliza frameworks de frontend, gestores de paquetes ni procesos de build.

## Estructura principal del estado

```text
meta
identity
governance
knowledgeSources[]
data
actions[]
integrations[]
ownership
kpis[]
observability
lifecycle
reviews
```

Las colecciones repetibles se almacenan como arrays. Las revisiones se almacenan como objetos compuestos independientes.

## Personalización

### Cambiar textos o traducciones

Los contenidos bilingües se encuentran en el objeto JavaScript:

```javascript
const CONTENT = {
  es: { /* Español de Argentina */ },
  en: { /* English - United States */ }
};
```

### Cambiar listas controladas

Las opciones reutilizables se encuentran en:

```javascript
const OPTION_SETS = {
  agentType: [],
  platform: [],
  audience: [],
  sensitivity: [],
  actionLevel: [],
  autonomy: [],
  impact: [],
  lifecycle: [],
  sourceType: [],
  grounding: [],
  access: [],
  refresh: [],
  operation: [],
  permission: [],
  risk: [],
  kpiCategory: [],
  reviewStatus: []
};
```

### Cambiar los tipos de revisión

Los bloques de revisión se generan desde la colección `REVIEW_TYPES`. Para incorporar una nueva revisión, agregá una entrada con su clave y nombres en ambos idiomas.

### Cambiar libros

Las ediciones en español e inglés se configuran en:

```javascript
const BOOKS = {
  es: [],
  en: []
};
```

### Cambiar herramientas adicionales

Las herramientas complementarias se configuran en:

```javascript
const TOOLS = [];
```

Cada entrada contiene una URL y textos diferenciados por idioma.

### Cambiar LinkedIn

El perfil se define mediante:

```javascript
const LINKEDIN = "https://www.linkedin.com/in/nfernandezba";
```

## Modelo de zonas del libro

La clasificación del libro utiliza exclusivamente:

- **Z1**
- **Z2**
- **Z3**
- **Z3+**

Esta clasificación se registra de manera independiente de la zona de gobierno de Microsoft. La solución no asume que ambas clasificaciones sean equivalentes.

## Libros relacionados

La aplicación incluye enlaces a las ediciones en español e inglés de:

- **Definiendo la estructura marco para el Centro de Excelencia de Power Platform**.
- **Copilot Studio y el futuro del Centro de Excelencia de Power Platform**.
- **Defining the Framework Structure for the Power Platform Center of Excellence**.
- **Copilot Studio and the Future of the Power Platform Center of Excellence**.

## Otras herramientas del CoE Toolkit

### Power Platform Tenant Inventory Explorer

Exploración read-only del inventario del tenant, entornos, recursos, políticas DLP y configuraciones de gobierno.

<https://nfernandezba.github.io/power-platform-tenant-inventory-explorer/>

### Copilot Studio Credits Monitor

Monitoreo de capacidad comprada, asignada y consumida, asignaciones por entorno e inventario de agentes.

<https://nfernandezba.github.io/Copilot-Studio-Credits-Monitor/>

### Environment Strategy Quick Assessment

Autoevaluación bilingüe de definición, cobertura, documentación, comunicación y vigencia de la estrategia de entornos.

<https://nfernandezba.github.io/Power-Platform-Copilot-Studio-Environment-Assessment/>

## Limitaciones conocidas

- No existe guardado automático del pasaporte.
- No incluye autenticación ni control de acceso.
- No utiliza Dataverse, SharePoint ni otra persistencia empresarial.
- No permite colaboración simultánea entre múltiples usuarios.
- No adjunta archivos al JSON; únicamente almacena referencias o enlaces introducidos por el usuario.
- La generación de PDF depende de que jsPDF pueda cargarse desde su CDN.
- Las portadas de los libros dependen de recursos externos de Amazon.
- La exportación PDF utiliza las fuentes estándar de jsPDF y normaliza algunos caracteres para mejorar la compatibilidad.
- El porcentaje de completitud es orientativo y no representa una certificación, auditoría o aprobación formal.

## Consideraciones de gobierno

Agent Passport es una plantilla de ideación y gobierno. No sustituye:

- Evaluaciones legales.
- Revisiones de seguridad.
- Análisis de privacidad o DPIA.
- Evaluaciones de compliance.
- Revisiones de Responsible AI.
- Revisiones de arquitectura.
- Pruebas técnicas o de penetración.
- Procesos formales de aceptación de riesgo.

Las organizaciones deben adaptar los campos, clasificaciones, revisiones y criterios de aprobación a su marco normativo y operativo.

## Control de versión

Versión actual de la solución:

```text
v1.0
```

El esquema JSON utilizado por esta versión es:

```text
agent-passport / 1.0
```

Antes de introducir cambios incompatibles en el modelo de datos, se recomienda definir una estrategia de migración para los archivos JSON exportados con versiones anteriores.

## Autor

**Nico Fernández**  
Power Platform, Copilot Studio y Centros de Excelencia

LinkedIn: <https://www.linkedin.com/in/nfernandezba>

## Aviso

Agent Passport forma parte del **CoE Toolkit**. Es una herramienta orientativa y no constituye una certificación de Microsoft ni una validación automática de seguridad, privacidad, cumplimiento normativo o arquitectura.
