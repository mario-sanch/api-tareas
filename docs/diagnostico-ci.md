# Laboratorio de integración continua

<!-- Al terminar, este archivo va al repositorio como docs/diagnostico-ci.md (guía de laboratorio del Tema 3, Parte 3). -->

> **Cómo completar esta plantilla**
>
> Cada texto que está entre los signos **menor que** y **mayor que** se reemplaza por lo que se pide,
> incluidos los dos signos. El resto queda como está.
>
> | Signo | Nombre    |
> | :---: | --------- |
> |  `<`  | menor que |
> |  `>`  | mayor que |
>
> Ejemplo, con `mi-usuario` en lugar del usuario de GitHub:
>
> | En la plantilla                                       | Ya completado                                          |
> | ----------------------------------------------------- | ------------------------------------------------------ |
> | `https://github.com/<usuario>/api-tareas/tree/lab-ci` | `https://github.com/mi-usuario/api-tareas/tree/lab-ci` |
>
> En la vista previa, algunos de esos textos no se muestran, porque se leen como código HTML. En el editor
> siempre se ven.

## 1. Enlaces

| Qué                                                         | Enlace                                              |
| ----------------------------------------------------------- | --------------------------------------------------- |
| Repositorio en el tag `lab-ci`                              | https://github.com/<usuario>/api-tareas/tree/lab-ci |
| Pull request que el check bloqueó (prueba rota a propósito) | https://github.com/mario-sanch/api-tareas/pull/5    |

## 2. Diagnóstico de los tres pipelines rotos

### Caso 1

**Síntoma** (el paso que falló primero y su mensaje, copiado del log como texto):

```text
Pruebas: No module named pytest
```

**Causa:** No se instalo el paquete pytest con su version

**Corrección:** Se agrego la libreria pytest con su version respectiva · Commit: https://github.com/mario-sanch/api-tareas/pull/6/changes/4ef8e3590940df5238f959e0f28831b69ae04977

**Prevención:** exigir el check de CI en el ruleset y revisar en el diff del pull request que las librerias que se van a instalar lleven la version correspondiente

### Caso 2

**Síntoma** (el paso que falló primero y su mensaje, copiado del log como texto):

```text
Error: No files were found with the provided path: reporte/. No artifacts will be uploaded.
```

**Causa:** La ruta del campo path para el artefacto de reportes esta mal escrita

**Corrección:** Se corrige la ruta del artefacto de reportes · Commit: https://github.com/mario-sanch/api-tareas/commit/fbc9153dccd7321a704007f37de44c1727d73611

**Prevención:** exigir en el rule set que solo se haga merge si los checks estan en verde

### Caso 3

**Síntoma** (el paso que falló primero y su mensaje, copiado del log como texto):

```text
ERROR tests/test_datos_ejemplo.py::test_carga_las_tareas_de_ejemplo - FileNotFoundError: [Errno 2] No such file or directory: '/home/runner/work/api-tareas/api-tareas/tests/datos/tareas_ejemplo.json
```

**Causa:** El archivo .gitignore agrega el patron \*.json por lo que el archivo tareas_ejemplo.json queda fuera del comit

**Corrección:** Se quita el patron \*.json de .gitignore · Commit: https://github.com/mario-sanch/api-tareas/commit/6cc1636f5358f195b06151c47bd9e2839af64f3b

**Prevención:** Evitar patrones amplios como \*.json en .gitignore y verificar en las diferencias del commit que los archivos de datos para las pruebas queden trackeados.

## 3. Uso de IA

No se usó IA.
