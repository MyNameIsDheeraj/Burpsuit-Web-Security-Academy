# 26. How does the AngularJS sandbox work?

### 🔄 Expression Parsing and Rewriting

The sandbox operates by:

- Parsing an expression
- Rewriting the JavaScript code
- Using various functions to check if the rewritten code contains any **dangerous objects**

---

### 🛡️ Key Functions in the Sandbox

- **`ensureSafeObject()`**
    
    Checks if an object references itself, which can help detect objects like `window`.
    
- **`ensureSafeMemberName()`**
    
    Inspects each property access; blocks objects if properties are dangerous, such as:
    
    - `__proto__`
    - `__lookupGetter__`
- **`ensureSafeFunction()`**
    
    Prevents calls to functions like:
    
    - `call()`
    - `apply()`
    - `bind()`
    - `constructor()`

---

### 🔍 See It in Action

You can observe the sandbox behavior yourself:

- Visit [this fiddle](http://jsfiddle.net/2zs2yv7o/1/)
- Set a breakpoint at **line 13275** in the `angular.js` file
- Inspect the variable `fnString`, which contains the rewritten code, to see how AngularJS transforms expressions.