# Rust

Rust is a multi-paradigm, general-purpose programming language that emphasizes performance, type safety, and concurrency. It enforces memory safety—meaning that all references point to valid memory—without a garbage collector. To simultaneously enforce memory safety and prevent data races, its "borrow checker" tracks the object lifetime of all references in a program during compilation. Rust was influenced by ideas from functional programming, including immutability, higher-order functions, and algebraic data types. It is popular for systems programming.Software developer Graydon Hoare created Rust as a personal project while working at Mozilla Research in 2006. Mozilla officially sponsored the project in 2009. In the years following the first stable release in May 2015, Rust was adopted by companies including Amazon, Discord, Dropbox, Google (Alphabet), Meta, and Microsoft. In December 2022, it became the first language other than C and assembly to be supported in the development of the Linux kernel.
Rust has been noted for its rapid adoption, and has been studied in programming language theory research.


== History ==


=== Origins (2006–2012) ===
Rust grew out of a personal project begun in 2006 by Mozilla Research employee Graydon Hoare. Mozilla began sponsoring the project in 2009 as a part of the ongoing development of an experimental browser engine called Servo, which was officially announced by Mozilla in 2010. During this time, the Rust logo was developed based on a bicycle chainring. Around the same year, work shifted from the initial compiler written in OCaml to a self-hosting compiler based on LLVM written in Rust. The new Rust compiler successfully compiled itself in 2011.


=== Evolution (2012–2020) ===
Rust's type system underwent significant changes between versions 0.2, 0.3, and 0.4. In version 0.2, which was released in March 2012, classes were introduced for the first time. Four months later, version 0.3 added destructors and polymorphism, through the use of interfaces. In October 2012, version 0.4 was released, which added traits as a means of inheritance. Interfaces were combined with traits and removed as a separate feature; and classes were replaced by a combination of implementations and structured types.Through the early 2010s, memory management through the ownership system was gradually consolidated to prevent memory bugs. By 2013, Rust's garbage collector was removed, with the ownership rules in place.In January 2014, the editor-in-chief of Dr. Dobb's Journal, Andrew Binstock, commented on Rust's chances of becoming a competitor to C++, along with D, Go, and Nim (then Nimrod). According to Binstock, while Rust was "widely viewed as a remarkably elegant language", adoption slowed because it radically changed from version to version. The first stable release, Rust 1.0, was announced on May 15, 2015.The development of the Servo browser engine continued alongside Rust's own growth. In September 2017, Firefox 57 was released as the first version that incorporated components from Servo, in a project named "Firefox Quantum".


=== Mozilla layoffs and Rust Foundation (2020–present) ===
In August 2020, Mozilla laid off 250 of its 1,000 employees worldwide, as part of a corporate restructuring caused by the COVID-19 pandemic. The team behind Servo was disbanded. The event raised concerns about the future of Rust, as some members of the team were active contributors to Rust. In the following week, the Rust Core Team acknowledged the severe impact of the layoffs and announced that plans for a Rust foundation were underway. The first goal of the foundation would be to take ownership of all trademarks and domain names, and take financial responsibility for their costs.On February 8, 2021, the formation of the Rust Foundation was announced by its five founding companies (AWS, Huawei, Google, Microsoft, and Mozilla). In a blog post published on April 6, 2021, Google announced support for Rust within the Android Open Source Project as an alternative to C/C++.On November 22, 2021, the Moderation Team, which was responsible for enforcing community standards and the Code of Conduct, announced their resignation "in protest of the Core Team placing themselves unaccountable to anyone but themselves". In May 2022, the Rust Core Team, other lead programmers, and certain members of the Rust Foundation board implemented governance reforms in response to the incident.The Rust Foundation posted a draft for a new trademark policy on April 6, 2023, revising its rules on how the Rust logo and name can be used, which resulted in negative reactions from Rust users and contributors.


== Syntax and features ==
Rust's syntax is similar to that of C and C++, although many of its features were influenced by functional programming languages. Hoare described Rust as targeted at "frustrated C++ developers" and emphasized features such as safety, control of memory layout, and concurrency. Safety in Rust includes the guarantees of memory safety, type safety, and lack of data races.


