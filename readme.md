# [BAZ | Wizeline] Demo OpenRewrite

## Parte 1 - Ejecutar una receta

Para este demo de OpenRewrite, se deben de seguir los siguientes pasos:

1. En el archivo `pom.xml`, en la sección de `<plugins>`, se debe de agregar la dependencia de OpenRewrite:
```
<plugin>
    <groupId>org.openrewrite.maven</groupId>
    <artifactId>rewrite-maven-plugin</artifactId>
    <version>6.0.5</version>
</plugin>
```

2. Una vez agregada la dependencia, hay que obtener la lista de las recetas disponibles, ejecutando el siguiente comando en la línea de comandos:
```
./mvnw rewrite:discover
```

3. De regreso en el archivo `pom.xml`, dentro de la dependencia de OpenRewrite se debe de agregar la receta a ejecutar, quedando todo el elemento de OpenRewrite como sigue:
```
<plugin>
    <groupId>org.openrewrite.maven</groupId>
    <artifactId>rewrite-maven-plugin</artifactId>
    <version>6.0.5</version>
    <configuration>
        <activeRecipes>
            <recipe>org.openrewrite.java.format.AutoFormat</recipe>
            <recipe>org.openrewrite.java.OrderImports</recipe>
        </activeRecipes>
    </configuration>
</plugin>
```

4. Para aplicar las recetas, en la línea de comandos hay que ejecutar el comando
```
./mvnw rewrite:run
```

## Parte 2 - Recetas con configuración

El objetivo de esta parte es cambiar el nombre a un paquete (package) utilizando la receta `org.openrewrite.java.ChangePackage`.

Hay que cambiar el nombre del paquete `org.springframework.samples.petclinic.vet` por el nombre `org.springframework.samples.petclinic.veterinary`

1. Crear el archivo `rewrite.yml` en la raíz del directorio con el siguiente contenido:
```
---
type: specs.openrewrite.org/v1beta/recipe
name: com.bancoazteca.VetToVeterinary
recipeList:
  - org.openrewrite.java.ChangePackage:
      oldPackageName: org.springframework.samples.petclinic.vet
      newPackageName: org.springframework.samples.petclinic.veterinary
```

2. Obtener las recetas disponibles y verificar que la receta `com.bancoazteca.VetToVeterinary` existe en la lista
```
./mvnw rewrite:discover
```

3. Agregar la receta en el archivo `pom.xml`
```
<recipe>com.bancoazteca.VetToVeterinary</recipe>
```

4. Ejecutar la receta
```
./mvnw rewrite:run
```
