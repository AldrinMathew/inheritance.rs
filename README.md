# Inheritance in `rust`

Explanation about implementing inheritance in `rust`. The following example will serve as the foundation for further explanation of related concepts and ideas.

```rust
use std::string::String;

pub struct Human<T> {
    name: String,
    age: u8,
    address: String,
    _derived: T,
}
pub type HumanTy = Human<()>;

pub struct Employee {
    id: String,
    salary: u64,
    title: String,
}
pub type EmployeeTy = Human<Employee>;

pub struct Employer {
    section: String,
    employees: Vec<Employee>
}
pub type EmployerTy = Human<Employer>;

```

In this case,

- `Human<T>` is the generic type representing all possible variations of the datatype.
- `Human<()>` is the base type that is not derived in any way.
- `Human<Employee>` and `Human<Employer>` are derived types.

The data for an instance of the derived type is stored alongside the base type. The somewhat popular way to achieve inheritance in Rust is adding the instance of the base class as a member of the the derived class. But this makes the rest of the design and implementation redundant. Basically you will have to write base functions for all derived types in such a scenario. The above method however can avoid that problem.

## Base Functions

Base functions in this context means functions that can be called on the base type as well as all derived types. Translating this feature to Rust, it makes more sense to call these ***Generic Base Functions***. Because in order to be able to call these functions on all possible variations of the base type, you will have to implement functions for `Human<T>` and not `Human<()>`.
Coming from other languages like C++, Java, Dart... that has extensive support for Object Oriented Programming, one would assume that the implementations should be for `Human<()>`. However `Human<()>` is also a derived datatype and so any functions implemented for `Human<()>` will be limited to that type.