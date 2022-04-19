# Inheritance in `rust`

The following is a detailed explanation about implementing inheritance in `rust`

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

In this case, the data for an instance of the derived type is stored alongside the base type.

The somewhat popular way to achieve inheritance in Rust is adding the instance of the base class as a member of the the derived class. But this makes the rest of the design and implementation redundant.