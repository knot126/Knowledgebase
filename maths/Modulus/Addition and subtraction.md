> Written with [StackEdit](https://stackedit.io/).

$a + b \mod{c} = (a \mod{c} + b \mod{c}) \mod c$

They call it modular addition property or some bullshit I hear in school. Similar thing for substraction.

$a - b \mod{c} = (a \mod{c} - b \mod{c}) \mod{c}$

For this one you just have to look at clock arithmetic, it become way easier to see these properties:

```
==================================================== mod C
------------------------~~~~~~~~~~~~~~
A                       + B

=

==================================================== mod C
(
==================================================== mod C
------------------------
A

+

==================================================== mod C
~~~~~~~~~~~~~~
B
}
```
