# Worksheet 3: Earthquake Visualization

**Due: Monday, February 21, 11:59pm CDT**

For the worksheets in this course, we will provide a Markdown template in a repository that will be created for you through GitHub classroom.  You can clone this repository, directly edit your local copy with your answers, and then commit and push the file to complete the submission.  Alternatively, you can use GitHub's built-in Markdown editor and edit directly on your repository website without having to clone it locally. 

*Do not make a copy of the provided Markdown template and submit that instead.* Our grading scripts will be looking for `README.md` within the root folder of your repository.  You should modify this template directly without changing the filename.



## Q1: Useful Math

In this assignment, you will be dealing with earthquake data from the United States Geological Survey. As with any real-world dataset, the data have real-world units, which may not always match up with units we want to use for the data visualization. As such, there are a few handy practices commonly used when constructing visualizations from real-world data; one of the most common is normalization.

Normalization is the process of converting a number inside of an arbitrary range to a floating point number between 0.0 and 1.0, inclusive. For example, if we have a value `v = 1.5` in the list of numbers `[0.0, 1.5, 2.0, 1.3]`, the normalized value would be `vNormalized = 0.75`.

These two functions, part of the TypeScript Math library, will be useful for your first question: 

```typescript
/**
 * Returns the larger of a set of supplied numeric expressions.
 * @param values Numeric expressions to be evaluated.
 */
max(...values: number[]): number;

/* Returns the smaller of a set of supplied numeric expressions.
 * @param values Numeric expressions to be evaluated.
 */
min(...values: number[]): number;
 
/* Example usage:
 *	var quakes = [0.0, 1.5, 2.0, 1.3];
 *	var minMagnitude = Math.min(...quakes);
 */
```

Note that the `...` before the parameter is known as [destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment).  This makes it possible to unpack values from arrays into distinct variables.  The `min()` and `max()` functions expect each number to be passed in as separate values.  For example, the above code returns the same result as the following call in which each array element is a separate parameter: `Math.min(0.0, 1.5, 2.0, 1.3);` 

Using the `min()` and `max()` functions, write a routine to normalize the values in an arbitrary array of numbers and return a new array. 

```typescript
function normalizeArray(inputArray : number[]) : number[]
{
  /* --- Fill in your algorithm here --- */
}
```

Now, to check that your algorithm works, let's just work out a quick example by hand.  What would the following code print out if you were to run it? Note, if your math is correct, all of the values printed should be between 0.0 and 1.0, inclusive.

```typescript
var quakes = [0.0, 2.3, 5.1, 1.1, 7.6, 1.];
var normalizedQuakes = normalizeArray(quakes);

normalizedQuakes.forEach((elem: number) => {
    console.log(elem)
});
```

Output: 

```typescript
/* --- Fill in the expected console output here --- */
```



## Q2: Constructing a Mesh

For the first two assignments, we were able to use the built-in shapes in Three.js to draw pretty much everything we had to draw because everything could be constructed from 3D graphics primitives like cubes, spheres, cones, etc.  This assignment will be the first one where we create a custom 3D shape made of triangles and apply a custom texture to it.

To create a triangle mesh from scratch, you will need to understand how a **Vertex Array** and an **Index Array** are used together to define each triangle that belongs to the mesh.  We discuss this in detail in lecture, but here is a brief recap:  

The vertex array will hold the actual 3D coordinates for each vertex of the mesh.  To store this values efficiently, the `BufferGeometry` expects these coordinates to be collapsed into a single array that takes the following form `[x1, y1, z1, x2, y2, z2, ... , xn, yn, zn]` .  So, the total number of elements in this array will be the number of vertices in the mesh multiplied by 3.

The index array tells tells us how to connect these vertices together to form triangles.  The elements of this array are the index number of specific vertices from the vertex array.  So, if the vertex array is of length `n`, valid indices would be `0, 1, 2, ... , n-1`.  Similar to the vertices, these entries are listed in a single array in groups of 3 (because it takes 3 vertices to define a single triangle).  Therefore, we should always add indices in groups of 3, and the length of the index array should always be 3 times the number of triangles in the mesh.

One final tip to remember is to use counter-clockwise vertex ordering to tell the graphics engine which side of the triangle is the "front" and which side is the "back."  Remember, only the front face will show up; the back will be invisible!  

Let's practice all these concepts with a simple example of a square.  Create your own copy of the image below and label each vertex with an index number (starting at 0).  Note that the original graphic is included as an SVG file, which you could edit with a program such as [Inkscape](https://inkscape.org/).  Alternatively, you could screenshot and edit the image, or draw it out on paper and take a picture.

**Replace this image with your drawing:**

![](./images/square.svg)

Now, write out the square's vertex array, using the format 
```
[
    x1, y1, z1, 
    x2, y2, z2, 
    ... , 
    xn, yn, zn
]
``` 
(because it's in the *xy*-plane, assume z = 0 for all points):

```typescript
var squareVertexArray = [
	/* --- Fill in the vertex array values --- */
];
```

Finally, write out the square's index array based on the indices you defined in the picture above. Make sure your indices are defined in counter-clockwise order so that a 3D camera looking down on your square from some +Z height above will see the front faces of your triangles.

```typescript
var squareIndexArray = [
    /* --- Fill in your first triangle indices --- */
    /* --- Fill in your second triangle indices --- */
];
```



## License

Material for [CSCI 4611 Spring 2022](https://canvas.umn.edu/courses/290928/assignments/syllabus) by [Evan Suma Rosenberg](https://illusioneering.umn.edu/) is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).
