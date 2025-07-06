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

### La directiva `needs`

La directiva `needs` permite definir dependencias entre jobs dentro de un workflow, asegurando que un job no comience hasta que los jobs de los que depende hayan finalizado correctamente.

#### Ejemplo de uso de `needs`

```yaml
jobs:
	build:
		runs-on: ubuntu-latest
		steps:
			- name: Checkout repository
				uses: actions/checkout@v3

	test:
		runs-on: ubuntu-latest
		needs: build
		steps:
			- name: Ejecutar pruebas
				run: echo "Ejecutando pruebas después de build"
```
En este ejemplo, el job `test` solo se ejecutará después de que el job `build` haya finalizado con éxito.