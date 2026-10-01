# RFP — Modernización de Plataforma de Datos y Analítica

**Cliente ficticio:** Financiera Andina S.A.  
**Documento:** RFP-DEMO-001  
**Versión:** 1.0  
**Clasificación:** Synthetic demo data — not real customer information

## 1. Contexto

Financiera Andina opera actualmente una plataforma analítica on-premises soportada por bases de datos Oracle y SQL Server, archivos intercambiados por SFTP y algunas APIs REST. La organización busca modernizar esta plataforma sobre Google Cloud para reducir tiempos de disponibilidad de información, mejorar gobierno, trazabilidad y automatización del ciclo de entrega.

## 2. Objetivo

Diseñar e implementar una plataforma de datos y analítica en Google Cloud que permita migrar progresivamente las cargas actuales, habilitar ingestión batch y de baja latencia, fortalecer gobierno y seguridad, y establecer prácticas repetibles de CI/CD e Infraestructura como Código.

## 3. Alcance técnico

1. Migración inicial de 40 interfaces de origen.
2. Fuentes: Oracle, SQL Server, archivos CSV/SFTP y APIs REST.
3. Aproximadamente 120 pipelines ETL existentes deberán ser evaluados, racionalizados y migrados cuando corresponda.
4. Volumen actual estimado: 8 TB de información analítica.
5. La mayoría de fuentes se procesa diariamente.
6. Cuatro fuentes críticas requieren disponibilidad de datos en un máximo de 5 minutos desde su generación.
7. La plataforma debe soportar datos estructurados y semi-estructurados.
8. Se requieren ambientes Dev, QA y Producción.

## 4. Seguridad y cumplimiento

1. La solución procesará información de identificación personal y datos financieros.
2. La información debe estar cifrada en tránsito y en reposo.
3. Los accesos a Producción deben ser basados en roles y auditables.
4. Las bases de datos de origen no deben exponerse directamente a Internet pública.
5. La solución deberá utilizar prácticas de mínimo privilegio.

## 5. Gobierno de datos

1. Se requiere catálogo gobernado de datos.
2. Debe existir trazabilidad/linaje para datasets críticos.
3. La propuesta debe describir cómo se incorporarán controles de calidad de datos.
4. Los periodos de retención pueden variar por dominio y deberán definirse durante el proyecto.

## 6. DevSecOps y operación

1. CI/CD es obligatorio para pipelines y cambios de infraestructura.
2. Infraestructura como Código es obligatoria.
3. Debe existir monitoreo, logging y alertamiento centralizado.
4. La solución deberá contemplar documentación operativa y transferencia de conocimiento.

## 7. Continuidad

Para los servicios analíticos críticos se solicita:

- RTO objetivo: 4 horas.
- RPO objetivo: 1 hora.

La región específica para recuperación ante desastre será definida durante el diseño detallado.

## 8. Plazo

El cliente espera completar el alcance inicial en aproximadamente 16 semanas.

## 9. Entregables esperados

La propuesta deberá incluir como mínimo:

- entendimiento del alcance;
- arquitectura propuesta;
- explicación de decisiones de arquitectura;
- plan de implementación;
- WBS y cronograma;
- equipo/roles requeridos;
- supuestos y exclusiones;
- dependencias del cliente;
- propuesta económica para implementación;
- opción separada de soporte posterior;
- documentación y handoff operativo.

## 10. Información aún por confirmar

La siguiente información será precisada en rondas de preguntas y respuestas:

- crecimiento anual esperado del volumen de datos;
- concurrencia máxima de usuarios BI;
- región objetivo para DR;
- tecnologías específicas de las cuatro fuentes de baja latencia;
- inventario detallado de reglas de calidad existentes;
- cantidad de reportes/dashboards que requieren remediación;
- retención por dominio;
- RACI para cambios requeridos en sistemas fuente.

## 11. Evaluación de la propuesta

Se valorará:

1. claridad del entendimiento;
2. trazabilidad entre requerimientos y diseño;
3. uso de patrones y estándares de arquitectura justificables;
4. transparencia de supuestos y dependencias;
5. consistencia entre solución, esfuerzo, cronograma y precio;
6. capacidad de transferencia y operación posterior.
