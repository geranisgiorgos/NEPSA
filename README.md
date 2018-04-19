NEPSA
======
A Network Exterior Point Simplex Type Algorithm for the solution of the
Minimum Network Flow Problem.

Algorithm implemented in C.
--------------------------
v6.3
- a small change in calc_X_flows() (no need to check the non basic arcs)

v6.2
- Try to compute J_ in a different way: Instead of keeping all in array J_ (containing 0 or 1)
I tried to only maintain the indexes of arcs really belonging into J_ and search among them. It worked BUT
it takes more time....

v5.6.5
- renew D vector

v5.6.2
- a small change into calc_J (no need to check if basic)

v5.6.1
- Write better getsumh

v5.6
+ deleted some no needed variables

v5.5
+ uses find_theta instead pf find_thetas

v5.4
+ I removed exerx_toxo etx. information


v5.0
Implement Dual Network Simplex

v4.0
- Print nothing!! Commented checks etc. so that it takes less time to execute!!!

v3.3
- Calculates cpu time

v3.1
Added the ability to store many graphs into a directory
Added main.c
Added multi generate and store graphs
Added multi solve graphs

v2.3
Same as 2.2 but more clearly writen and corrected

v2.2
- Check J_ behaviour and find directions dij and flow tij (which is dual feasible)

v2.1
- Calculates difference Dz between the new and previous objective value. It is Dz=theta*c_enteringarc=theta*Sum(tij*cij)
- Check type-A pivots and type-B pivots (entering arc's  flow, s_leavingarc etc...)

v2.0
- Actually the same as v1.9.2.
- In Aggelos' examples it does not obtain an initial dual feasible solution (bug in dualtree function?)


v1.9.2
- The only difference compared to version 1.9 is that method dnepsa() has a parameter objval that returns the objective value.

v1.9.1
- The only thing that 1.9.1 does is to compare the solutions found when renewing sets I_,I+ against
the solutions found when these sets are calculating from scratch.So I made 2 methods dnepsa() and
dnepsa1() where the one renews sets I_,I+ and the 2nd calculates them from scratch.
- I changed methods dnepsa() and dnepsa1() to have a parameter objval that returns the objective value.
- In order to make them give same results I changed the renewal methos. The problem was that when
we had more than one arc having the same negative flow and one of them was chosen to be the leaving arc,
then the others remained in I_. To avoid this problem I made the program to check the arcs having
flow 0 (the new flows calculated) and put them into I+
v1.9
- Add new main and make dnepsa function. The new main can produce different seeds in order to test the program...
dnepsa() Returns 0 if the solution is primal feasible and dual feasible
 Returns 1 if the solution is primal feasible but not dual feasible
 Returns 2 if the solution is not primal feasible and dual feasible
 Returns 3 if the solution is not primal feasible and not dual feasible
 Returns 4 if the graph is disconnected
 Returns 5 if the problem is infeasible
 Returns -1 if it doesn't find an initial dual feasible solution

- add test_dnepsa function that test the algorithm for a number (loop) of different problems (different seeds)
- add function isekfyl that checks the flow and returns 1 if it is ekfylismeni

v1.8.1
- Change the way I_ and I+ are renewed. (in case it is th1<=th2 then I[i]=1...)

v1.8
- Make array I to contain DENSITY elements where it is -1 for I_
 and +1 for I+ and 0 is non-basic.
- So, functions calc_I, print_I etc has been changed.
- Function get_index added to give the index of an arc in FROM[] TO[] structures
- Functions find_th1, find_th2 changed in order to return the above index (it is named index_i)

v1.7.1
new:
use double instead of float for logos, s[] and t[]

v1.7
- Calculate D direction and then values t[i]=s[i]+a*D[i] where a=logos. i.e. t gives a sequence of
dual variables that are always dual feasible.
- Changed the way I_ and I+ are formes. I_ contains the non-basic arcs where sij<0 and I+ the non-basic arcs where
sij>=0.
- Better comments
- Better printings
- No need for ptint_basic_tree (Use of print_tree instead)
