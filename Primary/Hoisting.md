# Hoisting

In Javascript we have hoisting. This is a default behavior where declerations in a scope or a within a function is moved to the top of the scope or function. 

Variables that are defined with let and const are hoisted up to the top of the block but they are not **initialized**.

This means that the code block is aware of the variable but cannot use it before it is declared. Trying to use it before declaring the variable will lead to a `ReferenceError`.

Its important to know that JS only hoists declarations not initializations. 



---
status: #🌱 
Tags: [[Programming]]-[[Javascript]]