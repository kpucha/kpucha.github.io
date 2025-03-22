---
title: 'Spring y Angular en Monorepo de GitHub: Seguridad, Colaboración y CI/CD con Caché'
categories:
- Proyectos
- NeuronForge
tags:
- GitHub
- Java
- Spring Boot
- Angular
image: "/assets/img/headers/github-submodulos.png"
---

## 1. Creación y Organización de los Repositorios

### 1.1. Repositorios del proyecto
Lo primero que vamos a necesitar es crear 3 repositorios de GitHub. 

- **Frontend:**  
  Contiene la aplicación Angular y la configuración de CI (usando npm y cache).
	
- **Backend:**  
  Contiene la aplicación Spring Boot  y la configuración de CI (usando Maven y cache).  
- **Repositorio Principal:**  
  Funciona como hub central de documentación, coordinación y configuración común.  

### 1.2. Vinculación mediante Submódulos

Utilizar submódulos te permitirá versionar y sincronizar las versiones exactas del backend y frontend, además de compartir configuraciones y secrets comunes a través del repositorio principal.

#### 1.2.1 Configuración de Submódulos

##### Clona el repositorio principal:
   ```bash
   git clone https://github.com/usuario/repositorio-principal.git
   cd repositorio-principal
   ```
##### Agrega los repositorios como submódulos:
   ```bash
   git submodule add https://github.com/usuario/repositorio-back.git repositorio-backend
   git submodule add https://github.com/usuario/repositorio-front.git repositorio-frontend
   ```
   
   Con esto obtendrás la siguiente estructura:
   ```
   repositorio-principal/
   ├── repositorio-backend/           <-- Submódulo de repositorio-backend
   ├── repositorio-frontend/          <-- Submódulo de repositorio-frontend
   └── README.md
   ```
##### Para clonar con submódulos:
   Los colaboradores deberán usar:
   ```bash
   git clone --recurse-submodules https://github.com/usuario/repositorio-principal.git
   ```
   O, si ya se clonó sin submódulos:
   ```bash
   git submodule update --init --recursive
   ```

### 1.3. Creación de los proyectos base

#### 1.3.1 Crear y Subir el Proyecto Angular al Repositorio Existente

##### Ve al repositorio remoto ya creado (con README.md)
```powershell
cd repositorio-frontend
```
##### Crea el proyecto Angular dentro del repositorio clonado
```powershell
# Borra el README.md para que Angular no reviente al generar el proyecto
rm .\README.md  
# Vuelve a la carpeta anterior
cd ..
# Instala npm si no lo tenias ya
npm install -g @angular/cli
# Genera el proyecto para frontend con Angular 
ng new repositorio-frontend --routing --style=scss --skip-git
# Ve al repositorio
cd repositorio-frontend
# Arranca la aplicación en una ventana emergente
ng serve -o
# Comprobar que se abre la ventana con nuestra app angular
# Ctrl + c para cancelar el proceso
```

##### Realiza el commit inicial y subelo a GitHub
```
git add .
git commit -m "Inicialización del proyecto frontend con Angular"
git push origin main
```
 ##### Vuelve al repositorio princial
```powershell
cd ..
```
 #### 1.3.2 Crear y Subir el Proyecto Spring al Repositorio Existente
##### Ve al repositorio remoto ya creado (con README.md)
```powershell
cd repositorio-backend
```
##### Crea el proyecto Spring dentro del repositorio clonado

