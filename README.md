# 🏭 Registro y Validación de Producción Local (Agrozzi - Simulación Local)

Esta es una aplicación web simple, **totalmente local (offline)**, diseñada para simular el registro de producción y la posterior validación o firma de supervisores y validadores en un entorno de campo o planta. Los datos se almacenan directamente en el **navegador del usuario (LocalStorage)**.

La aplicación fue diseñada con un enfoque en la **portabilidad** y la **resiliencia** a problemas de almacenamiento, incluyendo la compresión de imágenes para manejar la cuota de LocalStorage.


---

## ✨ Características Principales

* **Registro de Producción:** Permite a un "Supervisor" registrar el nombre del material, la cantidad producida, tomar una foto de evidencia (con compresión automática) y firmar digitalmente.
* **Almacenamiento Local (Offline):** Todos los datos se guardan en el `localStorage` del navegador. Ideal para operar sin conexión a internet.
* **Reporte y Filtrado:** Visualización de un listado de todos los registros con capacidad de filtrar por el nombre del material.
* **Validación con Firma:** Los registros pueden ser validados (firmados) por un "Validador" diferente, cambiando su estado a **Validado**.
* **Exportación de Datos:**
    * Descarga de Reporte a **CSV (Excel)** con delimitador `;` (punto y coma).
    * Exportación de registros **individuales a PDF** (con firmas y foto).
    * Exportación de **todos los registros a un PDF Masivo** de múltiples páginas.
* **Gestión de Registros:** Funcionalidades de **Edición**, **Eliminación** y **Deshacer** la última eliminación.
* **Compresión Inteligente de Imágenes:** Las fotos de evidencia se comprimen automáticamente a un máximo de **800px** de ancho/alto con calidad JPEG 0.7 para evitar el error `QuotaExceededError` en LocalStorage.

---

## 🛠️ Tecnologías Utilizadas

Esta aplicación es un proyecto *Single-File Application* (SFA) y no requiere de un backend o servidor web para funcionar:

| Categoría | Tecnología | Uso Específico |
| :--- | :--- | :--- |
| **Diseño** | **Tailwind CSS** | Estilizado rápido y responsivo de la interfaz (clases integradas). |
| **Firma Digital** | **Signature Pad (4.x)** | Captura y manipulación de firmas en canvas. |
| **Generación de PDF** | **jsPDF** | Creación y manipulación del documento PDF final. |
| **Conversión HTML a Imagen** | **html2canvas** | Conversión del contenido HTML (incluyendo firmas e imágenes) a una imagen para el PDF. |
| **JavaScript Nativo** | - | Toda la lógica de la aplicación (CRUD de LocalStorage, Modales, Vistas, Exportación). |

---

## 🚀 Instalación y Uso

Dado que es un archivo HTML independiente que utiliza bibliotecas externas a través de CDN, la instalación es extremadamente sencilla.

### 1. Instalación

1.  Clona o descarga este repositorio:
    ```bash
    git clone [https://docs.github.com/es/repositories/creating-and-managing-repositories/quickstart-for-repositories](https://docs.github.com/es/repositories/creating-and-managing-repositories/quickstart-for-repositories)
    ```
2.  Navega al directorio clonado.

### 2. Ejecución

Simplemente **abre el archivo `registros.html`** en cualquier navegador web moderno (Chrome, Firefox, Safari, Edge).

La aplicación se cargará y estará lista para usar inmediatamente, sin necesidad de configuración adicional.

### 3. Flujo de Trabajo

1.  **Nuevo Registro:**
    * Rellena el **Nombre del Material** y la **Cantidad Producida**.
    * (Opcional) Carga una **Foto de Evidencia** (se comprimirá automáticamente).
    * Firma en el canvas de **Firma del Supervisor**.
    * Haz clic en **Guardar Registro**.
2.  **Ver Reporte:**
    * Haz clic en el botón **Ver Reporte** en la esquina superior derecha.
    * Aquí verás la lista, podrás **Filtrar por Material**, **Editar**, **Eliminar**, **Exportar Individualmente a PDF**, o iniciar el proceso de **Firma** (Validación).
3.  **Validar:**
    * En la vista de Reporte, haz clic en **Firmar** en un registro **Pendiente**.
    * Ingresa el **Nombre del Validador**.
    * Firma en el canvas de **Firma del Validador**.
    * Haz clic en **Firmar y Validar**.

---

## ⚠️ Notas Importantes (LocalStorage)

* **Datos Volátiles:** Los datos almacenados en `localStorage` son específicos del navegador y el dispositivo. **Si borras el caché o usas un navegador diferente, los datos se perderán.**
* **Compresión:** El límite de `localStorage` suele ser de 5MB. La función `compressAndConvertImage` ayuda a mitigar esto al reducir las imágenes a `800px` y calidad JPEG 0.7, pero el almacenamiento masivo de registros con imágenes sigue siendo limitado.
* **Compatibilidad PDF:** La exportación a CSV y PDF utiliza la función `pdf.output('blob')` de `jsPDF` y `Blob` para CSV, lo que garantiza una **mejor compatibilidad con navegadores móviles, especialmente Safari (iOS)**.

---

## 🤝 Contribución

¡Las contribuciones son bienvenidas! Si deseas mejorar la aplicación, corregir un error o agregar una característica:

1.  Haz un Fork del repositorio.
2.  Crea una nueva rama (`git checkout -b feature/nueva-funcionalidad`).
3.  Realiza tus cambios.
4.  Haz commit de tus cambios (`git commit -m 'feat: Añade nueva funcionalidad X'`).
5.  Sube la rama (`git push origin feature/nueva-funcionalidad`).
6.  Abre un *Pull Request*.
