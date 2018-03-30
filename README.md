
# Filter in Python

### Learning Objectives

* Understand how to filtering with a for loop has common code that can be moved to a function
* Understand how to use the filter function in Python

### Filtering Elements

When discussing conditionals, we saw how an `if` statement could be combined with a for loop to return a subset of the array that meets certain conditions.  We do so by iterating through a list of elements and adding the element to a new list when they meet certain conditions.  For example, imagine we want to write a function that selects even numbers.

### First solve it for one element

Before determining how to categorize all elements in a list, let's focus on just answering whether one element is even.  We can do so by making use of the modulo operator, `%`.  The % returns the remainder of dividing a number by another.  For example:


```python
7 % 3
```




    1



Seven divided by three, is two with a remainder of one.  So the modulo operator returns the remainder, one.  Let's look at some other examples.  Six divides into three two times without a remainder, so the operator returns zero.


```python
6 % 3
```




    0



And four divided by two also brings a remainder of zero.


```python
4 % 2
```




    0



Whenever we follow the modulo operator with the number two, we are determining if a number is even.  If a number is even, then dividing the number by two brings a remainder of zero.  If odd, then dividing the number by two brings a remainder of one.  Ok let's write a function that checks if a number is even. 


```python
def is_even(number):
    return number % 2 == 0
```


```python
is_even(3) # False
is_even(100) # True
```




    True



### Then solve for all

So now we can iterate through the numbers one by one, and for each number, check if that number is even.  If it's even then append it to a new list of even numbers.


```python
def select_even(elements):
    selected = []
    for element in elements:
        if is_even(element):
            selected.append(element)
    return selected
```


```python
numbers = list(range(0, 11, 1))
numbers
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]




```python
select_even(numbers)
```




    [0, 2, 4, 6, 8, 10]



### Find what's common

Returning a subset of elements that meet a specific criteria is something commonly done in Python. And the procedure looks pretty much the same regardless of what we are selecting.  For example, let's now select words that end with `'ing'`.


```python
def ends_ing(word):
    return word.endswith('ing')

def select_ing(elements):
    selected = []
    for element in elements:
        if ends_ing(element):
            selected.append(element)
    return selected

words = ['camping', 'biking', 'sailed', 'swam']
select_ing(words)
```




    ['camping', 'biking']



Notice that our two functions `select_ing` and `select_even` share a lot of similarity.  In fact, let's just highlight the differences.

```python
def select_ing(elements):
#     selected = []
#     for element in elements:
        if ends_ing(element):
#             selected.append(element)
#     return selected

def select_even(elements):
#     selected = []
#     for element in elements:
        if is_even(element):
#             selected.append(element)
#     return selected

```

Essentially, the only thing different between the functions is the criteria of how we are selecting.  The filter function, allows us to filter for specific elements, so long as it knows the criteria and the elements. 


```python
list(filter(is_even,numbers))
```




    [0, 2, 4, 6, 8, 10]




```python
list(filter(ends_ing, words))
```




    ['camping', 'biking']



So for the `filter` function, we pass through a function has a truthy or falsy return value.  The function goes through each element, and passes that element into the criteria function.  If that criteria function returns a truthy value, the element is selected.  If not, the element is not selected. 

### Summary

In this section, we learned about the `filter` function.  The `filter` function selects those elements in a list that match a specific criteria.  The list of elements is provided as the second argument to filter.  The first argument is a function that specifies the criteria of how to select elements.  Each of the elements is passed to the function one by one and if the function returns true the element is selected.
