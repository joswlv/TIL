#Codewars #21
##Question
Description:

In this kata, you should calculate type of triangle with three given sides a, b and c (given in any order).

If all angles are less than 90°, this triangle is acute and function should return 1.

If one angle is strictly 90°, this triangle is right and function should return 2.

If one angle more than 90°, this triangle is obtuse and function should return 3.

If three sides cannot form triangle, or one angle is 180° (which turns triangle into segment) - function should return 0.

Input parameters are sides of given triangle. All input values are non-negative floating point or integer numbers (or both).

Examples:

```
triangle_type(2, 4, 6) # return 0 (Not triangle)
triangle_type(8, 5, 7) # return 1 (Acute, angles are approx. 82°, 38° and 60°)
triangle_type(3, 4, 5) # return 2 (Right, angles are approx. 37°, 53° and exactly 90°)
triangle_type(7, 12, 8) # return 3 (Obtuse, angles are approx. 34°, 106° and 40°)
```

[link](https://www.codewars.com/kata/triangle-type/python)

#My Soultion

```python
# Should return triangle type:
#  0 : if triangle cannot be made with given sides
#  1 : acute triangle
#  2 : right triangle
#  3 : obtuse triangle

def triangle_type(a, b, c):
  x,y,z = sorted([a,b,c])
  if z >= x + y: return 0
  if z*z == x*x + y*y: return 2
  return 1 if z*z < x*x + y*y else 3
```
피타고라스의 정리를 사용하여 삼각형 유형을 결정하였다. 그리고 학습한 삼항연산을 사용했다.