=== Hello World program ===
Below is a "Hello, World!" program in Rust. The fn keyword denotes a function, and the println! macro prints the message to standard output. Statements in Rust are separated by semicolons.


=== Keywords and control flow ===
In Rust, blocks of code are delimited by curly brackets, and control flow is implemented by keywords including if, else, while, and for. Pattern matching can be done using the match keyword. In the examples below, explanations are given in comments, which start with //.


=== Expression blocks ===
Rust is expression-oriented, with nearly every part of a function body being an expression, including control-flow operators. The ordinary if expression is used instead of C's ternary conditional. With returns being implicit, a function does not need to end with a return expression; if the semicolon is omitted, the value of the last expression in the function is used as the return value, as seen in the following recursive implementation of the factorial function:

The following iterative implementation uses the ..= operator to create an inclusive range:


==== Closures ====


=== Types ===
Rust is strongly typed and statically typed. The types of all variables must be known at compilation time; assigning a value of a particular type to a differently typed variable causes a compilation error. Variables are declared with the keyword let, and type inference is used to determine their type. Variables assigned multiple times must be marked with the keyword mut (short for mutable).The default integer type is i32, and the default floating point type is f64. If the type of a literal number is not explicitly provided, either it is inferred from the context or the default type is used.


==== Primitive types ====


==== Standard library ====
Option values are handled using syntactic sugar, such as the if let construction, to access the inner value (in this case, a string):


==== Pointers ====
Rust does not use null pointers to indicate a lack of data, as doing so can lead to null dereferencing. Accordingly, the basic & and &mut references are guaranteed to not be null. Rust instead uses Option for this purpose: Some(T) indicates that a value is present, and None is analogous to the null pointer. Option implements a "null pointer optimization", avoiding any spatial overhead for types that cannot have a null value (references or the NonZero types, for example).Unlike references, the raw pointer types *const and *mut may be null; however, it is impossible to dereference them unless the code is explicitly declared unsafe through the use of an unsafe block. Unlike dereferencing, the creation of raw pointers is allowed inside of safe Rust code.


==== User-defined types ====
User-defined types are created with the struct or enum keywords. The struct keyword is used to denote a record type that groups multiple related values. enums can take on different variants at runtime, with its capabilities similar to algebraic data types found in functional programming languages. Both structs and enums can contain fields with different types. Alternative names for the same type can be defined with the type keyword.The impl keyword can define methods for a user-defined type (data and functions are defined separately). Implementations fulfill a role similar to that of classes within other languages.


==== Type conversion ====


=== Ownership and lifetimes ===
Rust's ownership system consists of rules that ensure memory safety without using a garbage collector. At compile time, each value must be attached to a variable called the owner of that value, and every value must have exactly one owner. Values are moved between different owners through assignment or passing a value as a function parameter.  Values can also be borrowed, meaning they are temporarily passed to a different function before being returned to the owner. With these rules, Rust can prevent the creation and use of dangling pointers:

Because of these ownership rules, Rust types are known as linear or affine types, meaning each value can be used exactly once. This enforces a form of software fault isolation as the owner of a value is solely responsible for its correctness and deallocation.Lifetimes are usually an implicit part of all reference types in Rust. Each lifetime encompasses a set of locations in the code for which a variable is valid. For example, a reference to a local variable has a lifetime corresponding to the block it is defined in:

The borrow checker in the Rust compiler uses lifetimes to ensure that the values a reference points to remain valid. It also ensures that a mutable reference exists only if no immutable references exist at the same time. In the example above, the subject of the reference (variable x) has a shorter lifetime than the lifetime of the reference itself (variable r), therefore the borrow checker errors, preventing x from being used from outside its scope. Rust's memory and ownership system was influenced by region-based memory management in languages such as Cyclone and ML Kit.Rust defines the relationship between the lifetimes of the objects created and used by functions, using lifetime parameters, as a signature feature.When a stack or temporary variable goes out of scope, it is dropped by running its destructor. The destructor may be programmatically defined through the drop function. This technique enforces the so-called resource acquisition is initialization (RAII) design pattern, in which resources, such as file descriptors or network sockets, are tied to the lifetime of an object: when the object is dropped, the resource is closed.The example below parses some configuration options from a string and creates a struct containing the options. The struct only contains references to the data; so, for the struct to remain valid, the data referred to by the struct must be valid as well. The function signature for parse_config specifies this relationship explicitly. In this example, the explicit lifetimes are unnecessary in newer Rust versions, due to lifetime elision, which is an algorithm that automatically assigns lifetimes to functions if they are trivial.