Ve a [Spring Initializr](https://start.spring.io) y crea un nuevo proyecto con las dependencias que necesites.
Descomprime el zip y copia el contenido dentro la carpeta repositorio-backend

##### Realiza el commit inicial y subelo a GitHub
```
git add .
git commit -m "Inicialización del proyecto backend con Spring"
git push origin main
```


---

## 2. Protección del Repositorio y Permisos

### 2.1. Protección de la Rama Principal (Branch Protection Rules)

**Objetivo:**  
- Garantizar que la rama `main` no se modifique directamente por usuarios no autorizados.  
- Forzar que los cambios se integren a través de pull requests, los cuales deben ser revisados y pasar todos los checks de CI.

**Pasos a seguir en cada repositorio:**

1. **Accede a Settings > Branches:**  
   En la página del repositorio en GitHub, haz clic en **Settings** y luego en **Branches**.

2. **Crear una Regla de Protección para `main`:**  
   - Haz clic en **Add rule** y en **Branch name pattern** escribe `main`.  
   - Activa las siguientes opciones:
     - **Require pull request reviews before merging:**  
       Obliga a que los cambios en `main` se integren mediante PRs que deben ser revisados y aprobados.
     - **Require status checks to pass before merging:**  
       Garantiza que los workflows de GitHub Actions (como tests y builds) se ejecuten y aprueben antes del merge.
     - **Include administrators (opcional):**  
       Para que incluso los administradores cumplan estas reglas.

3. **Guarda la regla.**

### 2.2. Configuración de Permisos de Colaboradores

**Objetivo:**  
- Permitir que solo colaboradores autorizados (con permisos Write o Admin) puedan hacer push directo.  
- Usuarios externos, sin esos permisos, podrán únicamente abrir issues y pull requests, asegurando que los cambios sean revisados.

**Pasos:**

1. En **Settings > Collaborators and teams** de cada repositorio, agrega a los colaboradores de confianza.  
2. Asegúrate de que usuarios externos no tengan permisos de escritura directa.

---

## 3. Configuración de GitHub Actions con Caché

Optimiza el tiempo de construcción y pruebas utilizando caché en los workflows de CI en cada repositorio.

### 3.1. Workflow para el Backend

En el repositorio **repositorio-backend**:

1. Crea la ruta:
   ```
   repositorio-backend/
   └── .github/
       └── workflows/
           └── ci.yml
   ```

2. Archivo `ci.yml`:
   ```yaml
   name: CI - Backend (Spring Boot)

   on:
     push:
       branches:
         - main
     pull_request:
       branches:
         - main

   jobs:
     build:
       runs-on: ubuntu-latest

       steps:
         - name: Checkout code
           uses: actions/checkout@v2

         - name: Set up JDK 21
           uses: actions/setup-java@v2
           with:
             java-version: '21'

         - name: Cache Maven dependencies
           uses: actions/cache@v2
           with:
             path: ~/.m2/repository
             key: ${{ runner.os }}-maven-${{ hashFiles('**/pom.xml') }}
             restore-keys: |
               ${{ runner.os }}-maven-

         - name: Build with Maven
           run: mvn clean install -DskipTests

         - name: Run unit tests
           run: mvn test
   ```
**Detalles:**  
La acción de caché almacena la carpeta `~/.m2/repository` basándose en el hash del `pom.xml`, evitando descargas repetitivas y reduciendo el tiempo de construcción.

### 3.2. Workflow para el Frontend 

En el repositorio **repositorio-frontend**:

1. Crea la ruta:
   ```
   repositorio-frontend/
   └── .github/
       └── workflows/
           └── ci.yml
   ```

2. Archivo `ci.yml`:
   ```yaml
   name: CI - Frontend (Angular)

   on:
     push:
       branches:
         - main
     pull_request:
       branches:
         - main

   jobs:
     build:
       runs-on: ubuntu-latest

       steps:
         - name: Checkout code
           uses: actions/checkout@v2

         - name: Set up Node.js
           uses: actions/setup-node@v2
           with:
             node-version: '16'

         - name: Cache Node.js dependencies
           uses: actions/cache@v2
           with:
             path: ~/.npm
             key: ${{ runner.os }}-npm-${{ hashFiles('**/package-lock.json') }}
             restore-keys: |
               ${{ runner.os }}-npm-

         - name: Install dependencies
           run: npm install

         - name: Run Angular tests
           run: npm run test -- --watch=false --browsers=ChromeHeadless

         - name: Build Angular project
           run: npm run build --prod
   ```
**Detalles:**  
El caché se configura para almacenar las dependencias de npm, basado en el `package-lock.json`, lo que acelera la instalación de paquetes en ejecuciones posteriores.

---
## 4. Validación de Versiones Compatibles entre Frontend y Backend
### 4.1. Objetivo
Asegurar que las versiones del frontend y backend sean compatibles antes de crear una nueva release.

### 4.2. Configuración del Workflow en el Repositorio Principal
En el repositorio neuron-forge, crea el archivo de workflow .github/workflows/version-validation.yml para validar las versiones de frontend y backend.

Contenido de version-validation.yml :
```yaml
name: Validación de Versiones - Frontend y Backend

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  validate_versions:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout código
        uses: actions/checkout@v2
        with:
          submodules: 'recursive'

      - name: Obtener la versión del backend
        run: |
          BACKEND_VERSION=$(xmllint --xpath "string(//project/version)" repositorio-backend/pom.xml)
          echo "BACKEND_VERSION=$BACKEND_VERSION" >> $GITHUB_ENV

      - name: Obtener la versión del frontend
        run: |
          FRONTEND_VERSION=$(node -p "require('./repositorio-frontend/package.json').version")
          echo "FRONTEND_VERSION=$FRONTEND_VERSION" >> $GITHUB_ENV

      - name: Validar que las versiones del backend y frontend coincidan
        run: |
          if [ "$BACKEND_VERSION" != "$FRONTEND_VERSION" ]; then
            echo "Error: Las versiones no coinciden. Backend: $BACKEND_VERSION, Frontend: $FRONTEND_VERSION"
            exit 1
          else
            echo "Las versiones son compatibles."
          fi

      - name: Crear una release si las versiones son compatibles
        if: success()
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: "v${{ github.run_number }}"
          release_name: "Release v${{ github.run_number }}"
          body: "Nueva release generada con backend y frontend validados."

```

---

## 5. Repositorio Principal y Flujo de Trabajo
El repositorio principal **repositorio-principal** actuará como hub central para la documentación, configuración común y coordinación entre frontend y backend. 

---

## Resumen Final
### Repositorios y Submódulos:
   - Repositorios separados para el backend, frontend y el repositorio principal, que conecta ambos mediante submódulos.
### Protección y Permisos:
   - Reglas de protección de ramas para evitar modificaciones directas en `main` y asegurar la revisión de PRs.
### GitHub Actions con Caché:
   - Workflows de CI con caché en el backend (Maven) y el frontend (npm) para optimizar tiempos de construcción.
### Validación de Versiones:
   - Un workflow en el repositorio principal asegura que las versiones del frontend y backend sean compatibles antes de crear una nueva release.
