# OOP -- Object Oriented Programming
---

## Class
- Class is a blueprint for creating objects, attributes and methods
- 
```
class car:
    pass

audi=car()
bmw=car()
```

## Object
- Object is an instance of a class
- 

## Constructor
- Constructor is a special method that is called when an object is created
- It is used to initialize the object
- It is called automatically when an object is created
- It is defined using the __init__ method
- 
```
class car:
    def __init__(self,name,model):
        self.name=name
        self.model=model

audi=car("Audi","A4")
print(audi.name)
print(audi.model)
```