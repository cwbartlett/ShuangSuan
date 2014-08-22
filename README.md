ShuangSuan (SwanSong) README.md
==============
Christopher W. Bartlett  (with contributions by Amber Shindhelm)
--------------
August 22,2014

ShuangSuan could roughly be translated to "twin simulation" the closest sounding
English word that is semantic would be "Swan Song", so feel free to call it that.  I hope
its not my swan song, per se.  

Documentation right now is just the comments from the code.  More later.



######
#  There are four matrix designs, and these get run twice, once for MZ and once for DZ
#   These matricies provide the random numbers that could, depending on user needs
#   be reused across twins or triaits.  Other random numbers that only provide noise are
#   are simulated here too and added in when the time comes.

## A Matrix for 5 potentially correlated traits
  # Within a trait MZ alwasy share 100%, DZ alwasy 50% share (i.e., they share this and a new randome number mixed 50/50).
  # FYI, a better way to do these matricies is to combine one with all C_rho and an Identity matrix.  Bound to tbe more compact than this, and less error prone

## C Matrix for 5 potentially correlated traits
  # Within a twin pair, this is always 100% shared for a given trait, though across traits thre need not be 100% corrleated of course                                       

## E Matrix for 5 potentially correlated traits
   # Within a twin pair, this is never shared for a given trait, though across traits they can be up to 100% corrleated of course                                       

## AxE Matrix for 5 potentially correlated traits
  # Within a trait MZ alwasy share 100% of thier AxE deviate, DZ always 50% share AxE deviate (i.e., they share this and a new randome number mixed 50/50).
  # I will show later too, but the actual VC is A deviate * AxE deviate * weight but total variance will not necessarily be 1 anymore.

## Now make the actual traits
  # The general form is MZ Twin 1 = A_T1*sqrt(a2) + C_T1 * sqrt(c2) + E_T1*sqrt(e2)+ AxE_T1*CHAOS*sqrt(axe2)
  # Let's do this as matricies since it will be quicker
  # Here's the trick that drove me mad till I figured it out
  # The GxE deviate follows the same rules as the A deviate (shared by MZ, only 50% corrleated in DZ)
  # so that's why GxE deviate is interacting with additive genetic variance even though its multipled by an external variable
  # FYI, if you want to have a CxE interaction, then you would always share the deviate (just like C)
  # and for ExE you never share the deviate (i.e., the only correlation comes from the extrenal trait like CHAOS having a correlation)
  # or in other words, there is no such thing as ExE in the classical twin setting
  # Note that the sqrt of 0.707 is 0.5 - for mixing things 50/50

## Using the twin corrleation difference method to calc A, C, and E
  # Note that GxE will bleed into the A component since its not being modeled explicitly
  # I did check to make sure the bleed in component was the correct magnitude
  # This awaits further testing with a better estimation method
