# Proyecto-Simulador-de-Arquitectura-x86-UCB
**Materia:** Arquitectura de Computadoras  
**Carrera:** Ingeniería de Software  
**Universidad:** Universidad Católica Boliviana – Sede Santa Cruz  

**Integrantes:**  
- Andrés Mallea  
- Mijael Callejas  
- Israel Gutiérrez  

**Docente:** Paulo Cesar Loayza Carrasco  
**Fecha:** 06/10/2025  

---

## 1. Introducción

El propósito del simulador es ilustrar el funcionamiento interno de los principales componentes de una computadora tipo x86, incluyendo la CPU, la Unidad Aritmético-Lógica (ALU), los registros, la memoria RAM y el pipeline.
 El proyecto se implementó en Microsoft Excel utilizando Visual Basic for Applications (VBA), con el objetivo de crear una herramienta didáctica que permita a los estudiantes comprender de forma visual el ciclo de instrucción, las banderas (flags), el funcionamiento de la memoria caché y el flujo de ejecución de instrucciones.


###  Objetivos
• Simular el ciclo de instrucción de una arquitectura x86 de forma interactiva.
• Visualizar en tiempo real el cambio de valores en registros, memoria y flags.
• Mostrar el funcionamiento del pipeline a través de una animación en Excel.
• Proveer una base didáctica para el aprendizaje de los conceptos de arquitectura de computadoras.

---

## 2. Marco Teórico

 El simulador se fundamenta en los principios de la arquitectura x86, que sigue el paradigma CISC (Complex Instruction Set Computer), caracterizado por un conjunto extenso de instrucciones y operaciones complejas a nivel de hardware.

### 2.1 Ciclo de Instrucción
El ciclo de instrucción describe las etapas que sigue la CPU para ejecutar una instrucción: Fetch, Decode, Execute, Memory y Writeback. En el simulador, este proceso se realiza paso a paso mediante la macro principal “Simular_ALU_Paso()”.
### 2.2 Componentes del Sistema
• **CPU**: Incluye la Unidad de Control, la ALU y los registros.
 • **Memoria**: Representada por celdas de Excel que simulan RAM, Caché y Memoria Virtual.
 • **Pipeline**: Simula el flujo de instrucciones en el rango U:Y (filas 9–28).
 • **Flags**: ZF, CF, NF y SWAP, que indican los estados de la ALU.
  

---

## 3. Diseño del Simulador

El simulador fue desarrollado sobre Excel con macros VBA para controlar la ejecución.  
Los principales componentes están mapeados a celdas específicas:

| Componente | Rango / Celda | Descripción |
|-------------|----------------|--------------|
| PC (Program Counter) | C30 | Fila de instrucción actual |
| Acumulador (AC) | M9 | Resultado de operaciones |
| Entradas A/B | C5 y C6 | Operandos de entrada |
| Registros R1–R4 | M25–M28 | Registros de propósito general |
| Flags | P14–P17 | ZF, CF, NF, SWAP |
| RAM | C33:E54 | Memoria simulada |
| Caché | H38:K41 | Bloque de 4 líneas de caché |
| Pipeline | U:Y (filas 9–28) | Animación visual del flujo |

---

## 4. Historias de Usuario y Planificación del Proyecto

El proyecto se organizó bajo una **metodología ágil**, con un sprint de una semana para tres desarrolladores.  
Las historias de usuario se agrupan por épicas funcionales:

### Epic 1 – Configuración del Proyecto
| ID | Historia de Usuario | Criterios de Aceptación |
|----|----------------------|--------------------------|
| HU-001 | Configurar repositorio GitHub para colaboración. | Repositorio creado y compartido; estructura de ramas establecida. |
| HU-002 | Configurar la plataforma (Excel + VBA). | Proyecto base `.xlsm` cargado al repositorio. |

### Epic 2 – Desarrollo del Simulador
| ID | Historia de Usuario | Criterios de Aceptación |
|----|----------------------|--------------------------|
| HU-003 | Ingresar código ensamblador x86. | El simulador lee las instrucciones desde filas 9–28. |
| HU-004 | Ejecutar instrucciones paso a paso. | Botón “Ejecutar Paso” procesa una instrucción por vez. |
| HU-005 | Visualizar registros. | R1–R4, AC y F5 actualizados correctamente. |
| HU-006 | Visualizar memoria RAM. | Celdas C33:E54 actualizadas tras operaciones. |

### Epic 3 – Documentación y Presentación
| ID | Historia de Usuario | Criterios de Aceptación |
|----|----------------------|--------------------------|
| HU-007 | Preparar contenidos teóricos para la presentación. | CPU, memoria, pipeline explicados. |
| HU-008 | Redactar documentación en formato APA. | Documento Word estructurado. |

