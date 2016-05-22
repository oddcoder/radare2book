## Working with data types

Radare2 can also work with data types. You can use standart C data types or define your own using C. Currently their is support for structs, unions, function signatures, and enums.

```

[0x00000000]> t?
|Usage: t # cparse types commands
| t                       List all loaded types
| t <type>                Show type in 'pf' syntax
| t*                      List types info in r2 commands
| t- <name>               Delete types by its name
| t-*                     Remove all types
| tb <enum> <value>       Show matching enum bitfield for given number
| te                      List all loaded enums
| te <enum> <value>       Show name for given enum number
| td <string>             Load types from string
| tf                      List all loaded functions signatures
| tk <sdb-query>          Perform sdb query
| tl[?]                   Show/Link type to an address
| to -                    Open cfg.editor to load types
| to <path>               Load types from C header file
| tp <type>  = <address>  cast data at <adress> to <type> and print it
| ts                      print loaded struct types
| tu                      print loaded union types
[0x00000000]> 

```

### Defining new types

Their is three different methods to define new types:
1- Defining new type from r2 shell immediately, to do this you will use `td` command, and put the whole line between double quotes. Ex:
    "td struct person {int age; char *name; char *address;};"

2- You can also use `to -` to open text editor and write you own types in there. This is preferable when you got too many types to define.

3- Radare2 also supports loading header files using the command `to` followed by path to the the header file you want to load.

You can View loaded types in r2 using `ts` for structures, `tu` for uninos, `tf` for functions signatures, ect...

You can also cast pointers to data types and view data in there accordingaly with `tp`. EX:

```
[0x00400511]> tp person = 0x7fff170a46b0
       age : 0x7fff170a46b0 = 20
       name : (*0x4005b0) 0x7fff170a46b4 = My name
       address : (*0x4005b8) 0x7fff170a46bc = My age
[0x00400511]> 
```

