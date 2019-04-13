{{jsSidebar("JavaScript Guide")}} {{PreviousNext("Web/JavaScript/Guide/Loops\_and\_iteration", "Web/JavaScript/Guide/Expressions\_and\_Operators")}}

Foksiyonlar, JavaScript'in en temel yapıtaşlarından biridir. Her bir fonksiyon, bir JavaScript işlemidir---herhangi bir görevi yerine getiren  veya değer hesaplayan bir ifade kümesini içerirler. Bir fonksiyonu kullanmak için, fonksiyonu çağıracağınız kısmın faaliyet gösterdiği alanda fonksiyonu tanımlıyor olmanız gerekmektedir.

Daha fazla bilgi için [JavaScript fonksiyonları ile ilgili buradaki detaylı kaynağı](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions) inceleyebilirsiniz.

## Fonksiyonların tanımlanması

### Fonksiyon tanımlamaları

Bir **fonksiyon tanımı** (**fonksiyon betimlemesi**, veya **fonksiyon ifadesi** de denir) [`function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function "function") anahtar kelimesinden sonra aşağıdaki kısımları içerir:

* Fonksiyonun adı.
* Fonksiyonun aldığı parametreler (parantezler ile çevrili ve virgüller ile birbirinden ayrılmış olmalıdırlar).
* Çalıştırılacak JavaScript ifadeleri (süslü parantezler ile çevrilmelidir).

Örneğin aşağıdaki kodda `karesiniAl` isimli basit bir fonksiyon tanımlanmıştır:
    
    function karesiniAl(sayı) {  
      return sayı * sayı;  
    }  
    

`karesiniAl` fonksiyonu, `sayı` isminde tek bir parametre içerir. Tek bir ifade içeren fonksiyonda, `sayı` parametresinin kendisi ile çarpılıp geri döndürülmesi işlemi yapılmıştır. [`return`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/return "return") ifadesi, fonksiyon tarafından döndürülen değeri belirler.
    
    return sayı * sayı;  
    

Sayı türünde olduğu gibi ilkel parametreler fonksiyonlara **değer ile geçilirler**; ilgili değer, fonksiyona parametre olarak geçildiğinde parametre değerinin fonksiyonda ayrı bir kopyası alınır, eğer fonksiyon içerisinde parametre değerinde değişik yapılırsa, bu değişiklik sadece kopyalanan değer üzerinde gerçekleşmiştir, fonksiyona geçilen asıl değer değişmez.

Eğer bir nesneyi ({{jsxref("Array")}} veya bir kullanıcı tanımlı nesne gibi ilkel olmayan değer) fonksiyona parametre olarak geçerseniz, nesne fonksiyon içerisinde kopyalanmadığı için nesne üzerinde yapılan değişiklikler fonksiyon dışında da korunur. Aşağıdaki örneği inceleyelim:
    
    function arabamıDeğiştir(araba) {  
      araba.markası = "Toyota";  
    }  
      
    var arabam = {markası: "Honda", modeli: "Accord", yılı: 1998};  
    var x, y;  
      
    x = arabam.markası ; // "Honda" değerini getirir  
      
    arabamıDeğiştir(arabam);  
    y = arabam.markası; // "Toyota" değeri döndürülür  
                        // (markası özelliği fonksiyon tarafından değiştirilmiştir)  
    

### Fonksiyon ifadeleri

Yukarıdaki fonksiyon tanımlaması sözdizimsel olarak bir ifade olmasına rağmen, fonksiyonlar ayrıca bir f**onksiyon ifadesi **ile de oluşturulabilirler. Böyle bir fonksiyon **anonim** olabilir; bir isme sahip olmak zorunda değildir. Örnek olarak, matematikteki kare alma fonksiyonu aşağıdaki şekilde tanımlanabilir:
    
    var karesiniAl = function(sayı) { return sayı * sayı };  
    var x = karesiniAl(4) // x'in değeri 16 olur.

Fonksiyon ifadesi ile belirtilen fonksiyon adı, fonksiyonun içerisinde kendisini çağıracak şekilde kullanılabilir:
    
    var faktoriyel = function fa(n) { return n < 2 ? 1 : n * fa(n-1) };  
      
    console.log(faktoriyel(3));  
    

Fonksiyon ifadeleri, bir fonksiyon diğer fonksiyona parametre olarak geçilirken oldukça elverişlidir. Aşağıdaki örnekte `map` fonksiyonu tanımlanmış ve ilk parametresinde başka bir fonksiyonu parametre olarak almıştır:
    
    function map(f,d) {  
      var sonuç = [], // Yeni bir dizi  
          i;  
      for (i = 0; i != d.length; i++)  
        sonuç[i] = f(d[i]);  
      return sonuç;  
    }  
    

Aşağıdaki kodda kullanımı mevcuttur:
    
    var çarpım = function(x) {return x * x * x}; // Fonksiyon ifadesi.  
    map(çarpım, [0, 1, 2, 5, 10]);  
    

\[0, 1, 8, 125, 1000\] dizisini döndürür.

JavaScript'te bir fonksiyon, herhangi bir duruma bağlı olarak oluşturulabilir.Örneğin aşağıdaki fonksiyonda `benimFonk` fonksiyonu, `sayı` değeri sadece 0'a eşit olursa tanımlanır:
    
    var benimFonk;  
    if (sayı === 0){  
      benimFonk = function(araba) {  
        araba.marka = "Toyota"  
      }  
    }

Burada tanımlanan fonksiyonlara ek olarak {{jsxref("Function")}} yapıcısını kullanarak da çalışma zamanında fonksiyon oluşmasını sağlanabilir. Örneğin {{jsxref("eval", "eval()")}} ifadesi gibi.

Bir nesnenin özelliği olan fonksiyona **metot** adı verilir. Nesneler ve metotlar hakkında daha fazla bilgi için bkz: [Nesneler ile çalışma](/tr/docs/Web/JavaScript/Guide/Working_with_Objects "en-US/docs/JavaScript/Guide/Working with Objects").

## Fonksiyonları çağırma

Bir fonksiyonu tanımlamakla o fonksiyon çalışmaz. Fonksiyonu tanımlamak kısaca, o fonksiyona bir isim vermek ve o fonkisyon çağırıldığında bizim için hangi eylemleri yapması gerektiğini belirtmektir. Fonksiyonu **çağırmak**, bu belirlenmiş eylemleri bizim o fonksiyona verdiğimiz parametrelerin de kullanılmasıyla gerçekleştirir.  Örneğin, `karesiniAl `diye bir fonksiyon tanımladığınızda, o fonksiyonu aşağıdaki gibi çağırabilirsiniz:
    
    karesiniAl(5);  
    

Bu ifade, fonksiyona parametre olarak 5 sayısını yollayarak çağırır. Fonksiyon, tanımlanırken belirttiğimiz eylemleri yapar ve bize 25 değerini döndürür.

Fonksiyonlar çağrıldıklarında bir alanda olmalıdılar, fakat fonksiyon bildirimi kaldırılabilir, örnekteki gibi:
    
    console.log(square(5));  
    /* ... */  
    function square(n) { return n * n }   
    

Bir fonksiyonun alanı, bildirilen işlevdir, veya tüm program üst seviyede bildirilmişse.

**Not:**  Bu, yalnızca yukarıdaki sözdizimini (i.e. `function benimFonk(){}`) işlevini kullanarak işlevi tanımlarken çalışır. Aşağıdaki kod çalışmayacak. Yani, işlev kaldırma sadece işlev bildirimi ile çalışır ve işlev ifadesiyle çalışamaz.
    
    console.log(square); // square is hoisted with an initial value undefined.  
    console.log(square(5)); // TypeError: square is not a function  
    var square = function (n) {   
      return n * n;   
    }  
    

Bir fonksiyonun argümanları karakter dizileri ve sayılarla sınırlı değildir. Tüm nesneleri bir fonksiyona aktarabilirsiniz. `show_props()` fonksiyonu ([Working with objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Objects_and_Properties "https://developer.mozilla.orghttps://developer.mozilla.org/en-US/docs/JavaScript/Guide/Working_with_Objects#Objects_and_Properties") bölümünde tanımlanmıştır.) nesneyi argüman olarak alan bir fonksiyon örneğidir.

Bir fonksiyon kendini çağırabilir. Örneğin, burada faktöriyelleri yinelemeli olarak hesaplayan bir fonksiyon var.
    
    function factorial(n){  
      if ((n === 0) || (n === 1))  
        return 1;  
      else  
        return (n * factorial(n - 1));  
    }  
    

Daha sonra bir ile beş arasındaki faktöriyelleri şu şekilde hesaplayabilirsiniz:
    
    var a, b, c, d, e;  
    a = factorial(1); // a gets the value 1  
    b = factorial(2); // b gets the value 2  
    c = factorial(3); // c gets the value 6  
    d = factorial(4); // d gets the value 24  
    e = factorial(5); // e gets the value 120  
    

Fonksiyonları  çağırmanın başka yolları da var. Bir fonksiyonun dinamik olarak çağrılması gerektiği veya bir fonksiyonun argümanlarının sayısının değişebileceği veya fonksiyon çağrısının içeriğinin çalışma zamanında belirlenen belirli bir nesneye ayarlanması gerektiği durumlar vardır. Fonksiyonların kendileri nesneler olduğu ve bu nesnelerin sırasıyla yöntemleri olduğu anlaşılıyor (bkz. {{Jsxref ("Function")}} nesnesi). Bunlardan biri, {{jsxref ("Function.apply", "application ()")}} yöntemi, bu amaca ulaşmak için kullanılabilir.

## Fonksiyon Kapsamı

Bir fonksiyon içinde tanımlanmış değişkenlere, fonksiyonun dışındaki herhangi bir yerden erişilemez, çünkü değişken sadece fonksiyon kapsamında tanımlanır. Bununla birlikte, bir fonksiyon tanımlandığı kapsamda tanımlanan tüm değişkenlere ve fonksiyonlara erişebilir. Başka bir deyişle, global kapsamda tanımlanan bir fonksiyon, global kapsamda tanımlanan tüm değişkenlere erişebilir. Başka bir fonksiyonun içinde tanımlanmış bir fonksiyon, ana fonksiyonunda tanımlanan tüm değişkenlere ve ana fonksiyonun erişebildiği herhangi bir değişkene de erişebilir.
    
    // The following variables are defined in the global scope  
    var num1 = 20,  
        num2 = 3,  
        name = "Chamahk";  
      
    // This function is defined in the global scope  
    function multiply() {  
      return num1 * num2;  
    }  
      
    multiply(); // Returns 60  
      
    // A nested function example  
    function getScore () {  
      var num1 = 2,  
          num2 = 3;  
        
      function add() {  
        return name + " scored " + (num1 + num2);  
      }  
        
      return add();  
    }  
      
    getScore(); // Returns "Chamahk scored 5"

## Kapsam ve fonksiyon yığını

### Yineleme

Bir fonksiyon kendisine başvurabilir ve kendisini arayabilir. Bir işlevin kendisine başvurması için üç yol vardır:

  
1. fonksiyonun adı
2. `[arguments.callee](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments/callee)`
3. fonksiyona başvuran bir kapsam içi değişken 

Örneğin, aşağıdaki işlev tanımını göz önünde bulundurun:

  
    var foo = function bar() {  
       // statements go here  
    };  
    

Fonksiyon gövdesinde aşağıdakilerden hepsi eşdeğerdir.

1. `bar()`
2. `arguments.callee()`
3. `foo()`

Kendisini çağıran fonksiyona özyinelemeli fonksiyon denir. Bazı açılardan, özyineleme bir döngüye benzer. Her ikisi de aynı kodu birkaç kez uygular ve her ikisi de bir koşul gerektirir (bu, sonsuz bir döngüden kaçınmak veya daha doğrusu bu durumda sonsuz özyinelemeden kaçınmak için). Örneğin, aşağıdaki döngü:  

    var x = 0;  
    while (x < 10) { // "x < 10" is the loop condition  
       // do stuff  
       x++;  
    }  
    

özyinelemeli bir fonksiyona ve bu fonksiyonun çağrısına dönüştürülebilir:
    
    function loop(x) {  
      if (x >= 10) // "x >= 10" is the exit condition (equivalent to "!(x < 10)")  
        return;  
      // do stuff  
      loop(x + 1); // the recursive call  
    }  
    loop(0);  
    

Ancak, bazı algoritmalar basit yinelemeli döngüler olamaz. Örneğin, bir ağaç yapısının tüm düğümlerinin (örneğin [DOM](https://developer.mozilla.org/en-US/docs/DOM)) alınması özyineleme kullanılarak daha kolay yapılır:
    
    function walkTree(node) {  
      if (node == null) //   
        return;  
      // do something with node  
      for (var i = 0; i < node.childNodes.length; i++) {  
        walkTree(node.childNodes[i]);  
      }  
    }  
    

Fonksiyon `döngüsü` ile karşılaştırıldığında, her özyinelemeli çağrının kendisi burada birçok özyinelemeli çağrı yapar.

Herhangi bir özyinelemeli algoritmayı özyinelemeli olmayan bir algoritmaya dönüştürmek mümkündür, ancak çoğu zaman mantık çok daha karmaşıktır ve bunu yapmak bir yığının kullanılmasını gerektirir. Aslında, özyinelemenin kendisi bir yığın kullanır: Fonksiyon yığını.

Yığın benzeri davranış aşağıdaki örnekte görülebilir:
    
    function foo(i) {  
      if (i < 0)  
        return;  
      console.log('begin:' + i);  
      foo(i - 1);  
      console.log('end:' + i);  
    }  
    foo(3);  
      
    // Output:  
      
    // begin:3  
    // begin:2  
    // begin:1  
    // begin:0  
    // end:0  
    // end:1  
    // end:2  
    // end:3

### Nested functions and closures

You can nest a function within a function. The nested (inner) function is private to its containing (outer) function. It also forms a *closure*. A closure is an expression (typically a function) that can have free variables together with an environment that binds those variables (that "closes" the expression).

Since a nested function is a closure, this means that a nested function can "inherit" the arguments and variables of its containing function. In other words, the inner function contains the scope of the outer function.

To summarize:

* The inner function can be accessed only from statements in the outer function.

* The inner function forms a closure: the inner function can use the arguments and variables of the outer function, while the outer function cannot use the arguments and variables of the inner function.

The following example shows nested functions:
    
    function addSquares(a,b) {  
      function square(x) {  
        return x * x;  
      }  
      return square(a) + square(b);  
    }  
    a = addSquares(2,3); // returns 13  
    b = addSquares(3,4); // returns 25  
    c = addSquares(4,5); // returns 41  
    

Since the inner function forms a closure, you can call the outer function and specify arguments for both the outer and inner function:
    
    function outside(x) {  
      function inside(y) {  
        return x + y;  
      }  
      return inside;  
    }  
    fn_inside = outside(3); // Think of it like: give me a function that adds 3 to whatever you give it  
    result = fn_inside(5); // returns 8  
      
    result1 = outside(3)(5); // returns 8  
    

### Preservation of variables

Notice how `x` is preserved when `inside` is returned. A closure must preserve the arguments and variables in all scopes it references. Since each call provides potentially different arguments, a new closure is created for each call to outside. The memory can be freed only when the returned `inside` is no longer accessible.

This is not different from storing references in other objects, but is often less obvious because one does not set the references directly and cannot inspect them.

### Multiply-nested functions

Functions can be multiply-nested, i.e. a function (A) containing a function (B) containing a function (C). Both functions B and C form closures here, so B can access A and C can access B. In addition, since C can access B which can access A, C can also access A. Thus, the closures can contain multiple scopes; they recursively contain the scope of the functions containing it. This is called *scope chaining*. (Why it is called "chaining" will be explained later.)

Consider the following example:
    
    function A(x) {  
      function B(y) {  
        function C(z) {  
          console.log(x + y + z);  
        }  
        C(3);  
      }  
      B(2);  
    }  
    A(1); // logs 6 (1 + 2 + 3)  
    

In this example, `C` accesses `B`'s `y` and `A`'s `x`. This can be done because:

1. `B` forms a closure including `A`, i.e. `B` can access `A`'s arguments and variables.
2. `C` forms a closure including `B`.
3. Because `B`'s closure includes `A`, `C`'s closure includes `A`, `C` can access both `B` *and* `A`'s arguments and variables. In other words, `C` *chains* the scopes of `B` and `A` in that order.

The reverse, however, is not true. `A` cannot access `C`, because `A` cannot access any argument or variable of `B`, which `C` is a variable of. Thus, `C` remains private to only `B`.

### Name conflicts

When two arguments or variables in the scopes of a closure have the same name, there is a *name conflict*. More inner scopes take precedence, so the inner-most scope takes the highest precedence, while the outer-most scope takes the lowest. This is the scope chain. The first on the chain is the inner-most scope, and the last is the outer-most scope. Consider the following:
    
    function outside() {  
      var x = 10;  
      function inside(x) {  
        return x;  
      }  
      return inside;  
    }  
    result = outside()(20); // returns 20 instead of 10  
    

The name conflict happens at the statement `return x` and is between `inside`'s parameter `x` and `outside`'s variable `x`. The scope chain here is {`inside`, `outside`, global object}. Therefore `inside`'s `x` takes precedences over `outside`'s `x`, and 20 (`inside`'s `x`) is returned instead of 10 (`outside`'s `x`).

## Closures

Closures are one of the most powerful features of JavaScript. JavaScript allows for the nesting of functions and grants the inner function full access to all the variables and functions defined inside the outer function (and all other variables and functions that the outer function has access to). However, the outer function does not have access to the variables and functions defined inside the inner function. This provides a sort of security for the variables of the inner function. Also, since the inner function has access to the scope of the outer function, the variables and functions defined in the outer function will live longer than the outer function itself, if the inner function manages to survive beyond the life of the outer function. A closure is created when the inner function is somehow made available to any scope outside the outer function.
    
    var pet = function(name) {   // The outer function defines a variable called "name"  
      var getName = function() {  
        return name;             // The inner function has access to the "name" variable of the outer function  
      }  
      return getName;            // Return the inner function, thereby exposing it to outer scopes  
    }  
    myPet = pet("Vivie");  
         
    myPet();                     // Returns "Vivie"  
    

It can be much more complex than the code above. An object containing methods for manipulating the inner variables of the outer function can be returned.
    
    var createPet = function(name) {  
      var sex;  
        
      return {  
        setName: function(newName) {  
          name = newName;  
        },  
          
        getName: function() {  
          return name;  
        },  
          
        getSex: function() {  
          return sex;  
        },  
          
        setSex: function(newSex) {  
          if(typeof newSex === "string" && (newSex.toLowerCase() === "male" || newSex.toLowerCase() === "female")) {  
            sex = newSex;  
          }  
        }  
      }  
    }  
      
    var pet = createPet("Vivie");  
    pet.getName();                  // Vivie  
      
    pet.setName("Oliver");  
    pet.setSex("male");  
    pet.getSex();                   // male  
    pet.getName();                  // Oliver  
    

In the code above, the `name` variable of the outer function is accessible to the inner functions, and there is no other way to access the inner variables except through the inner functions. The inner variables of the inner functions act as safe stores for the outer arguments and variables. They hold "persistent", yet secure, data for the inner functions to work with. The functions do not even have to be assigned to a variable, or have a name.
    
    var getCode = (function(){  
      var secureCode = "0]Eal(eh&2";    // A code we do not want outsiders to be able to modify...  
        
      return function () {  
        return secureCode;  
      };  
    })();  
      
    getCode();    // Returns the secureCode  
    

There are, however, a number of pitfalls to watch out for when using closures. If an enclosed function defines a variable with the same name as the name of a variable in the outer scope, there is no way to refer to the variable in the outer scope again.
    
    var createPet = function(name) {  // Outer function defines a variable called "name"  
      return {  
        setName: function(name) {    // Enclosed function also defines a variable called "name"  
          name = name;               // ??? How do we access the "name" defined by the outer function ???  
        }  
      }  
    }  
    

The magical `this` variable is very tricky in closures. They have to be used carefully, as what `this` refers to depends completely on where the function was called, rather than where it was defined.

## Using the arguments object

The arguments of a function are maintained in an array-like object. Within a function, you can address the arguments passed to it as follows:
    
    arguments[i]  
    

where `i` is the ordinal number of the argument, starting at zero. So, the first argument passed to a function would be `arguments[0]`. The total number of arguments is indicated by `arguments.length`.

Using the `arguments` object, you can call a function with more arguments than it is formally declared to accept. This is often useful if you don't know in advance how many arguments will be passed to the function. You can use `arguments.length` to determine the number of arguments actually passed to the function, and then access each argument using the `arguments` object.

For example, consider a function that concatenates several strings. The only formal argument for the function is a string that specifies the characters that separate the items to concatenate. The function is defined as follows:
    
    function myConcat(separator) {  
       var result = ""; // initialize list  
       var i;  
       // iterate through arguments  
       for (i = 1; i < arguments.length; i++) {  
          result += arguments[i] + separator;  
       }  
       return result;  
    }  
    

You can pass any number of arguments to this function, and it concatenates each argument into a string "list":
    
    // returns "red, orange, blue, "  
    myConcat(", ", "red", "orange", "blue");  
      
    // returns "elephant; giraffe; lion; cheetah; "  
    myConcat("; ", "elephant", "giraffe", "lion", "cheetah");  
      
    // returns "sage. basil. oregano. pepper. parsley. "  
    myConcat(". ", "sage", "basil", "oregano", "pepper", "parsley");  
    

**Note:** The `arguments` variable is "array-like", but not an array. It is array-like in that is has a numbered index and a `length` property. However, it does not possess all of the array-manipulation methods.

See the {{jsxref("Function")}} object in the JavaScript reference for more information.

## Function parameters

Starting with ECMAScript 6, there are two new kinds of parameters: default parameters and rest parameters.

### Default parameters

In JavaScript, parameters of functions default to `undefined`. However, in some situations it might be useful to set a different default value. This is where default parameters can help.

In the past, the general strategy for setting defaults was to test parameter values in the body of the function and assign a value if they are `undefined`. If in the following example, no value is provided for `b` in the call, its value would be `undefined` when evaluating `a*b` and the call to `multiply` would have returned `NaN`. However, this is caught with the second line in this example:
    
    function multiply(a, b) {  
      b = typeof b !== 'undefined' ?  b : 1;  
      
      return a*b;  
    }  
      
    multiply(5); // 5  
    

With default parameters, the check in the function body is no longer necessary. Now, you can simply put `1` as the default value for `b` in the function head:
    
    function multiply(a, b = 1) {  
      return a*b;  
    }  
      
    multiply(5); // 5

Fore more details, see [default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters) in the reference.

### Rest parameters

The [rest parameter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) syntax allows us to represent an indefinite number of arguments as an array. In the example, we use the rest parameters to collect arguments from the second one to the end. We then multiply them by the first one. This example is using an arrow function, which is introduced in the next section.
    
    function multiply(multiplier, ...theArgs) {  
      return theArgs.map(x => multiplier * x);  
    }  
      
    var arr = multiply(2, 1, 2, 3);  
    console.log(arr); // [2, 4, 6]

## Arrow functions

An [arrow function expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) (also known as **fat arrow function**) has a shorter syntax compared to function expressions and lexically binds the `this` value. Arrow functions are always anonymous. See also this hacks.mozilla.org blog post: "[ES6 In Depth: Arrow functions](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)".

Two factors influenced the introduction of arrow functions: shorter functions and lexical `this`.

### Shorter functions

In some functional patterns, shorter functions are welcome. Compare:
    
    var a = [  
      "Hydrogen",  
      "Helium",  
      "Lithium",  
      "Beryllium"  
    ];  
      
    var a2 = a.map(function(s){ return s.length });  
      
    console.log(a2); // logs [ 8, 6, 7, 9 ]  
      
    var a3 = a.map( s => s.length );  
      
    console.log(a3); // logs [ 8, 6, 7, 9 ]  
    

### Lexical `this`

Until arrow functions, every new function defined its own [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this) value (a new object in case of a constructor, undefined in strict mode function calls, the context object if the function is called as an "object method", etc.). This proved to be annoying with an object-oriented style of programming.
    
    function Person() {  
      // The Person() constructor defines `this` as itself.  
      this.age = 0;  
      
      setInterval(function growUp() {  
        // In nonstrict mode, the growUp() function defines `this`   
        // as the global object, which is different from the `this`  
        // defined by the Person() constructor.  
        this.age++;  
      }, 1000);  
    }  
      
    var p = new Person();

In ECMAScript 3/5, this issue was fixed by assigning the value in `this` to a variable that could be closed over.
    
    function Person() {  
      var self = this; // Some choose `that` instead of `self`.   
                       // Choose one and be consistent.  
      self.age = 0;  
      
      setInterval(function growUp() {  
        // The callback refers to the `self` variable of which  
        // the value is the expected object.  
        self.age++;  
      }, 1000);  
    }

Alternatively, a [bound function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind) could be created so that the proper `this` value would be passed to the `growUp()` function.

Arrow functions capture the `this` value of the enclosing context, so the following code works as expected.
    
    function Person(){  
      this.age = 0;  
      
      setInterval(() => {  
        this.age++; // |this| properly refers to the person object  
      }, 1000);  
    }  
      
    var p = new Person();

## Predefined functions

JavaScript has several top-level, built-in functions:

**{{jsxref("Global\_Objects/eval", "eval()")}}**
> 
> The `**eval()**` method evaluates JavaScript code represented as a string.

**{{jsxref("Global\_Objects/uneval", "uneval()")}} {{non-standard\_inline}}**
> 
> The `**uneval()**` method creates a string representation of the source code of an {{jsxref("Object")}}.

**{{jsxref("Global\_Objects/isFinite", "isFinite()")}}**
> 
> The global `**isFinite()**` function determines whether the passed value is a finite number. If needed, the parameter is first converted to a number.

**{{jsxref("Global\_Objects/isNaN", "isNaN()")}}**
> 
> The `**isNaN()**` function determines whether a value is {{jsxref("Global\_Objects/NaN", "NaN")}} or not. Note: coercion inside the `isNaN` function has [interesting](https://developer.mozilla.orghttps://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN#Description) rules; you may alternatively want to use {{jsxref("Number.isNaN()")}}, as defined in ECMAScript 6, or you can use `[typeof](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof)` to determine if the value is Not-A-Number.

**{{jsxref("Global\_Objects/parseFloat", "parseFloat()")}}**
> 
> The `**parseFloat()**` function parses a string argument and returns a floating point number.

**{{jsxref("Global\_Objects/parseInt", "parseInt()")}}**
> 
> The `**parseInt()**` function parses a string argument and returns an integer of the specified radix (the base in mathematical numeral systems).

**{{jsxref("Global\_Objects/decodeURI", "decodeURI()")}}**
> 
> The `**decodeURI()**` function decodes a Uniform Resource Identifier (URI) previously created by {{jsxref("Global\_Objects/encodeURI", "encodeURI")}} or by a similar routine.

**{{jsxref("Global\_Objects/decodeURIComponent", "decodeURIComponent()")}}**
> 
> The `**decodeURIComponent()**` method decodes a Uniform Resource Identifier (URI) component previously created by {{jsxref("Global\_Objects/encodeURIComponent", "encodeURIComponent")}} or by a similar routine.

**{{jsxref("Global\_Objects/encodeURI", "encodeURI()")}}**
> 
> The `**encodeURI()**` method encodes a Uniform Resource Identifier (URI) by replacing each instance of certain characters by one, two, three, or four escape sequences representing the UTF-8 encoding of the character (will only be four escape sequences for characters composed of two "surrogate" characters).

**{{jsxref("Global\_Objects/encodeURIComponent", "encodeURIComponent()")}}**
> 
> The `**encodeURIComponent()**` method encodes a Uniform Resource Identifier (URI) component by replacing each instance of certain characters by one, two, three, or four escape sequences representing the UTF-8 encoding of the character (will only be four escape sequences for characters composed of two "surrogate" characters).

**{{jsxref("Global\_Objects/escape", "escape()")}} {{deprecated\_inline}}**
> 
> The deprecated `**escape()**` method computes a new string in which certain characters have been replaced by a hexadecimal escape sequence. Use {{jsxref("Global\_Objects/encodeURI", "encodeURI")}} or {{jsxref("Global\_Objects/encodeURIComponent", "encodeURIComponent")}} instead.

**{{jsxref("Global\_Objects/unescape", "unescape()")}} {{deprecated\_inline}}**
> 
> The deprecated `**unescape()**` method computes a new string in which hexadecimal escape sequences are replaced with the character that it represents. The escape sequences might be introduced by a function like {{jsxref("Global\_Objects/escape", "escape")}}. Because `unescape()` is deprecated, use {{jsxref("Global\_Objects/decodeURI", "decodeURI()")}} or {{jsxref("Global\_Objects/decodeURIComponent", "decodeURIComponent")}} instead.

{{PreviousNext("Web/JavaScript/Guide/Loops\_and\_iteration", "Web/JavaScript/Guide/Expressions\_and\_Operators")}}
