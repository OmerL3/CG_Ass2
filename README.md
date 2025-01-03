Brief explanation of the project:
there is 4 main data structures:
1. Rays
2. Intersections
3. Objects(sphere and plane)
4. Lights(ambient, directional and spotlight)

Rays and Intersections both pretty basic objects
Rays only hold the information of starting point and direction, and a method that returns the point of the ray at some t - calculatin P0+t*V
Intersections only hold information of the point and the object intersected with

Objects:
there is implementation of plane which is quit simple holding the normal and d
and implementation of sphere which has the center and radius but also calculate snell's law
both objects calculate the intersection with them by giving them the Ray

Lights:
Ambient is simply holding the intensity and rgb, while allways being not-shadowed
Directional not only holds the direction and intensity information but also has a method that traverse all objects and check if one is shadowing the intersection
Spotlight very similar to Directional, though it has a different is_shadowed() calculation due to the fact that the intersection(with the object) might not be inside the light

Main loop: (without the menu explanation)
1. shooting rays through the screen by calculating (point of pixel - point of eye) which is a vector that starts at point of eye
2. traversing the rays, finding the closest object that the ray intersect with and saving the information in the array of Intersections
3. calculating each intersection value(=pixel value) with phong:
   -  there is a helper method that calculates single_pixel_phong which is recursable for the implementation of refractive and reflective objects.
   -  in the helper method i split the calculations to each type of object:
     *  refrective and reflective only calculate the next intersection(recursively)
     *  normal objects calculate the phong formula as described in class
   - finally asigning the returned value to the correct spot in the pixel array and return it to main
4. finally in main, using STB, i write the picture with correct dimensions
