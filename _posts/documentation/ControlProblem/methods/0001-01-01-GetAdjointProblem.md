---
title: GetAdjointProblem
url: /documentation/MDL01/ControlProblem/GetAdjointProblem
data: 
  little_description: Metodo capaz de calcular el problema adjunto de la ecuacion diferencial atravez del hamiltoniano
                       asociado (Principi de Pontriagin). Mediante la formula $ \frac{d\textbf{P}}{dt} = \vec{\nabla}_{Y} H $
  description: Este metodo agrega el problema adjunto al objecto ControlProblem, dado que tenemos 
                $$ \dot{\textbf{Y}} = f(\textbf{Y},t) $$ 
                y el funcional 
                $$ J = \Psi(\textbf{Y}(T)) + \int_{0}^T L(\textbf{Y},U,t)dt $$ 
                podemos crear el Hamiltoniano 
                $$ H = L + P*F $$
                donde $\textbf{P} = [p_1 p_2 p_3 ... ]^T$ . Entonces 
                segun el principio del maximo de pontriagin 
                podemos calcular el problemas adjunto mediantes las formulas 
                $$ \frac{d\textbf{P}}{dt} = \vec{\nabla}_{Y} H = 
                (\frac{\partial H}{ \partial y_1},\frac{\partial H}{ \partial y_2},...)$$
                con la condicion final 
                $$ \textbf{P}(T) = 
                (\frac{\partial \Psi}{ \partial y_1},\frac{\partial \Psi}{ \partial y_2},...)$$
  autor: JOroya
  MandatoryInputs:   
     iCP: 
         name: Control Problem
         description: Control problem object
         class: ControlProblem
         dimension: [1x1]
  Outputs:
     iCP: 
         name: Control Problem
         description: Control problem object
         class: ControlProblem
         dimension: [1x1]
categories: [ documentation , MDL01 , ControlProblem]
layout: method
---
