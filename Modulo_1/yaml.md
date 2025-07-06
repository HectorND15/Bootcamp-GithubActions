# YAML y Workflows

## ¿Qué es YAML?
* **YAML** significa *YAML Ain't Markup Language*.
* Es un formato de serialización de datos, legible para humanos.

### Diferencias con JSON
- **Sintaxis:**
	- *YAML*: Más legible, menos símbolos (no requiere llaves ni comillas en la mayoría de los casos).
	- *JSON*: Sintaxis más estricta, requiere llaves `{}` y comillas.
- **Tamaño:**
	- *YAML*: Más compacto.
	- *JSON*: Más verboso.
- **Parsing:**
	- *YAML*: Más complejo.
	- *JSON*: Más sencillo.
- **Uso común:**
	- *YAML*: Configuración (GitHub Actions, Docker, Ansible, Kubernetes, etc.).
	- *JSON*: APIs, objetos JavaScript.

### Características principales
- Formato clave-valor.
- Indentación obligatoria con espacios (no usar tabs).
- Soporta varios tipos de datos (números, booleanos, listas, diccionarios, nulos).
- Permite texto multilínea.

### Herramientas que utilizan YAML
- GitHub Actions
- Ansible
- Docker
- Docker Compose
- Kubernetes

### Tipos de datos en YAML (ejemplo)
```yaml
# Primitivos
ciudad: Madrid
comillas: "123"
edad: 24
temperatura: 32.5
masa: 1e6
activo: true
verificado: yes
descripcion: null
comentario: ~

# Lista
colores: 
    - rojo
    - verde
    - azul

# Lista de valores
usuarios:
	- nombre: Ana
	  edad: 30
	- nombre: Luis
	  edad: 25

# Mapas/Diccionarios
persona: 
	nombre: Juan
	edad: 30
```
- Cabe resaltar que los string no necesariamente necesitan comillas, a menos que requieran salto de linea.
- Booleanos con true/false o yes/no.
- Las listas son muy utilizadas en estos tipos de archivo.
- Las listas de valores, pueden tener varios atributos por cada objeto en la lista.
- YAML tambien soporta diccionarios

#### Modificadores de String multilinea
```yaml
mensaje: |
	Hola, 
	Esto es un texto multilinea.
```

```yaml
texto: >
	Esta es una linea
	que continuara en la siguiente.
```

### Herencia 
En YAML podemos tener Herencia, con una sintaxis un poco peculiar.
```yaml
default: &defaults
	color: blue
	size: medium

item1:
	<<: *defaults
	color: red

item2:
	<<: *defaults
	size: small
```

### Ejemplo de docker compose
```yaml
version: '3.8'

services:
	web:
		image: nginx:alpine
		ports:
			- "80:80"
		volumes:
			- ./nginx.conf:/etc/nginx/nginx.conf
			- .:/var/www/html
	
	php:
		image: php:8.2-fpm
		volumes:
			- .:/var/www/html
```