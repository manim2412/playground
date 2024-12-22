## [manim tutorial link](https://docs.manim.community/en/stable/tutorials/quickstart.html)

# 1. Animating a circle
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


# 2. Transforming a square into a circle
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

  
# 3. Positioning <code>Mobject</code>s
**[input]**
```python
from manim import *

class SquareAndCircle(Scene):
    def construct(self):
        circle = Circle()  
        circle.set_fill(PINK, opacity=0.5)  

        square = Square()
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

   
# 4. (1) Using <code>.animate</code> syntax to animate methods
**[input]**
```python
from manim import *

class AnimatedSquareToCircle(Scene):
    def construct(self):
        circle = Circle()  
        square = Square()  

        self.play(Create(square))  
        self.play(square.animate.rotate(PI / 4))  
        self.play(Transform(square, circle))  
        self.play(
            square.animate.set_fill(PINK, opacity=0.5)
        )  
```  
**[command line]**
```python
manim -pql scene.py AnimatedSquareToCircle
```
**[output]**  
[AnimatedSquareToCircle youtube](https://youtu.be/6ho6almFkoA)  


# 4. (2) Using <code>.animate</code> syntax to animate methods
**[input]**
```python
from manim import *

class DifferentRotations(Scene):
    def construct(self):
        left_square = Square(color=BLUE, fill_opacity=0.7).shift(2 * LEFT)
        right_square = Square(color=GREEN, fill_opacity=0.7).shift(2 * RIGHT)
        self.play(
            left_square.animate.rotate(PI), Rotate(right_square, angle=PI), run_time=2
        )

        self.wait()
```  
**[command line]**
```python
manim -pql scene.py DifferentRotations
```
**[output]**  
[DifferentRotations youtube](https://youtu.be/KkxieJMFGLI)
***

     
# 5. (1) <code>Transform</code> vs <code>ReplacementTransform</code>
**[input]**
```python
from manim import *

class TwoTransforms(Scene):
    def transform(self):
        a = Circle()
        b = Square()
        c = Triangle()
        self.play(Transform(a, b))
        self.play(Transform(a, c))
        self.play(FadeOut(a))

    def replacement_transform(self):
        a = Circle()
        b = Square()
        c = Triangle()
        self.play(ReplacementTransform(a, b))
        self.play(ReplacementTransform(b, c))
        self.play(FadeOut(c))

    def construct(self):
        self.transform()
        self.wait(0.5)
        self.replacement_transform()
```  
**[command line]**
```python
manim -pql scene.py TwoTransforms
```
**[output]**  
[TwoTransforms youtube](https://youtu.be/rDXPozUKzRs)


# 5. (2) <code>Transform</code> vs <code>ReplacementTransform</code>
**[input]**
```python
from manim import *

class TransformCycle(Scene):
    def construct(self):
        a = Circle()
        t1 = Square()
        t2 = Triangle()
        self.add(a)
        self.wait()
        for t in [t1,t2]:
            self.play(Transform(a,t))
```  
**[command line]**
```python
manim -pql scene.py TransformCycle
```
**[output]**  
[TransformCycle youtube](https://youtu.be/eYuxKHhh82I)



