<div align="center">

[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/Nomadiix/EPA)
[![GitHub stars](https://img.shields.io/github/stars/Nomadiix/EPA)](https://github.com/FabianMartinez1234567/EPA/stargazers/)
[![GitHub repo size in bytes](https://img.shields.io/github/repo-size/Nomadiix/EPA)](https://github.com/Nomadiix/EPA)
 </div>

<h1 align="center"> 💻EPA  </h1>
<div align="center">
  <img src="https://media.giphy.com/media/YnYpT4OL4pFVrBMc9R/giphy.gif"/>
 </div>

<h3 align='center'>
<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%"> <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMGxnMjNvcXFvM3cyOGY1MXIwanNlbHo3cjBnY243MjBoYmpseXppcyZjdD1z/JwOUH7TbHFHg3LnX18/giphy.gif" height="25" />  Indice  <img style="transform:scaleX(-1);" src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMGxnMjNvcXFvM3cyOGY1MXIwanNlbHo3cjBnY243MjBoYmpseXppcyZjdD1z/JwOUH7TbHFHg3LnX18/giphy.gif" height="25" />

</h3>

- [Capitulo N°1](/Capitulo%20N%C2%B01/)
- [Capitulo N°2](/Capitulo%20N%C2%B02/)
- [Capitulo N°3](/Capitulo%20N%C2%B03/)
- [Capitulo N°4](/Capitulo%20N%C2%B04/)
- [Capitulo N°5](/Capitulo%20N%C2%B05/)
- [Capitulo N°6](/Capitulo%20N%C2%B06/)
- [Capitulo N°7](/Capitulo%20N%C2%B07/)

<img src= 'https://i.gifer.com/origin/8c/8cd3f1898255c045143e1da97fbabf10_w200.gif' height="20" width="100%"> 

<div align='center'>

## 🤖Codigo de R-INFO

</div>

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
