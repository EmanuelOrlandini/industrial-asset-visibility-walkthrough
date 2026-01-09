# Recorrido de Visibilidad de Activos Industriales (OT/IT)

Un caso de estudio práctico sobre cómo realizar un inventario inicial de activos de red y evaluar configuraciones básicas de seguridad en un entorno real, aplicando principios de ciberseguridad industrial (OT Security).

--> 📋 Resumen
Este proyecto documenta la ejecución de un escaneo de red **no intrusivo** en una empresa del sector industrial, con el objetivo de establecer un **inventario base de activos** y identificar configuraciones que pudieran representar un riesgo de seguridad. El proceso se realizó en menos de un minuto, sin afectar la disponibilidad de los sistemas, y siguiendo un enfoque de **bajo impacto y máxima transparencia**.

--> 🧠 Contexto y Motivación
En la transición hacia la Industria 4.0, la convergencia entre los sistemas operativos (OT) y los sistemas de información (IT) crea nuevas superficies de ataque. El **primer paso** para proteger cualquier entorno es **saber qué hay conectado**. Este ejercicio simula esa tarea fundamental en un escenario controlado y autorizado.

--> 🛠️ Metodología (Enfoque Práctico y Seguro)

  ### 1. Autorización y Planificación ###
  - Obtención de **autorización por escrito** del responsable del área.
  - Entrevista breve con el personal técnico para identificar equipos sensibles.
  - Determinación del rango de red a escanear mediante `ipconfig`.

  ### 2. Selección de Herramienta ###
  Se eligió **Angry IP Scanner** (versión portable) por:
  - Interfaz gráfica que permite **control visual** en tiempo real.
  - Capacidad de **interrumpir el escaneo instantáneamente** (botón STOP).
  - Modo de **solo descubrimiento** (ping), sin escaneo agresivo de puertos.
  - Facilidad para **explicar el proceso** a personas no técnicas.

  ### 3. Ejecución por Capas ###
  - **Prueba Micro:** Escaneo de solo 10 direcciones IP en un segmento conocido. Espera de 15 minutos para verificar que no hubiera impacto.
  - **Escaneo Completo:** Ejecución del escaneo en el rango `/24` (254 direcciones). Duración: **44 segundos**.
  - **Análisis Manual:** Identificación de fabricantes mediante direcciones MAC (`arp -a` + lookup OUI) y verificación manual de servicios web en puertos comunes (80, 443)
  - **solo con fines de identificación**.

  ### 4. Principios de Seguridad Aplicados ###
  - **Velocidad Lenta:** Pausas entre requests para no saturar equipos antiguos.
  - **Horario No Crítico:** Ejecución fuera del horario productivo pico.
  - **Sin Interacción:** No se ingresaron credenciales ni se interactuó con los servicios descubiertos.

--> 🔍 Hallazgos y Análisis

  ### Resultados Cuantitativos ###
  - **IPs escaneadas:** 254
  - **Dispositivos activos:** 21 (8.2% del total)
  - **Tiempo total del escaneo:** 44 segundos (0.17 seg/dispositivo)

  ### Hallazgo Cualitativo Principal: Punto de Acceso con Administración Expuesta ###
  Se identificó un dispositivo activo (`192.168.100.205`) con los puertos **80 (HTTP) y 443 (HTTPS)** accesibles desde toda la red interna.

**Investigación posterior reveló:**
- **Modelo:** TP-Link EAP225-Outdoor (confirmado por dirección MAC `AA:BB:CC:DD:EE:FF`).
- **Función:** Punto de acceso WiFi empresarial para exteriores/áreas amplias.
- **Estado de seguridad:** Interfaz protegida por credenciales personalizadas (las de fábrica fueron cambiadas).

**Análisis de Riesgo:**
El dispositivo **no presenta una vulnerabilidad crítica**, pero su configuración actual **expone innecesariamente su panel de administración** a toda la red, violando el **principio de mínimo privilegio**. Esto incrementa la superficie de ataque para un posible **movimiento lateral** en caso de que un malware comprometa un equipo interno.

--> 📝 Aprendizajes y Recomendaciones

  ### Aprendizajes Clave ###
  1.  **La visibilidad es el cimiento:** No se puede proteger lo que no se conoce.
  2.  **La herramienta correcta depende del contexto:** Para un primer inventario, una GUI controlable puede ser más segura y efectiva que un script automatizado.
  3.  **Comunicación > Complejidad:** Un hallazgo bien documentado y contextualizado tiene más impacto que una lista técnica incomprensible.
  4.  **OT requiere paciencia:** Los principios de disponibilidad y cautela priman sobre la exhaustividad del escaneo.

  ### Recomendaciones Generadas (Para el Entorno Evaluado) ###
  1.  **Verificación de Hardening Básico:** Confirmar que el firmware del punto de acceso esté actualizado y que sus credenciales sean robustas.
  2.  **Documentación de Activos:** Iniciar un registro formal de activos de red (IP, MAC, responsable, función).
  3.  **Mejora de Arquitectura a Futuro:** Evaluar la segmentación de red para restringir el acceso administrativo únicamente al personal técnico autorizado.

--> ⚠️ Advertencia de Seguridad y Ética
  **⚠️ Este material es estrictamente para fines educativos y de evaluación autorizada.**
- **Nunca** escanee o interactúe con redes o sistemas sin autorización **explícita y por escrito**.
- En entornos OT/Industriales, la **disponibilidad** es la prioridad número uno. Privilegie siempre métodos **no intrusivos**.
- La **comunicación transparente** de los alcances y métodos es fundamental para mantener la confianza.
- El autor **no se hace responsable** del uso indebido de esta información o metodología.

---
*Proyecto realizado como parte de mi formación y transición profesional hacia la **Ciberseguridad Industrial**.*  
*Conectemos en [LinkedIn](https://linkedin.com/in/carlos-emanuel-orlandini-berger-4363451a0) | [GitHub](https://github.com/EmanuelOrlandini)*

**Palabras clave:** Ciberseguridad Industrial, OT Security, ICS Security, Inventario de Activos, Seguridad en Redes, Evaluación de Riesgos, Asset Discovery, Industrial Cybersecurity