=== Memory safety ===
Rust is designed to be memory safe. It does not permit null pointers, dangling pointers, or data races. Data values can be initialized only through a fixed set of forms, all of which require their inputs to be already initialized.Unsafe code can subvert some of these restrictions, using the unsafe keyword. Unsafe code may also be used for low-level functionality, such as volatile memory access, architecture-specific intrinsics, type punning, and inline assembly.


=== Memory management ===
Rust does not use garbage collection. Memory and other resources are instead managed through the "resource acquisition is initialization" convention, with optional reference counting. Rust provides deterministic management of resources, with very low overhead. Values are allocated on the stack by default, and all dynamic allocations must be explicit.The built-in reference types using the & symbol do not involve run-time reference counting. The safety and validity of the underlying pointers is verified at compile time, preventing dangling pointers and other forms of undefined behavior. Rust's type system separates shared, immutable references of the form &T from unique, mutable references of the form &mut T. A mutable reference can be coerced to an immutable reference, but not vice versa.


=== Polymorphism ===


==== Generics ====
Rust's more advanced features include the use of generic functions. A generic function is given generic parameters, which allow the same function to be applied to different variable types. This capability reduces duplicate code and is known as parametric polymorphism.
The following program calculates the sum of two things, for which addition is implemented using a generic function:

At compile time, polymorphic functions like sum are instantiated with the specific types the code requires; in this case, sum of integers and sum of floats.
Generics can be used in functions to allow implementing a behavior for different types without repeating the same code. Generic functions can be written in relation to other generics, without knowing the actual type.


==== Traits ====
Rust's type system supports a mechanism called traits, inspired by type classes in the Haskell language, to define shared behavior between different types. For example, the Add trait can be implemented for floats and integers, which can be added; and the Display or Debug traits can be implemented for any type that can be converted to a string. Traits can be used to provide a set of common behavior for different types without knowing the actual type. This facility is known as ad hoc polymorphism.
Generic functions can constrain the generic type to implement a particular trait or traits; for example, an add_one function might require the type to implement Add. This means that a generic function can be type-checked as soon as it is defined. The implementation of generics is similar to the typical implementation of C++ templates: a separate copy of the code is generated for each instantiation. This is called monomorphization and contrasts with the type erasure scheme typically used in Java and Haskell. Type erasure is also available via the keyword dyn (short for dynamic). Because monomorphization duplicates the code for each type used, it can result in more optimized code for specific-use cases, but compile time and size of the output binary are also increased.In addition to defining methods for a user-defined type, the impl keyword can be used to implement a trait for a type. Traits can provide additional derived methods when implemented. For example, the trait Iterator requires that the next method be defined for the type. Once the next method is defined, the trait can provide common functional helper methods over the iterator, such as map or filter.


==== Trait objects ====
Rust traits are implemented using static dispatch, meaning that the type of all values is known at compile time; however, Rust also uses a feature known as trait objects to accomplish dynamic dispatch (also known as duck typing). Dynamically dispatched trait objects are declared using the syntax dyn Tr where Tr is a trait. Trait objects are dynamically sized, therefore they must be put behind a pointer, such as Box. The following example creates a list of objects where each object can be printed out using the Display trait:

If an element in the list does not implement the Display trait, it will cause a compile-time error.


=== Iterators ===
For loops in Rust work in a functional style as operations over an iterator type. For example, in the loop

0..100 is a value of type Range which implements the Iterator trait; the code applies the function f to each element returned by the iterator. Iterators can be combined with functions over iterators like map, filter, and sum. For example, the following adds up all numbers between 1 and 100 that are multiples of 3:


=== Macros ===
It is possible to extend the Rust language using macros.


==== Declarative macros ====
A declarative macro (also called a "macro by example") is a macro that uses pattern matching to determine its expansion.


