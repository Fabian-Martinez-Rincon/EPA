<h1 align="center"> 💻EPA  </h1>

> [!IMPORTANT]  
> Podes usar los pdfs y guiarte con los ejercicios resueltos en el repositorio para estudiar y practicar. Yo utilizo el visual studio code para programar y despues abro el archivo en el R-INFO para ejecutar el codigo.

---

## Paso 1 Descargar el R-Info

![alt text](/imagenes/image.png)

## Paso 2 (Si no pueden abrir el R INFO)

Descargar e instalan este [https://www.java.com/es/download/manual.jsp](https://www.java.com/es/download/manual.jsp)

![alt text](/imagenes/image-1.png)

## Paso 3 Descargar VSCODE

[https://code.visualstudio.com/download](https://code.visualstudio.com/download)

![alt text](/imagenes/image-2.png)

## Paso 4 Instalar extención

Van a logo ese de la derecha abajo de todo casi y buscan la extencion de R-INFO

![alt text](/imagenes/image-3.png)

## Paso 5 Se crean un archivo ´ejemplo.ri´ y pegan lo siguiente

```
programa ejemplo

procesos
  proceso cuadrado (E lado: numero)
  comenzar
    {el lado tiene tantas cuadras como indica largo}
    repetir 4
      repetir lado
        mover
      derecha
  fin

areas
  ciudad: AreaC(1,1,100,100)

robots
  robot robot1
  variables
    largo: numero
  comenzar
    {valor inicial, el primer cuadrado es de uno}
    largo := 1
    repetir 4
      cuadrado(largo)
      {se incrementa el valor que indica el largo del lado}
      largo := largo + 1
  fin

variables
  R-info: robot1

comenzar
  AsignarArea(R-info, ciudad)
  Iniciar(R-info, 1, 1)
fin
```

## Paso 6 A practicar!!

![alt text](/imagenes/image-4.png)