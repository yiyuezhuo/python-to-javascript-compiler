# Python to JavaScript Compiler

I write it for my scientific computing (statistic) code, there are so fragile and I would not write it and test them again.
So compile them to valid JavaScript code is a good ideal.

## usage

```
$ python CLI.py make.json
```

or

```
python CLI.py test2.py --target test2.js
```

## rule example

function define and list comprehesion :

```python
def erfs(x):
    # erf(x/sqrt(2))
    b=[0,0.196854,0.115194,0.000344,0.019527]
    return 1-(1+sum([b[i]*x**i for i in range(1,5)]))**(-4)
```

`->`

```javascript
function erfs(__args__,__kwargs__){
	var x;
	
	x=__kwargs__.x;
	
	x=x || __args__[0];
	
	
	
	var b=[0,0.196854,0.115194,0.000344,0.019527];
	return (1-(Math.pow((1+sum([range([1,5],{}).map(function(i){
		return (b[i]*(Math.pow(x,i)));
	})],{})),(-4))));
}
```

tuple assignment

```python
a,b=a,test
```

`->`

```javascript
!function(){
	a=arguments[0];
	b=arguments[1];
}(a,test);
```

slice

```python
tl[0]/(1+cfrac(tl[1:]))
```

`->`

```javascript
(tl[0]/(1+cfrac([tl.slice(1,undefined,undefined)],{})))
```

keyword call (so I use the `__args__`,`__kwargs__` to support the feature)

```python
if roll and x>=(a-1)/(a+b-2):
	return 1-I(1-x,b,a,n,roll=False)
```

`->`

```javascript
if(roll&&(x>=((a-1)/((a+b)-2)))){ 
	return (1-I([(1-x),b,a,n],{"roll":false}));
}
```

if you worry you must call function as form `func([1,2,3],{})` for "pure function", you can export it through a `make.json` 
file, it can auto generate module scope and setting backend javascript binary (for this, I define `range`,`sum` function and
replace slice funtion).

as 

```json
{
	"source":"test/test2.py",
	"target":"test/test2.js",
	"include":"bin/backend.js",
	"module_name":"stat3",
	"export":[	"norms_cdf", 
					"norms_ppf", 
					"norm_cdf", 
					"norm_ppf", 
					"beta_cdf", 
					"beta_ppf", 
					"chi2_cdf", 
					"chi2_ppf", 
					"t_cdf", 
					"t_ppf", 
					"F_cdf", 
					"F_ppf"],
	"comment":"@Author yiyuezhuo"
}

```

then you call norm_cdf(normal distribution function) as the form `stat3.norm_cdf(0,0,1)`.


## TODO

I don't implement these because I can't use it in that project.

* `for`
* `class`
