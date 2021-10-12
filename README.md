# Visual-DaVinci
Entry course programs ._.

```Ruby
programa Cap7Pregunta9
procesos
  proceso recoger(ES PAPELES:numero;ES FLORES:numero)
  comenzar
    mientras((HayPapelEnLaEsquina)|(HayFlorEnLaEsquina))
      si(HayPapelEnLaEsquina)
        tomarPapel
        PAPELES:=PAPELES+1
      si(HayFlorEnLaEsquina)
        tomarFlor
        FLORES:=FLORES+1
  fin
  proceso rectangulo(E ANCHO:numero;E LADO:numero;ES NumPapeles:numero;ES NumFlores:numero)
  comenzar
    repetir 2
      repetir ANCHO
        recoger(NumPapeles,NumFlores)
        mover
      derecha
      repetir LADO
        recoger(NumPapeles,NumFlores)
        mover
      derecha
  fin
areas
  ciudad:AreaC(1,1,100,100)
robots
  robot robot1
  variables
    ancho,lado,cero:numero
    papeles,flores:numero
  comenzar
    papeles:=0
    flores:=0
    cero:=-2
    ancho:=1
    lado:=13
    repetir 7
      rectangulo(ancho,lado,papeles,flores)
      lado:=lado+cero
      Pos(1,PosCa+2)
    Informar(papeles,flores)
  fin
variables
  R-Info:robot1
comenzar
  AsignarArea(R-Info,ciudad)
  Iniciar(R-Info,1,1)
fin
```
