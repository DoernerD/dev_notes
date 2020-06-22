# MATLAB Programming Notes

# Matlab

## Logspace vector

    logspace(a,b)

where the range is [10^a,10^b]. It creates 50 points. If you want more, add another
argument n with n the number of points you want.

## Fill area

With the fill command, you can fill a polygon enclosed by the vector

    fill(X, Y, C)

where usually X = [x, flip(x)] to go back and forth on the x vector.
Y is the corresponding value, and might also be flipped, depending on the data.
C determines the color. To get some shading use

    h = fill(X, Y, C)
    set(h,'facealpha',0.5)

This makes the filling more transparent and you don't need to deal with RGB codes.

## Finding index of element

    idx = find(a == 2)

This returns the index of the element of a which equals 2. So for a = [1 2 3], the
answer would be 2.

# Simulink

- call Simulink from the matlab command line: 

