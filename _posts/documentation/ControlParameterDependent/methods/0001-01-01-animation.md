---
title: animation
data: 
  description: This method allows us to see an animation of the evolution of gradient methods, shows the controls
                    in each iteration with a lapse of $dt=0.15s$
  little_description: This method allows us to see an animation of the evolution of gradient methods, 
                        shows the controls in each iteration with a lapse of $dt=0.15s$
  autor: JOroya
  MandatoryInputs:   
   iCPD: 
     description: Control Parameter Dependent Problem
     class: ControlParameterDependent
     dimension: [1x1]
  OptionalInputs:
    figure: 
     description: figure where is the animation
     class: figure
     dimension: [1x1]
     default: []
    XLim: 
     description: axes YLim of Vector State 
     class: double
     dimension: [1x2]
     default: []
    ULim: 
     description: axes YLim of Vector Control 
     class: double
     dimension: [1x2]
     default: []
    JLim: 
     description: axes YLim of Functional Convergence 
     class: double
     dimension: [1x2]
     default: []
    SaveGif: 
     description: if this option is true, so the animation is save in gif format
     class: boolean
     dimension: [1x1]
     default: false
    path: 
     description: Name of file where the Gif will be saved
     class: string
     dimension: [1x1]
     default: ' '
    dt: 
     description: Interval of time between capture 
     class: double
     dimension: [1x1]
     default: 0.15
categories: [ documentation , MDL01 , ControlParameterDependent]
class: ControlParameterDependent
layout: method
---
