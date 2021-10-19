
# Data Types

There are two types of data types:
• System-defined data types (also called Primitive data types)
• User-defined data types


## System-defined data types (Primitive data types)

Data types that are defined by system are called primitive data types. The primitive data types provided by many programming languages are: int, float, char, double, bool, etc. The number of bits allocated for each primitive data type depends on the programming languages, the compiler and the operating system. For the same primitive data type, different languages may use different sizes. Depending on the size of the data types, the total available values (domain) will also change.

For example, “int” may take 2 bytes or 4 bytes. If it takes 2 bytes (16 bits), then the total possible values are minus 32,768 to plus 32,767 (-215 to 215-1). If it takes 4 bytes (32 bits), then the possible values are between -2,147,483,648 and +2,147,483,647 (-231 to 231-1). The same is the case with other data types.



## User defined data types

If the system-defined data types are not enough, then most programming languages allow the users to define their own data types, called user – defined data types. Good examples of user defined data types are: structures in C/C + + and classes in Java


# Data Structures

A data structure is a special format for organizing and storing data. General data structure types include arrays, files, linked lists, stacks, queues, trees, graphs and so on.

Depending on the organization of the elements, data structures are classified into two types:

## Linear data structures:
  Elements are accessed in a sequential order but it is not compulsory to store all elements sequentially. Examples: Linked Lists, Stacks and Queues.
## Non – linear data structures:
  Elements of this data structure are stored/accessed in a non-linear order. Examples: Trees and graphs.


# Commonly Used Rates of Growth

The diagram below shows the relationship between different rates of growth.

<img src="./images/rates of growth.png" width="800"  /> 

Below is the list of growth rates.

<img src="./images/growth rates.png" width="800"  /> 

# Linked List

A linked list is a data structure used for storing collections of data. A linked list has the following properties.
• Successive elements are connected by pointers
• The last element points to NULL
• Can grow or shrink in size during execution of a program
• Can be made just as long as required (until systems memory exhausts)
• Does not waste memory space (but takes some extra memory for pointers). It allocates memory as list grows.





