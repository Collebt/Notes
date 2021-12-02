1.<img src="C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103105928923.png" alt="image-20211103105928923" style="zoom:33%;" />



2. <img src="C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103105952656.png" alt="image-20211103105952656" style="zoom:33%;" />



3. <img src="C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110018258.png" alt="image-20211103110018258" style="zoom:33%;" />
4. <img src="C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110051488.png" alt="image-20211103110051488" style="zoom:50%;" />
5. ![image-20211103110105318](C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110105318.png)
6. ![image-20211103110114704](C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110114704.png)
7. ![image-20211103110156474](C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110156474.png)
8. ![image-20211103110206621](C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110206621.png)
9. ![image-20211103110217022](C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110217022.png)
10. ![image-20211103110225680](C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110225680.png)



# Answer

1. ![image-20211103110254214](C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110254214.png)

2. <img src="C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110314402.png" alt="image-20211103110314402" style="zoom:50%;" />
3. <img src="C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110324825.png" alt="image-20211103110324825" style="zoom:50%;" />
4. Purpose: In computer graphics, there are many surface detection algorithms. When we view a picture containing non-transparent objects and surfaces, then we cannot see those objects from view which is behind from objects closer to eye. We must remove these hidden surfaces to get a realistic screen image



Z-buffer: The depth in the camera to be rendered is defined as the z value between near and far. The new z'value is obtained by perspective transformation.

limitation: z-buffer algorithm requires a large amount of memory space. A drawback of Z-buffer is that it can only find one visible surface at each pixel position, cannot accumulate intensity values for more than one surface.



A-buffer expands the depth buffer so that each position in the buffer can refer to a linked list of surface, so that more than one surface will be considered and the object edges can be antialiased.

待渲染的照相机[空间](https://www.wikiwand.com/zh/空间)中的深度经常定义为近距到远距之间的z值，在透视变换之后，得到新的z'值







5. $$
   I_s=f_{att}I_p* k_s *cos^n \phi
   $$

   $I_p$ is the point light source's intensity.

   $f_{att}$ takes into account the fact that the energy from a point light source that reaches a given part of a surface falls off as the inverse square of $d_L$

   $k_s$ is the object's specular-reflection coefficients, which ranges from 0 to 1.

   Direction of reflection $R$, and the viewpoint direction $V$ are normalized, then 

   $cos\phi = R\cdot V$

$$
I = I_ak_a+\sum_i f_{att_i}I_{p_i}[k_d(N\cdot L)+k_s(R\cdot V)^n]
$$

   

6. Often illumination in the Flat shading is computed for only a single point on the facet, which is usually the centroid.

   Vertex normal: Assumes the polygons were a piecewise approximation of the real surface. It is useful because normals provide information about the tangent plane at each point.

   Gouraud shading: Firstly, requires that the normal be known for each vertex of the polygonal mesh.Approximate it by averaging the surface normals of all polygonal facets sharing each vertex. Next step is to find vertex intensities by using vertex normals with any desired illumination model.Finally, each polygon is shaded by linear interpolation of vertex intensities along each edge and then between edges along each scan line.

   **Advantages:**

   i. It removes the intensity discontinuity which exists in constant shading model.

   ii. It can be combined with hidden surface algorithm to fill in the visible polygons along each scan line.

   **Disadvantages:**

   i. Gouraud shading has a problem with specular reflections.

   ii. Gouraud shading can introduce anomalies known as Mach bands.

    

   Phong shading: The interpolation is done on all the three components of the normal vector.At each interpolated normal, the pixel intensity is calculated using an
   illumination model.  Phong shading yields substantial improvements over Gouraud shading because highlights are reproduced more faithfully.

   **Advantages:**

   i. It displays more realistic highlights on a surface.

   ii. It greatly reduces the Mach band effect.

   iii. It gives more accurate results.

   **Disadvantages:**

   It requires more calculations and greatly increases the cost of shading steeply.
   
7. <img src="C:\Users\HY Lee\AppData\Roaming\Typora\typora-user-images\image-20211103110413274.png" alt="image-20211103110413274" style="zoom:50%;" />

8. advantage:

   ​	Primitives are processed one at a time
   ​	All analytic processing early on 

   ​	Sampling occurs last
   ​	Minimal state required (immediate mode rendering)
   ​	Processing is forward-mapping

   disadvantage: 

   ​	 Takes no advantage of screen space coherence
   ​	 Requires costly visibility computation
   ​	Only works for solids
   ​	Forces per pixel illumination evaluations



9. Bump mapping

   	1. Look up the height in the heightmap that corresponds to the position on the surface.
   	2. Calculate the surface normal of the heightmap, typically using the finite difference method.
   	3. Combine the surface normal from step two with the true ("geometric") surface normal so that the combined normal points in a new direction.
   	4. Calculate the interaction of the new "bumpy" surface with lights in the scene using, for example, the Phong reflection model.

Different from Displacement mapping: Bump Maps simulate geometry changes based on an image - the light and dark values of an image imply height.

Displacement Maps actually change the geometry of the mesh based on the image.





10. The distinctions between VR and AR come down to the devices they require and the experience itself:

    - AR uses a real-world setting while VR is completely virtual
    - AR users can control their presence in the real world; VR users are controlled by the system
    - VR requires a headset device, but AR can be accessed with a smartphone
    - AR enhances both the virtual and real world while VR only enhances a fictional reality

    Key difference: AR lets the user experience the real world, which has been digitally augmented or enhanced in some way. VR, on the other hand, removes the user from that real-world experience, replacing it with a completely simulated one.

    Application: 

    ​	VR applications are best suited for simulation or complete immersion: Remote collaboration with 3D elements, point-of-view training, and virtual tours. Walmart uses VR to create both unlikely scenarios (such as weather emergencies) and common ones to give associates a first-hand training experience without disrupting operations.

    ​	AR applications are best suited for use cases where users need to be connected to and present in the real world. for example, Maintenance professionals use AR headsets to record and narrate their tasks.

