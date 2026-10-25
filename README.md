# Krag

Krag is a strictly typed, linear, zero-cost systems programming language that transpiles to clean C99.

It is built on a simple philosophy: predictability over magic, and compile-time power without runtime overhead. Krag provides powerful metaprogramming, explicit memory management, and a unique linear compilation model, all while generating pure C code that any standard compiler can build.

Krag is not just a syntactic sugar over C. It is a ground-up reimagining of how a compiler interacts with source code.

```luau
-- 1. Mutable Compile-Time State
-- Evaluated strictly top-to-bottom during compilation. No rollback.
static connection_id: integer = 0

-- 2. Custom Syntax (Zero-Cost Macros)
-- Extends the language grammar and runs at compile-time.
syntax spawn [name: static word] [port: integer] {
    connection_id = connection_id + 1
    
    const !name := Connection { 
        id = connection_id, 
        port = port, 
        timeout = 3.14 // 3. Contextual Literal
    }
}

-- Our runtime struct
typedata Connection(
    id: integer,
    port: integer,
    timeout: float 
)

-- Using the macro:
#spawn server_main 8080
#spawn server_backup 9090
```
