This  is a case trying to recreate poiseuille flow using interFoam, with no riblet involved in the system.

As a last ditch attempt to get this to work, I'm going to try to implement periodic boundary conditions, in order to allow the flow to fully develop (that phrasing might be meaningless here).

This was done in the following way:
  1.  Change leftWall and rightWall to type "cyclic".
  2. Add the "neighbourPatch" keyword, along with the patch that the periodic conditions are shared with. e.g. to leftWall add: "neighbourPatch rightWall";
  3. Change right and leftwall 0/U conditions to "type cyclic;"
  4. Ditto for the 0/alpha.water.orig file. (This might not be correct).

IGNORE ALL THE STUFF ABOVE THIS

The pressure conditions aren't really working here.  Lets try a simpler approach, but with a long narrow pipe.
This will be based on this document http://files.the-foam-house5.webnode.es/200000363-59a695aa6c/Chapter4_Pipe.pdf, but without all the wedge stuff. (hopefully that's fine)

Some changes were made from this wedge setup.  Instead it was modelled as a 2D pipe of height 0.008 m and length 0.4 m.  (This is double the length of the wedge pipe, not entirely sure this
change was necessary.)

The simulation was also run for a duration of 0.3 s instead of 0.2.

In lieu of wedge/axisymmetric boundary conditions, the top and bottom boundaries were set to noslip.

Using their values for p and U, the parabola didn't develop, and instead had a flattened top.  In order to achieve the proper parabolic profile, the velocity and pressure were both increased
by around a factor of 10.  Not sure why.

The algorithm used for the velocity solver that had been used in the other riblet simulations was also changed to the one used in the wedge paper.  Although I don't think this had a
phenomenological effect.
