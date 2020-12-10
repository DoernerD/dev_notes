# MATLAB Programming Notes

## Matlab

### Logspace vector

    logspace(a,b)

where the range is [10^a,10^b]. It creates 50 points. If you want more, add another
argument n with n the number of points you want.

### Fill area

With the fill command, you can fill a polygon enclosed by the vector

    fill(X, Y, C)

where usually X = [x, flip(x)] to go back and forth on the x vector.
Y is the corresponding value, and might also be flipped, depending on the data.
C determines the color. To get some shading use

    h = fill(X, Y, C)
    set(h,'facealpha',0.5)

This makes the filling more transparent and you don't need to deal with RGB codes.

### Finding index of element

    idx = find(a == 2)

This returns the index of the element of a which equals 2. So for a = [1 2 3], the
answer would be 2.

### GUI Design

- List directory content in Listbox

            filePattern = fullfile('03_simulation\','*.slx');
            simModels = dir(filePattern);
            simList = {simModels(~[simModels.isdir]).name};
            app.ChooseModelListBox.Items = simList;
  
  This lists all \*.slx files in the 03\_simulation directory in the ListBox.
  'dir' returs the directory content based on the 'filePattern' and 'simList'
  contains only the names of the files in an array to be used as items.

### Resample Simulation Data

To resample a timeseries y to a different time vector tnew use

    yResample = resample(y,tnew)

yResample is the new timeseries.


### Using one entry of a symbolic vector

When using the cross product, you obviously get a vector in return. Now, in
order to only use one entry, you can't use cp(2), as cp is the symbolic vector.
The easiest way is to use

    cp2 = cp'*[0; 1; 0];

cp2 is the desired scalar function.


## Simulink

- call Simulink from the matlab command line: 
        sim('model.slx')

- Simulink Debugger: *Debug* -> *Breakpoints List* -> *Debug Model*. Then start
  the debugger in the GUI. Afterwards you can use the debugging commands in the
  MATLAB command window.


## Stateflow

In Stateflow you can define various signals, events and so on. To get an
overview over all signals and define them you have two options (up to MATLAB
2019a).

1.) *Model Explorer*, then navigate to the chart and have them there.
2.) *View* -> *Symbols*, then you get the panel on the side.


## Algebraic Loops

Simulink has various ways to solve algebraic loops, either based on a *Trust
Region* or *Line Search* algorithm. There can be cases, where one or the other
fails. To set them manually, use

   set\_param(*modelName*,'AlgebraicLoopSolver','LineSearch');

This can help if the simulation doesn't converge because of algebraic loops (and
you can't solve them otherwise).
