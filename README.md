
# Filter in Python

### Learning Objectives

* Understand how filtering with a for loop has common code that can be abstracted, or moved, to a function
* Understand how to use the `filter` function in Python

### Filtering Elements

When discussing conditionals, we saw how an `if` statement could be combined with a for loop to return a subset of a list that meets certain conditions.  We did so by iterating through a list of elements and adding the element to a new list when an element met certain conditions.  For example, imagine we want to write a function that selects even numbers, how would we do this?

### First solve it for one element

Before determining how to categorize all elements in a list, let's just answer the question of whether one element is even.  We can do so by making use of the modulo operator, `%`.  The % returns the remainder resulting from dividing a number by another.  For example:


```python
7 % 3
```




    1



Seven divided by three, is two with a remainder of one.  So the modulo operator returns the remainder, one.  Let's look at some other examples.  Six divides into three two times leaving a remainder of zero. So the operator returns zero.


```python
6 % 3
```




    0



And four divided by two also brings a remainder of zero.


```python
4 % 2
```




    0



Note that the above line effectively asks (and answers) whether 4 is even.  This is because the statement 4 modulo two returns zero means that four divided by two has a remainder of zero, and as we know, any number that is divisible by two with no remainder leftover is an even number.

Similarly, if a number is odd, then dividing by the number two results in a remainder of one. Ok so now let's write a function that checks if a number is even. 


```python
def is_even(number):
    return number % 2 == 0
```


```python
print(is_even(3)) # False
print(is_even(100)) # True
```

    False
    True


### Then solve for all

Now we are ready to write our function that selects just even numbers.  We can iterate through the numbers one by one, and for each number, check if that number is even.  If it's even then append the element to a new list of even numbers.


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



Notice that our two functions `select_ing` and `select_even` share a lot of similarity.  Below, let's just highlight the differences.

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
filter(is_even,numbers)
```




    <filter at 0x102c346a0>



Note that `filter` returns a filter object, which isn't much use to us.  What does a `filter` object do?  Not much.  So we coerce it to a list and to see just the even numbers.


```python
list(filter(is_even, numbers))
```




    [0, 2, 4, 6, 8, 10]



Also notice that the `filter` function takes two arguments, the first is the function itself.    The function goes through each element, and passes that element into the criteria function.  If that criteria function returns a truthy value, the element is selected.  If not, the element is not selected. 


```python
list(filter(ends_ing, words))
```




    ['camping', 'biking']



> Note that when passing through the function, no parentheses are added at the end of the function.  This is important.  If we pass through the parentheses the filtering will not occur.

### Summary

In this section, we learned about the `filter` function, which selects the elements in a list that match a specific criteria. We learned that `filter` takes in two arguments. The first is the function that specifies the criteria specifying which elements to select, and the second argument is the list of elements to filter. Each element in the list is passed to the function one by one and if the function returns true the element is selected and put into a new array, which will be returned in the Filter object at the end.
