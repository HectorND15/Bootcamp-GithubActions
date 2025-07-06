# GitHub Actions

GitHub Actions es una plataforma de GitHub que permite implementar flujos de trabajo de integración y entrega continua (CI/CD).

- **CI (Integración Continua):** Automatiza la integración de cambios en el código.
- **CD (Entrega/Despliegue Continua):** Automatiza el despliegue de aplicaciones.

### Conceptos clave

- **Workflow:** Archivo YAML que define un conjunto de acciones automatizadas que se ejecutan en respuesta a eventos.
- **Evento (Trigger):** Suceso que inicia la ejecución de un workflow (por ejemplo, un push o pull request).
- **Job:** Conjunto de pasos que se ejecutan en un runner. Un workflow puede tener varios jobs, que pueden ejecutarse en paralelo o en secuencia.
- **Step:** Acción individual dentro de un job. Cada step ejecuta un comando o una acción.
- **Action:** Bloque de código reutilizable que realiza una tarea específica dentro de un step.
- **Runner:** Entorno donde se ejecutan los jobs (puede ser proporcionado por GitHub o **auto-hospedado**).

---

### Ejemplo CI Workflow

```yaml
name: CI
on:
	push:
		branches: [ main ]

jobs: 
	build:
		runs-on: ubuntu-latest

		steps:
			- name: Checkout repository
				uses: actions/checkout@v3
			
			- name: Configurar Node.js
				uses: actions/setup-node@v3
				with:
					node-version: '18'
```