### Epic 4 – Visualización Avanzada
| ID | Historia de Usuario | Criterios de Aceptación |
|----|----------------------|--------------------------|
| HU-009 | Simular operaciones de la ALU. | Flags y resultados actualizados. |
| HU-010 | Representar ciclo de instrucción. | Etapas resaltadas visualmente. |
| HU-011 | Visualizar memoria caché y políticas. | Caché muestra “hit” o “miss” con LRU/FIFO. |
| HU-012 | Visualizar pipeline de instrucciones. | Flujo paralelo y riesgos visibles. |

### Epic 5 – Funcionalidades Opcionales
| ID | Historia de Usuario | Criterios de Aceptación |
|----|----------------------|--------------------------|
| HU-013 | Traducir código C a ensamblador x86. | Código C simple convertido a ASM funcional. |

### Epic 6 – Documentación y Defensa Final
| ID | Historia de Usuario | Criterios de Aceptación |
|----|----------------------|--------------------------|
| HU-014 | Finalizar documentación del proyecto. | Documento APA completo. |
| HU-015 | Preparar presentación y defensa. | Presentación visual lista para exposición. |

#### Asignación del Trabajo
| Desarrollador | Responsabilidades | Historias Asignadas |
|----------------|------------------|----------------------|
| Andrés Mallea | Entorno y carga de código | HU-9, HU-10, HU-3, HU-8 |
| Mijael Callejas | Lógica de ejecución y registros | HU-1, HU-2, HU-5, HU-6, HU-7 |
| Israel Gutiérrez | Memoria y documentación | HU-3, HU-4, HU-11, HU-12 |

---

## ⚙️ 5. Desarrollo e Implementación

El simulador fue programado en VBA.  
Las macros controlan tanto la lógica de la CPU como la representación visual de la memoria y el pipeline.

### Principales funciones
- `Resetear_Simulacion()` → Inicializa registros, memoria y flags.  
- `Simular_ALU_Paso()` → Ejecuta una instrucción.  
- `Cargar_Caché_Controlada()` → Maneja bloques de caché.  
- `Resaltar_RAM_Activa()` → Marca las celdas activas de la RAM.  
- `SimularPipelineDinamico()` → Muestra la animación del pipeline.  

---

## 📊 6. Resultados

El simulador desarrollado permite ejecutar de manera controlada e independiente las principales funciones de una arquitectura x86 simplificada.
 A través del primer botón de “Ejecutar”, los usuarios pueden observar cómo las instrucciones —como MOVE, SUMA y RESTA— modifican los valores del acumulador (AC), los registros, la memoria RAM y los flags asociados.
De forma complementaria, mediante un segundo control o botón, se activa la animación del pipeline, la cual representa de manera visual el recorrido de las instrucciones a través de las etapas del procesador.
 Aunque ambas funciones operan de manera separada, su ejecución conjunta aunque no se puede sincronizar perfectamente por la velocidad de la animación del pipeline permite comprender la relación entre la lógica interna del CPU y el flujo teórico de instrucciones dentro del pipeline.
Durante las pruebas, se verificó que la actualización de registro sea coherente con las operaciones ejecutadas, y que la representación visual del pipeline contribuye a reforzar la comprensión conceptual del paralelismo y las etapas de ejecución, aun cuando no exista sincronización directa entre ambas simulaciones.


---

## 7. Conclusiones

 El desarrollo del Simulador de Arquitectura x86 en Excel VBA permitió demostrar que es posible representar de forma didáctica y funcional los principios fundamentales de la arquitectura de computadoras.
 A través de su implementación, el equipo integró conceptos teóricos como el ciclo de instrucción, la organización de la CPU, la ALU, los registros, la memoria RAM, la caché y el pipeline, transformándolos en una herramienta visual e interactiva.
La aplicación no solo cumple los objetivos técnicos planteados, sino que también fortalece el proceso de aprendizaje, al ofrecer una experiencia práctica que permite observar el flujo de ejecución y la relación entre hardware y software.
 Asimismo, el proyecto fomenta la colaboración interdisciplinaria, el uso de herramientas modernas de control de versiones (GitHub) y la aplicación de metodologías ágiles mediante historias de usuario, reflejando un enfoque profesional en su desarrollo.
Finalmente, el simulador se consolida como un recurso educativo accesible y expandible, capaz de apoyar el estudio de la arquitectura x86 y servir de base para futuras mejoras, como la incorporación de detección de riesgos en el pipeline, políticas avanzadas de reemplazo de caché o la traducción de código C a ensamblador.

---
