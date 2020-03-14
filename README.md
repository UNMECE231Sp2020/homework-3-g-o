# Homework3
Fourth homework of ECE 231: Intermediate Programming. Assigned 3/9/2020. Due 3/14/2020, 11:59 pm.

## Instructions
A class will be created that will act like a container for a doubly linked list. However, the class will not be held down by an particular data type. This will be done with templates. The class will be called `List` and the template declaration for the class will look like this:

    template<class Data> class List
    
The letter `Data` can change, and can be changed to whatever you want. Below is an example of the private data members should look like:
    
    template<class Data> class List {
      private:
      struct _list {
        Data value;
        struct _list *next;
        struct _list *prev;
      };
      typedef struct _list Dlist;
      
      size_t _size;
      Dlist *_front;
      Dlist *_back;
      
      void reccopy(const Dlist *ptr) {
        if(ptr) {
          reccopy(ptr->next);
          push_front(ptr->value);
        }
      }
      
Uncomment the line `push_front(ptr->value)` after you have implemented the function `push_front`. You have been given two constructors, a default constructor, and a copy constructor. The copy constructor should call `reccopy`.

    List()
    List(const List &list)
    
Where `list` is another `List` class. You must also implement a destructor that removes all nodes using `pop_front` and `empty` functions.

    ~List()
    
Three getters need to be implemented, one what gets the first value of the list, the last value of the list, and the size of the list.

    front()
    back()
    size()
    
You are also going to overload the `=` operator to copy the class to another class

    List &operator=(const List &x)
Where `x` is a variable of your choosing. Using `x` as the input variable, you must create a loop that iterates from `x._front` until the `nullptr`, calling `push_back` in the body of you code. Remember, `x._front` is a doubly linked list that should be moving forward, keep that in mind as you step through the loop.

You have been given these two push functions:

    void push_back(const Data &value)
    void push_front(const Data &value)
    
Where `Data` is your template name, and `value` is the value that you are adding to the `List` class (`value` can be changed). Make sure that you consider two cases: where there is no nodes and where at least one node already exists.

Next comes the pop functions:

    void pop_back()
    void pop_front()
    
Remember, consider two cases: when there is more than one node in your list class, and when there is only one node. `pop_front()` has been completed `pop_front()` must be converted from using a single linked list to a doubly linked list. 

This function has been given to you to determine if the `List` class is empty:
  
    bool empty() const
    
You need to create a function that prints the contents of the `List` class. Both forwards and backwards.

    void print()
    void print_back()
    
Finally, two friend functions are going to be created:

    template<typename V> friend bool operator==(const List<V> &a, const List<V> &b)
    template<typename V> friend bool operator!=(const List<V> &a, const List<V> &b)
    
These functions should compare two `List` classes with each other to check if they are the same or not (hint: use a for loop).
    
You'll be provided with a file `main.cpp` that will test your class, as well as `GeneralList.hpp`. You will need to finishing implementing the `List` class in `GeneralList.hpp`. Feel free to rename `GeneralList.hpp` to somthing else using the `git mv` command.

## Rubric
    Executable runs with no errors: 20%
    Implementation of functions in GeneralList.hpp: 40%
    Creation of Makefile: 20%
    Clean code: 20%
