# Informe Técnico: Sistema de Planificación Inteligente de Eventos

## I. Introducción y Dominio
Se seleccionó el dominio de la organización de bodas bajo la marca "Raquel & Alba Planner". La aplicación gestiona eventos que consumen recursos finitos (mobiliario, personal especializado y sedes físicas). El sistema no funciona como una simple base de datos, sino como un **motor de planificación** que garantiza la viabilidad operativa de cada evento mediante la resolución de conflictos de tiempo y espacio.

## II. Estructura y Diseño
El proyecto se diseñó bajo una arquitectura modular para separar la lógica de negocio de la persistencia de datos:
* **Capa de Datos:** Se empleó formato JSON para simular una base de datos relacional, permitiendo la actualización de stock en tiempo real.
* **Lógica de Negocio:** Se implementó un motor de validación cruzada que analiza la compatibilidad entre el lugar elegido, el personal contratado y los ítems de inventario.

## III. Reglas de Negocio y Restricciones
Se definieron un conjunto de restricciones basadas en la seguridad y el confort del asistente:
1.  **Restricciones Acústicas y Ambientales:** 
**Incompatibilidad de Materiales: Se bloquea la contratación de música de alto impacto (Mariachis) en entornos con materiales reflectantes como el Palacio de Cristal para evitar saturación por eco.

**Conflictos de Audio: El sistema prohíbe la contratación simultánea de un DJ y una Banda de Rock. Esta regla evita la superposición de señales sonoras y optimiza el uso del escenario.

**Infraestructura de Sonido: Si se detecta cualquier servicio musical, el sistema impone la inclusión obligatoria de "Equipo de Sonido Profesional".
2.  **Validación de Recursos (Pools):** 
**Validación de Recursos (Pools de Inventario)
Ratio de Asientos: El sistema calcula dinámicamente que el mobiliario reservado cubra al menos el 80% de los invitados registrados.

**Ratio de Superficie: Se exige la reserva de 1 mesa por cada 10 personas, garantizando la viabilidad del servicio de catering y el confort.

**Gestión de Stock: No se permite exceder las unidades físicas disponibles en los archivos JSON, asegurando que no existan "reservas fantasma".
3.  **Dependencias de Personal y Servicios:**
**Especialización en Bebidas: La selección de "Barra Libre" o "Coctelería" activa la obligatoriedad de contratar un Sommelier o Barman.

**Protocolo y Ceremonia: El servicio de "Solo de Violín" requiere la presencia de un Maestro de Ceremonias para la coordinación de los tiempos nupciales.
4.  **Seguridad Preventiva y Logistica:** 
**Gestión de Riesgos: Se impone la contratación de Personal de Seguridad de forma obligatoria para la sede "Terraza del Sol" debido a la presencia de riesgos físicos (piscina).

6. **Restricción de Duración Mínima:**
Se estableció un umbral de 120 minutos (2 horas) mediante el cálculo de `timedelta`. Esto asegura que los contratos con proveedores de música y catering sean rentables y operativos.

## IV. Problemas Enfrentados durante el Desarrollo
* **Gestión de Codificación:** Se presentó un conflicto con caracteres especiales (ñ, acentos) al serializar los archivos JSON. Se resolvió mediante la estandarización de codificación UTF-8 y el parámetro `ensure_ascii=False`.
* **Normalización de Tiempos:** El cálculo de intervalos que cruzan la medianoche representó un desafío logístico. Se solucionó mediante el uso de la librería `datetime` y objetos `timedelta` para verificar colisiones en reservas nocturnas.
* **Validación de Salida:** Inicialmente, los errores de stock se notificaban al final del proceso. Se rediseñó el flujo para incluir validaciones preventivas inmediatamente después de la selección de cada categoría, mejorando la experiencia del usuario.
* **Visualización y Formateo de Datos (PEP 8):** Uno de los retos fue presentar tablas de inventario legibles en consola sin exceder los límites de caracteres por línea. Se resolvió desacoplando las cadenas de formato de las variables y utilizando técnicas de *f-string splitting* para mantener el código limpio y cumplir con los estándares de documentación (Docstrings).
* **Limpieza de Código y Estándares:** Se realizó una refactorización para eliminar el error de "Line too long" y se añadieron encabezados de documentación a cada módulo para facilitar el mantenimiento futuro del software.

## V. Conclusión
La implementación demuestra que la gestión de eventos complejos requiere un balance entre flexibilidad y restricciones estrictas. El uso de validaciones intermedias asegura que no se generen compromisos de recursos imposibles de cumplir.
[⬅️ Volver al README principal](./README.md)