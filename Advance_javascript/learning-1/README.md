## Advanced JavaScript

- How javascript works ?
  -- Javascript Engine (V8 engine Google) (consider a js file computer should understand it) where v8 engine converts js files into mahine level language into render content on browser. Many ECMAScript engines.
- First JS engine **Brendan Eich**  JS creator, SPyder engine (firefox)
- v8 engine is used by chrome and node js and it is written in c++.
- JS File -> JS Lexical Analysis (Parser) -> AST (Abstract Syntax Tree) -> Interpreter (Byte code)-> Profiler (monitor or watcher) -> Compiler -> Optimized code === Only respect ECMAScript standards can engines be developed.
- ![image](https://github.com/bhargavvummadi/Learning/assets/52027911/c8e32c5e-75b5-420b-8606-47155168dbe3)

- Interpreter - convertes line by line to bytecode starts up fast but no optimization
- Compiler - convertes entire code at a time takes some time but gives optimization.
- Best of both worlds - JIT compiler

- Writing optimized code for better compilation
- Below are probalamatic concepts for js compilation (less optimized):
- eval()
- arguments https://github.com/petkaantonov/bluebird/wiki/Optimization-killers#3-managing-arguments
- for in
- with
- delete
- Hidden classes (Example reorder usage of objects) https://richardartoul.github.io/jekyll/update/2015/04/26/hidden-classes.html  and inline caching 
- Web Assembly binary executable format or standard (why not use machine code from start just give websites machine code because there is no standard conversion from server to browser compilation) https://webassembly.org/
- Call Stack and Memory Heap
- ![stack](https://github.com/bhargavvummadi/Learning/assets/52027911/c9a20a18-63ec-4b41-854e-119c992e053d)

- JS is garbage collected language (mark and sweep allocation (unreference data is gb collected)), but memory managmenet should be taken care
- Memory leak causes of following:
- - Global variables
- - Event listeners (var ele = document.getElementById('Button'); ele.addEventListner('click',onClick)) we usually don't remove
- - setInterval (setInterval(()=> {})
- JS is a single threaded programming language (has only one call stack) because of this js is synchronous.
- JavaScript Runtime
