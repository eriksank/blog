#The state of low-level, system programming

C code is very often called from scripting engines. This phenomenon started almost immediately when the first shell scripts appeared in the 1970s, chaining C programs. It only became more prevalent with scripting popularity going through the roof over the last few decades. Javascript, Ruby, Perl, PHP, Tcl, Lua, and so on, eventually all rest on a set of foreign, native functions, written in C. The typical DSL (Domain-Specific Languages) such as SQL, sed, regular expressions, or xpath are also executed by their own scripting engines.

In [Ousterhout's words](http://www.tcl.tk/doc/scripting.html): C provides the hardcore mechanisms while scripting engines execute the policies. The practices in programming have increasingly become polarized between either using a scripting engine or else a system language.

Any language that aims to replace C as a system language will need to be able to carry its functions over the C ABI (Application Binary Interface). It must be possible for such contender to be called from C code, because that is what it takes to be called from a modern scripting engine too. If a C library were a duck, this is what you can do with a duck:

    #include <dlfcn.h>

    void* library = dlopen("duck.so", RTLD_LAZY);

    typedef void (*duck_t)();

    duck_t walk = (duck_t) dlsym(library, "walk");

    walk();

Since you could create 'duck.so' also in Pascal, C++, or D, these languages could also be used effectively as system programming languages. These languages are not too popular, but they could actually do the job too.

For a language to be a valid substitute for C, it must simply be capable of walking like a duck. For example, Java and C# cannot walk like a duck, not even if that is what it would take to save themselves from drowning. Therefore, they are absolutely unsuitable as system languages.

There are at least two projects at the moment, aiming at creating a new system-level language. The [Go language](http://golang.org) and the [Rust language](http://www.rust-lang.org). What they have in common, though, is that both Go and Rust are entirely incapable of walking like a duck.

Since you cannot call Rust -or Go code from a scripting engine, they are inadvertently positioning themselves as alternatives to the scripting engines themselves. Go and Rust, however, do not stand the slightest chance to succeed when trying to position themselves like that. If programmers wanted a statically-typed, compiled system language for their scripting efforts, they would be using the existing system languages for that already.

This explains why neither Go nor Rust, in their current incarnations, will ever take off as replacements, neither for C nor for scripting languages.


