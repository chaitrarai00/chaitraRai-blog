---
title: First Unique character in a String
date: "2020-05-04T22:40:32.169Z"
description: The problem statement is to find the first non-repeating character in a given input string and return its index. If all characters are repeated / occurs more than once we return -1 indicating there is no such unique character.
---

The problem statement is to find the first non-repeating character in a given input string and return its index. If all characters are repeated / occurs more than once we return -1 indicating there is no such unique character.

Lets look into the solutions to approach this problem one by one.

The first approach that I can think of is where we store the count array as per the characters in the stream. something like this

```java
static final int NO_OF_CHARS=256;
static int count[]=new int [NO_OF_CHARS];
```

```java
for (int i=0;i<str.length();i++){

  count[Character.getNumericValue(str.charAt(i))] = count[Character.getNumericValue(str.charAt(i))+1;

 }
```

We iterate through the entire string and update count by incrementing the count value for corresponding character. Hence we get the array with the counts! Now, the character with exactly count equal to 1 would be the ones that never repeat which means we iterate through the string again.

```java
for(int i=0;i<s.length();i++) {
      if(count[Character.getNumericValue(s.charAt(i))]==1)
                    return i;
}
```

This has a time complexity of O(n^2) taking n time to iterate and find the count and n time to iterate over the string again and check its corresponding count. The space complexity would be O(n) with the creating of array of character count.

Now lets try to optimize the above solution

Lets create a hashmap instead with key as the characters and count of the character as values. Note that just by doing that we do not keep track of the index since maps store data in an unordered manner and hence the first repeating character might get lost since map do not keep hold of the sequence. Hmm… now what?

so why not make the value store both count and the index together. We create a class CountIndex with a count and index value:

```java
public class CountIndex {
     public int count,index;
     public CountIndex(int index) {
         this.count=1;
         this.index=index;
     }
 public void increment_count() {
     this.count++;
  }

static final int NO_OF_CHARS=256;
static HashMap<Character, CountIndex> charcount=new HashMap(NO_OF_CHARS);

for(int i=0;i<str.length();i++) {
  if(charcount.containsKey(str.charAt(i))) {
    charcount.get(str.charAt(i)).increment_count();
  }
  else {
    charcount.put(str.charAt(i), new CountIndex(i));
    }
}
```

seems fine? Now, once we get this hashmap ready we check for key value pair with count=1 and index the least.

We can start by setting the result to a maximum value and go aghead finding the least possible index in the character stream/ array.

```java
int result_index=Integer.MAX_VALUE;
 for(Map.Entry entry:charcount.entrySet()) {
             int count=entry.getValue().count;
             int current_index=entry.getValue().index;
             if(count==1 && current_index<result) {
                 result_index=current_index;
             }
         }
```

Retrieval from hashmap happens in linear time and the time to add key value would be depedent on length of the string.

The resulting the time complexity would be O(1)+O(n) so–> O(n) .The hashmap is created would result in a space complexity of O(n).
