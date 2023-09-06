# MyDataStructuresdocs2


Sets-2 JS (CSF)
The first thing you need to know is that Sets are collections of UNIQUE values. Sets often get lumped in with Arrays because they are both data collections, but unlike a Map, a Set is conceptually more similar to an Array than an Object, since it is a list of values and not key/value pairs. However, Set is not a replacement for Arrays, but rather a supplement for providing additional support for working with duplicated data.

Set has many of the same methods and properties as Map, so in this tutorial, we are going to take a different approach where we are going to implement sets in manipulating Moringa school staff data.

Basics

 Let’s cover the basics first.

You can initialize Sets with the new Set() syntax.

const set = new Set()
This gives us an empty Set:

Output

Set(0) {}
Items can be added to a Set with the add() method. (This is not to be confused with the set() method available to Map, although they are similar.)

// Add items to a Set
set.add('Beethoven')
set.add('Mozart')
A Set can be converted into an Array with one line of code:

const arr = [...set]
Output

(3) ["Beethoven", "Mozart", "Chopin"]
Example: Problem Set up

A set is an unordered collection of elements that are all unique. For example, the list of all employees at Moringa is a set. Each employee would be an element in the set. In reality, these elements would be stored using an ID (national or otherwise) because these are values we can ensure will be unique. Note how the order of these elements is irrelevant to us because sorting IDs has no meaning.  

We call our set of employees the universal set because it contains all elements under consideration. Let’s imagine another set. This set is the list of employees in Moringa who work in the engineering department. This is a subset of our employee set because every element in the engineering set also exists in the employee set. Another subset is the list of employees who are freelance contractors. Here is how we would create these sets: 

Note: Remember you can still use your console to test out these code blocks

let engineering = new Set(['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan']);


let freelancers = new Set(['Piccolo','Trunks', 'Vegeta', 'Goku', 'Gohan']);
If you want to add another person to one of our sets, we would use the syntax set.add(value) and replace set with the name of the “department” and value with the “name of the new staff member” being added. If we try to add an element that is already in the set, it will not be added. Example:

let engineering = new Set(['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan']);
engineering.add('Gohan');
console.log(engineering);
This will print Set { 'Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan' }.

Problems:

Now let's see how we can operate on sets to help us solve some common problems.

 

Combining teams

What if we want to find all the employees in our company who are freelancers or who work in the engineering department? We would need to combine the two sets, and then remove any duplicate names. This is called the union. The union of two sets is the set that contains elements from either set or both sets. Notice how elements in our engineering set are also in the freelancers set. Here is one way you can find the union of both sets:

let engineering = new Set(['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan']);
let freelancers = new Set(['Piccolo','Trunks', 'Vegeta', 'Goku', 'Gohan']);
let union = new Set([...engineering, ...freelancers]);
console.log(union);
As we saw earlier in the basics, the … operator turns our set into an array, and after combining the two arrays, the Set constructor removes the duplicate elements. The union of the two sets will be Set {'Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan', 'Piccolo', 'Vegeta', 'Goku' }.

convergence

Suppose we want to find all the employees who are in the engineering department and are freelancers. This is the intersection of the sets. The intersection of two sets is the set containing elements in both sets. 

To reproduce this, we can search through one set and check if each element is in the other set. To check if an element is in a set, we use the has method. Example:

let engineering = new Set(['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan']);
console.log(engineering.has('Alberta'));
This would return true. Using the has method, we can filter our engineering set for items that are also in the freelancers set.

let engineering = new Set(['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan']);
let freelancers = new Set(['Piccolo','Trunks', 'Vegeta', 'Goku', 'Gohan']);
let intersection = new Set([...engineering].filter(x => freelancers.has(x)));
console.log(intersection);
The intersection of engineering and freelancers is Set { 'Trunks', 'Gohan' }. 

 

Divergence

Let’s consider the scenario where we want to find the engineers who are not freelancers. This is the difference. The difference of two sets is the set containing elements that are in the first set, but not in the second set. 

For us, that means we will start with our engineering set, and then remove any elements that are also in the freelancers set. Example:

let engineering = new Set(['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan']);
let freelancers = new Set(['Piccolo','Trunks', 'Vegeta', 'Goku', 'Gohan']);
let difference = new Set([...engineering].filter(x => !freelancers.has(x)));
console.log(difference);
You should be able to see the results in the console where the difference of the engineering set and the freelancers set is Set { 'Alberta', 'Dr. Gero', 'Bulma' }. 

If we want to get the list of people who are freelancers and not engineers, we start with the freelancers set and remove the elements that appear in the engineers set. Example:

let difference = new Set([...freelancers].filter(x => !engineering.has(x)));
console.log(difference);
This gives us a different result. The difference of the freelancers set and the engineering set is Set { 'Piccolo', 'Vegeta', 'Goku' }.

 

Difference

Now, we would like to find who in the company is either an engineer or a freelancer, but not both. This is the symmetric difference. The symmetric difference of two sets is the set containing elements from either set, but not both sets. 

One approach we could use is to find the union of the two sets (everyone who is an engineer, freelancer, or both) and subtract the intersection (everyone who is both an engineer and a freelancer). Combining the techniques we used previously, we can get the symmetric difference with the following code:

let engineering = new Set(['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan']);
let freelancers = new Set(['Piccolo','Trunks', 'Vegeta', 'Goku', 'Gohan']);
let union = new Set([...engineering, ...freelancers]);
let intersection = new Set([...engineering].filter(x => freelancers.has(x)))
let symmetricDifference = new Set([...union].filter(x => !intersection.has(x)));
console.log(symmetricDifference);
The symmetric difference between our engineering set and our freelancers set is Set { 'Alberta', 'Dr. Gero', 'Bulma', 'Piccolo', 'Vegeta', 'Goku' }.

 

Complement

If we have our set of employees and a set of engineers, how could we find the set of all people who are not engineers? One thing we could do is subtract the engineers set from the employees set. This set is the complement to our engineers set in relation to our employees set. Example:

let employees = ['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan', 'Goku', 'Piccolo', 'Vegeta'];
let engineering = new Set(['Alberta', 'Dr. Gero', 'Trunks', 'Bulma', 'Gohan']);
let complement = new Set([...employees].filter(x => !engineering.has(x)));
console.log(complement);
The complement to the engineering set in relation to our employees set is Set { 'Goku', 'Piccolo', 'Vegeta' }.