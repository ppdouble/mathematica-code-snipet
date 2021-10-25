piecewise with color:

smooth L1:

```
Plot[Piecewise[{{0.5 u^2, Abs[u] < 1}, {-0.5 + Abs[u], Abs[u] >= 1}},
  0], {u, -4.2, 4.2}]
```

```
s = Piecewise[{{0.5 #^2, Abs[#] < 1}, {Abs[#] - 0.5, Abs[#] >= 1}}] &;

colorFunction = s;
piecewiseParts = Length@colorFunction[[1, 1]];
colors = ColorData[1][#] & /@ Range@piecewiseParts;
colorFunction[[1, 1, All, 1]] = colors;

Plot[s[x], {x, -2, 2}, ColorFunction -> colorFunction,
 ColorFunctionScaling -> False]
 ```

 ```
 pwSplit[_[pairs : {{_, _} ..}]] :=
 Piecewise[{#}, Indeterminate] & /@ pairs

pwSplit[_[pairs : {{_, _} ..}, expr_]] :=
 Append[pwSplit@{pairs}, pwSplit@{{{expr, Nor @@ pairs[[All, 2]]}}}]

 pw = Piecewise[{{0.5 x^2, Abs[x] < 1}, {Abs[x] - 0.5, Abs[x] >= 1}}];

 Plot[Evaluate[pwSplit@pw], {x, -2, 2}, PlotStyle -> Thick,
 Axes -> True]
 ```

 ```
 Export["smoothl1.png",
 Plot[Evaluate[pwSplit@pw], {x, -2, 2}, PlotStyle -> Thick,
  Axes -> True], ImageSize -> Scaled[.8], ImageResolution -> 300]
 ```

 [1] https://mathematica.stackexchange.com/questions/1128/plotting-piecewise-function-with-distinct-colors-in-each-section
