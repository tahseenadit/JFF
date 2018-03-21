The following code is wrong:
```
var x = document.getElementsByClassName("example_classname").innerHTML;
alert(x);
```
To get the innerHTML of all the elements with the same class name:

```

var x = document.getElementsByClassName("example_classname");
var i = 0;

while(i < x.length){

   console.log(x[i].innerHTML);

}

```