==== Procedural macros ====
Procedural macros are Rust functions that run and modify the compiler's input token stream, before any other components are compiled. They are generally more flexible than declarative macros, but are more difficult to maintain due to their complexity.Procedural macros come in three flavors:

Function-like macros custom!(...)
Derive macros #[derive(CustomDerive)]
Attribute macros #[custom_attribute]The println! macro is an example of a function-like macro. Theserde_derive macro provides a commonly used library for generating code
for reading and writing data in many formats, such as JSON. Attribute macros are commonly used for language bindings, such as the extendr library for Rust bindings to R.The following code shows the use of the Serialize, Deserialize, and Debug-derived procedural macros
to implement JSON reading and writing, as well as the ability to format a structure for debugging.


==== Variadic macros ====


=== Interface with C and C++ ===
Rust has a foreign function interface (FFI) that can be used both to call code written in languages such as C from Rust and to call Rust code from those languages. As of 2023, an external library called CXX exists for calling to or from C++. Rust and C differ in how they lay out structs in memory, so Rust structs may be given a #[repr(C)] attribute, forcing the same layout as the equivalent C struct.


== Ecosystem ==
The Rust ecosystem includes its compiler, its standard library, and additional components for software development. Component installation is typically managed by rustup, a Rust toolchain installer developed by the Rust project.


=== Compiler ===
The Rust compiler is named rustc, and translates Rust code into a low level language called LLVM intermediate representation (LLVM IR). LLVM is then invoked as a subcomponent to translate IR code into machine code. A linker is then used to combine multiple crates together as a single executable or binary file.Other than LLVM, the compiler also supports using alternative backends such as GCC and Cranelift for code generation. The intention of those alternative backends is to increase platform coverage of Rust or to improve compilation times.


=== Standard library ===
The Rust standard library defines and implements many widely used custom data types, including core data structures such as Vec, Option, and HashMap, as well as smart pointer types. Rust also provides a way to exclude most of the standard library using the attribute #![no_std]; this enables applications, such as embedded devices, which want to remove dependency code or provide their own core data structures. Internally, the standard library is divided into three parts, core, alloc, and std, where std and alloc are excluded by #![no_std].


=== Cargo ===
Cargo is Rust's build system and package manager. It downloads, compiles, distributes, and uploads packages—called crates—that are maintained in an official registry. It also acts as a front-end for Clippy and other Rust components.By default, Cargo sources its dependencies from the user-contributed registry crates.io, but Git repositories and crates in the local filesystem, and other external sources can also be specified as dependencies.


=== Rustfmt ===
Rustfmt is a code formatter for Rust. It formats whitespace and indentation to produce code in accordance with a common style, unless otherwise specified. It can be invoked as a standalone program, or from a Rust project through Cargo.


=== Clippy ===
Clippy is Rust's built-in linting tool to improve the correctness, performance, and readability of Rust code. As of 2024, it has more than 700 rules.


=== Versioning system ===
Following Rust 1.0, new features are developed in nightly versions which are released daily. During each six-week release cycle, changes to nightly versions are released to beta, while changes from the previous beta version are released to a new stable version.Every two or three years, a new "edition" is produced. Editions are released to allow making limited breaking changes, such as promoting await to a keyword to support async/await features. Crates targeting different editions can interoperate with each other, so a crate can upgrade to a new edition even if its callers or its dependencies still target older editions. Migration to a new edition can be assisted with automated tooling.


=== IDE support ===
The most popular language server for Rust is Rust Analyzer, which officially replaced the original language server, RLS, in July 2022. Rust Analyzer provides IDEs and text editors with information about a Rust project; basic features including autocompletion, and the display of compilation errors while editing.


