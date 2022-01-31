## Do you know the difference between for...in and for...of loops in JavaScript?


### for...in: 

`for...in` iterates over through properties of an Object. 

```
//Syntax:  
for (variable in object) {
     statement;
}```


**Example I: Object**

if you use `for...in` loop in Object it returns the **Keys** 

```
const object = {
    loop: "for",
    ds: "Array",
    dataType: "int"
};
for(const i in object) {
    console.log(i);
}
//output
loop
ds
dataType```
**Example II: Array**

if you used `for...in` loop in Array it returns the **index number**

```
const list = ["for", 3, "while", 2];
for(const i in list) {
    console.log(i);
}
//output
0
1
2
3
```

**Example III: String**

in the string `for...in` loop returns the **index number**

```
const str1 = "Hello folks";

for(const i in str1) {
    console.log(i);
}
//output
0
1
2
3
4
5
6
7
8
9
10
```
### for...of:
        
`for...of` iterates through the values of an iterable object such as Array, String, array-like objects (e.g.,  [arguments ](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) or  [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) ),  [TypedArray](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray) ,  [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) ,  [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) , and user-defined iterables.
```
//Syntax:
 for (variable of iterable) {
    statement;
}```
**Example I: Object **

We can't use `for...of` loop in Object. because Object is **not iterable**

![for..of used in object.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1625850906702/TiuwavXRc.png)

**Example II: Array**

If we use `for...of` loop in Array, It returns the **value of the Array**. because Array is **iterable**

```
const list = ["for", 3, "while", 2];
for(const i of list) {
    console.log(i);
}
//output
for
3
while
2
```

**Example III: String**

If we use `for...of` loop in String, It returns the **letter from that String**. because String is** iterable**
```
const str = "Hello folks";
for(const i of list) {
    console.log(i);
}
//output
H
e
l
l
o

f
o
l
k
s
```


### Comparison

![for..in vs for...of.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1625851288625/-1-xJARVD.png)

If you enjoyed learning and find it useful please do like and share so that, it reaches others as well 🤝

## Thanks for reading 😃
I would ❤ to connect with you at  [Twitter](https://twitter.com/verreauxblack)  |  [LinkedIn](https://linkedin.com/in/verreauxblack)  |  [GitHub](https://github.com/verreauxblack) |  [Telegram](https://telegram.me/verreauxblack_blog) .<br>
Let me know in the comment section if you have any doubts or feedback.<br>
See you in my next Blog article, Take care!! <br>**Happy Learning😃😃**
