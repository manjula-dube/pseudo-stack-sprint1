
# Understanding Deep and Shallow Copy in Javascript

#### Shallow copy

Shallow copy is a bit-wise copy of an object. A new object is created that has an exact copy of the values in the original object. If any of the fields of the object are references to other objects, just the reference addresses are copied i.e., only the memory address is copied.

#### Deep copy

A deep copy copies all fields, and makes copies of dynamically allocated memory pointed to by the fields. A deep copy occurs when an object is copied along with the objects to which it refers.

###Lets take an example
**Shallow Copy**: 
It makes a copy of the reference to X into Y. Think about it as a copy of X's Address. So, the addresses of X and Y will be the same i.e. they will be pointing to the same memory location.

**Deep copy**: 
It makes a copy of all the members of X, allocates  different memory location for Y and then assigns the copied members to Y to achieve deep copy. In this way, if X vanishes Y is still valid in the memory. 


**The correct term to use would be cloning, where you know that they both are totally the same, but yet different (i.e. stored as two different locations in the memory space).**


Consider this example:

    var employeeDetailsOriginal = {  name: 'Manjula', age: 25, Profession: 'Software Engineer' };
Let's say you want to create a duplicate of this, so that even if you change the original values, you can always return to the original.

I can do this:

    var employeeDetailsDuplicate = employeeDetailsOriginal; //Shallow copy!
If we change a value:

    employeeDetailsDuplicate.name = 'NameChanged';
This statement will also change name from employeeDetailsOriginal, since we have a shallow copy, or a reference to var  employeeDetailsOriginal. This means, you're losing the original data as well.

But, creating a brand new variable by using the properties from the original employeeDetailsOriginal variable, you can create a deep copy.

    var employeeDetailsDuplicate = { name: employeeDetailsOriginal.name, age: employeeDetailsOriginal.age, Profession: employeeDetailsOriginal.Profession}; //Deep copy!
Now if you change employeeDetailsDuplicate.name, it will only affect employeeDetailsDuplicate and not employeeDetailsOriginal

Diagramatic example 

![](https://s30.postimg.org/pjbzvamtd/Screen_Shot_2016_12_08_at_10_27_22_PM.png)

###So  How to copy JavaScript object to new variable NOT by reference?

        	
Your only option is to somehow clone the object.



        For simple JSON objects, the simplest way would be:

        var objectIsNew = JSON.parse(JSON.stringify(objectIsOld));
        //if you use jQuery, you can use:

        In Jquery you can use:

        // Shallow copy
        var objectIsNew = jQuery.extend({}, objectIsOld);

        // Deep copy
        var objectIsNew = jQuery.extend(true, {}, objectIsOld);
        
 Pure javascript method to deep clone object
 
            function keepCloning(objectpassed) {
            if (objectpassed === null || typeof objectpassed !== 'object') {
            return objectpassed;
            }

            var temporary-storage = objectpassed.constructor(); // give temporary-storage the original obj's constructor
            for (var key in objectpassed) {
            temporary-storage[key] = cloneObject(objectpassed[key]);
            }

            return temporary-storage;
            }

            var employeeDetailsOriginal = {  name: 'Manjula', age: 25, Profession: 'Software Engineer' };
            
            var employeeDetailsDuplicate = (keepCloning(employeeDetailsOriginal));
            employeeDetailsOriginal.name = "NameChanged";

            console.log(employeeDetailsOriginal);
            console.log(employeeDetailsDuplicate);
            
            

**Hope now you are clear with deep and shallow copy**
        
