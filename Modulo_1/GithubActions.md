# GitHub Actions

GitHub Actions es una plataforma de GitHub que permite implementar flujos de trabajo de integración y entrega continua (CI/CD).

- **CI (Integración Continua):** Automatiza la integración de cambios en el código.
- **CD (Entrega/Despliegue Continua):** Automatiza el despliegue de aplicaciones.

---

### Conceptos clave

- **Workflow:** Archivo YAML que define un conjunto de acciones automatizadas que se ejecutan en respuesta a eventos.
- **Evento (Trigger):** Suceso que inicia la ejecución de un workflow (por ejemplo, un push o pull request).
- **Job:** Conjunto de pasos que se ejecutan en un runner. Un workflow puede tener varios jobs, que pueden ejecutarse en paralelo o en secuencia.
- **Step:** Acción individual dentro de un job. Cada step ejecuta un comando o una acción.
- **Action:** Bloque de código reutilizable que realiza una tarea específica dentro de un step.
- **Runner:** Entorno donde se ejecutan los jobs (puede ser proporcionado por GitHub o **auto-hospedado**).

---

### Contextos en GitHub Actions

Los **contextos** en GitHub Actions proporcionan información y variables sobre el entorno de ejecución, el repositorio, el workflow, los jobs y los eventos. Se accede a los contextos usando la sintaxis `${{ <contexto>.<propiedad> }}`.

Algunos contextos comunes:

- **github:** Información sobre el repositorio, el evento y el actor (por ejemplo, `${{ github.repository }}`, `${{ github.ref }}`).
- **env:** Variables de entorno definidas en el workflow o en los jobs.
- **job:** Información sobre el job actual (por ejemplo, `${{ job.status }}`).
- **steps:** Resultados de steps anteriores (por ejemplo, `${{ steps.<id>.outputs.<output> }}`).
- **runner:** Información sobre el runner (por ejemplo, `${{ runner.os }}`).
- **secrets:** Acceso a secretos definidos en el repositorio (por ejemplo, `${{ secrets.MY_SECRET }}`).

#### Ejemplo de uso de contextos

```yaml
jobs:
	ejemplo-contextos:
		runs-on: ubuntu-latest
		steps:
			- name: Mostrar información de contexto
				run: |
					echo "Repositorio: ${{ github.repository }}"
					echo "Rama: ${{ github.ref }}"
					echo "Sistema operativo: ${{ runner.os }}"
```

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

---

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

---

### Condicionales en GitHub Actions

Puedes usar la clave `if` para ejecutar jobs o steps solo si se cumple una condición.

#### Ejemplo de uso de condicionales

```yaml
jobs:
	build:
		runs-on: ubuntu-latest
		steps:
			- name: Ejecutar solo en ramas main o develop
				if: github.ref == 'refs/heads/main' || github.ref == 'refs/heads/develop'
				run: echo "Este step solo se ejecuta en main o develop"
```

---