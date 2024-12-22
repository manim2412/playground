# [manim tutorial link](https://docs.manim.community/en/stable/tutorials/quickstart.html)

1. Animating a circle


**[input]**
```python
from manim import *

class CreateCircle(Scene):
    def construct(self):
        circle = Circle()
        circle.set_fill(PINK, opacity=0.5)
        self.play(Create(circle))
```  
**[command line]**
```python
manim -pql scene.py CreateCircle
```
**[output]**  
[CreateCircle youtube](https://youtu.be/a6TyJKwqiTc){:target="_blank"}
***
<a href="https://www.youtube.com" target="_blank">YouTube</a>


2. Transforming a square into a circle


**[input]**
```python
from manim import *

class SquareToCircle(Scene):
    def construct(self):
        circle = Circle()  
        circle.set_fill(PINK, opacity=0.5)  

        square = Square()  
        square.rotate(PI / 4)  

        self.play(Create(square))  
        self.play(Transform(square, circle))  
        self.play(FadeOut(square))  
```  
**[command line]**
```python
manim -pql scene.py SquareToCircle
```
**[output]**  
[SquareToCircle youtube](https://youtu.be/iypJjYoq1YQ)
***


  
3. Positioning <code>Mobject</code>s


**[input]**
```python
from manim import *

class SquareAndCircle(Scene):
    def construct(self):
        circle = Circle()  
        circle.set_fill(PINK, opacity=0.5)  

        square = Square()  # create a square
        square.set_fill(BLUE, opacity=0.5)  

        square.next_to(circle, RIGHT, buff=0.5) 
        self.play(Create(circle), Create(square))  
```  
**[command line]**
```python
manim -pql scene.py SquareAndCircle
```
**[output]**  
[SquareAndCircle youtube](https://youtu.be/m2E5gCw8gzA)
***

   
6. Using <code>.animate</code> syntax to animate methods


**[input]**
```python
from manim import *

class CreateCircle(Scene):
    def construct(self):
        circle = Circle()
        circle.set_fill(PINK, opacity=0.5)
        self.play(Create(circle))
```  
**[command line]**
```python
manim -pql scene.py CreateCircle
```
**[output]**  
[CreateCircle youtube](https://youtu.be/a6TyJKwqiTc)
***

     
7. <code>Transform</code> vs <code>ReplacementTransform</code>


**[input]**
```python
from manim import *

class CreateCircle(Scene):
    def construct(self):
        circle = Circle()
        circle.set_fill(PINK, opacity=0.5)
        self.play(Create(circle))
```  
**[command line]**
```python
manim -pql scene.py CreateCircle
```
**[output]**  
[CreateCircle youtube](https://youtu.be/a6TyJKwqiTc)