== Performance ==
In general, Rust's memory safety guarantees do not impose a runtime overhead. A notable exception is array indexing which is checked at runtime, though this often does not impact performance. Since it does not perform garbage collection, Rust is often faster than other memory-safe languages.Rust provides two "modes": safe and unsafe. Safe mode is the "normal" one, in which most Rust is written. In unsafe mode, the developer is responsible for the code's memory safety, which is useful for cases where the compiler is too restrictive.Many of Rust's features are so-called zero-cost abstractions, meaning they are optimized away at compile time and incur no runtime penalty. The ownership and borrowing system permits zero-copy implementations for some performance-sensitive tasks, such as parsing. Static dispatch is used by default to eliminate method calls, with the exception of methods called on dynamic trait objects. The compiler also uses inline expansion to eliminate function calls and statically-dispatched method invocations.Since Rust utilizes LLVM, any performance improvements in LLVM also carry over to Rust. Unlike C and C++, Rust allows for reordering struct and enum elements to reduce the sizes of structures in memory, for better memory alignment, and to improve cache access efficiency.


== Adoption ==

Rust has been used in software across different domains. Rust was initially funded by Mozilla as part of developing Servo, an experimental parallel browser engine, in collaboration with Samsung. Components from the Servo engine were later incorporated in the Gecko browser engine underlying Firefox. In January 2023, Google (Alphabet) announced support for third party Rust libraries in Chromium and consequently in the ChromeOS code base.Rust is used in several backend software projects of large web services. OpenDNS, a DNS resolution service owned by Cisco, uses Rust internally. Amazon Web Services began developing projects in Rust as early as 2017, including Firecracker, a virtualization solution; Bottlerocket, a Linux distribution and containerization solution; and Tokio, an asynchronous networking stack. Microsoft Azure IoT Edge, a platform used to run Azure services on IoT devices, has components implemented in Rust. Microsoft also uses Rust to run containerized modules with WebAssembly and Kubernetes. Cloudflare, a company providing content delivery network services uses Rust for its firewall pattern matching engine and the Pingora web server.In operating systems, Rust support has been added to Linux and Android. Microsoft is rewriting parts of Windows in Rust. The r9 project aims to re-implement Plan 9 from Bell Labs in Rust. Rust has been used in the development of new operating systems such as Redox, a "Unix-like" operating system and microkernel, Theseus, an experimental operating system with modular state management,, and most of Fuchsia. Rust is also used for command-line tools and operating system components, including stratisd, a file system manager and COSMIC, a desktop environment by System76.
In web development, the npm package manager started using Rust in production in 2019. Deno, a secure runtime for JavaScript and TypeScript, is built with V8, Rust, and Tokio. Other notable adoptions in this space include Ruffle, an open-source SWF emulator, and Polkadot, an open source blockchain and cryptocurrency platform.Discord, an instant messaging social platform uses Rust for portions of its backend, as well as client-side video encoding. In 2021, Dropbox announced their use of Rust for a screen, video, and image capturing service. Facebook (Meta) used Rust for Mononoke, a server for the Mercurial version control system.In the 2023 Stack Overflow Developer Survey, 13% of respondents had recently done extensive development in Rust. The survey also named Rust the "most loved programming language" every year from 2016 to 2023 (inclusive), based on the number of developers interested in continuing to work in the same language. In 2023, Rust was the 6th "most wanted technology", with 31% of developers not currently working in Rust expressing an interest in doing so.


== Community ==


=== Rust Foundation ===
The Rust Foundation is a non-profit membership organization incorporated in United States, with the primary purposes of backing the technical project as a legal entity and helping to manage the trademark and infrastructure assets.It was established on February 8, 2021, with five founding corporate members (Amazon Web Services, Huawei, Google, Microsoft, and Mozilla). The foundation's board is chaired by Shane Miller. Starting in late 2021, its Executive Director and CEO is Rebecca Rumbul. Prior to this, Ashley Williams was interim executive director.


=== Governance teams ===
The Rust project is composed of teams that are responsible for different subareas of the development. The compiler team develops, manages, and optimizes compiler internals; and the language team designs new language features and helps implement them. The Rust project website lists 9 top-level teams as of January 2024. Representatives among teams form the Leadership council, which oversees the Rust project as a whole.


== See also ==
Comparison of programming languages
History of programming languages
List of programming languages
List of programming languages by type


== Notes ==


== References ==


=== Book sources ===


=== Others ===


== Further reading ==
Blandy, Jim; Orendorff, Jason; Tindall, Leonora F. S. (2021-07-06). Programming Rust: Fast, Safe Systems Development. O'Reilly Media. ISBN 978-1-4920-5259-3.


== External links ==

Official website
