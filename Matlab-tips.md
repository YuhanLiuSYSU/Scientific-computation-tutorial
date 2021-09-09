# Matlab Tips
Here are some tips for scientific computation using Matlab which may help make your coding smoother :)

## Save with a given name
Here is an example using `eval` from [this post](https://www.mathworks.com/matlabcentral/answers/57818-using-a-matlab-string-as-a-valid-variable-name):
```matlab
X = 'omega';
eval([X '= [2 3 4 5]']);
```
In this way, we create a variable `omega` which is `[2 3 4 5]`.
Another example:
```matlab
eval(['Result = Result',num2str(i)]);
```
when `i = 1`, this is `Result = Result1`. 
## Optional input arguments
### First option: varagin
Sometimes we want optional input arguments with default values. This can be done  using `varagin`. Here is an example from [this post](https://www.mathworks.com/matlabcentral/answers/217363-how-to-support-default-parameter-in-matlab-function):
```matlab
function foobar(varargin)

Defaults = {A,B,C...};

idx = ~cellfun('isempty',varargin);

Defaults(idx) = varargin(idx);
```
or
```matlab
function foobar(varargin)

Defaults = {A,B,C...};

Defaults(1:nargin) = varargin;
```
Here is my code
```matlab
function [K] = getKRNS_(N,varargin)
% getKRNS_ Get the K-matrix of R-NS two string
%   N : Cutoff length for one string
%	Optional input epsilon: Regulator
ep = 0;
if nargin == 2
    ep = varargin{1};
end
pass
end
```
The input can be
```matlab
>> K = getKRNS_(50);
>> K = getKRNS_(50,0.005);
```

Note:
* `nargin` counts all the input arguements, including the ones that are not optional. 
* The optional arguments don't need to be grouped in extra brackets. The sequence matters.

### Second option: struct
A _structure array_ is a data type that groups related data using data containers called _fields_. Each field can contain any type of data. Access data in a field using dot notation of the form `structName.fieldName`. Note the field names have to be strings.
An example from [this post](https://www.mathworks.com/matlabcentral/answers/156063-two-optional-parameters-mutually-exclusive):
```matlab
function y = f(x,params)
% Something
if isfield(params,'length')
	v = linspace(a,b,params.opt1);
elseif isfield(params,'step')
	v = a:params.opt2:b;
end
% Something
end
```
```
y=f(42, struct('length',100));
y=f(42, struct('step',0.5));
```

## Return a "dictionary"
### First option: containers.map
If I want to write a function which can return the entanglement entropy (denoted as S) for bipartition, and return the entanglement entropy as well as the logarithmic negativity (LN) for tripartition. 
This can be done using `containers.Map`. 
```matlab
function[Ent] = getEnt_(Gamma)
Ent = containers.Map;
%% EE
% do something...
Ent('S') = S;
Ent('ES') = ES;
%% LN 
% do something...
Ent('LN') = LN;
Ent('LNS') = LNS;
end
```
### Second option: struct

## Function handle
Function handle can save us from writing lengthy for loop, which is particularly useful if we want to generate a matrix with known expression. Here is an example:
```matlab
RLis = (1:N)';
eleFun = @(n,m) 1/2.*(n-m)./(n+m).*u(2.*n+1).*u(2.*m+1);
ele = bsxfun(eleFun, RLis, RLis');
```
Note:
* We need to use element-wise operator in function handle `.*`

## OOP in Matlab
[User manual](https://www.mathworks.com/help/matlab/matlab_oop/specifying-methods-and-functions.html), and [this](https://www.mathworks.com/help/matlab/matlab_oop/user-defined-classes.html), [this](https://www.mathworks.com/help/matlab/matlab_oop/developing-classes-typical-workflow.html). 
One thing worth noticing (and sometimes annoying) is:
> MATLAB differs from languages like C++ and Java® in that there is no special hidden class object passed to all methods. You must pass an object of the class explicitly to the method.
