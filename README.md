Calculating frequency of characters in a string.
In this article we will learn how to write a C++ program to calculate the frequency of characters in a string. First we have to find out unique characters from the string as calculating frequency means how many times each character is present in the string.

We will use a for loop that will count how many times every unique character is present in the string. Then to print the result we will use another for loop.

Calculate Frequency of Characters in C
Methods Discussed
Method 1: Simple iterative using ASCII frequency array (For Loop)
Method 2: Simple iterative using ASCII frequency array (while Loop)
Method 3: Using inbuilt method count
Method 4: Using recursion
Method 5: Using an additional visited array
Method 6: Using sorted last occurrence counting
count the number of occurrences of each character in a string in C++
Method 1
C++ programming code to calculate the frequency of characters in a string
Objective: Write a C++ Program to count the number of occurrences of each character in a string

Algorithm:
Initialize the variables.
Accept the input.
Initialize a for loop.
This for loop will be used to count the number of time each character is present.
Terminate first at the end of string. 
Initialize another for loop to print the frequency if it is at least 1.
While loop in C
Run
#include <iostream>
using namespace std;

int main()
{
    //Initializing variables.
    char str[100]="prepinsta";
    int i;
    int freq[256] = {0};
    
    //Calculating frequency of each character.
    for(i = 0; str[i] != '\0'; i++)
    {
        freq[str[i]]++;
    }
    
    //Printing frequency of each character.
    for(i = 0; i < 256; i++)
    {
        if(freq[i] != 0)
        {
           cout<<"The frequency of "<<char(i)<<" is "<<freq[i]<<endl;
        }
    }
    return 0;
}
Output
The frequency of a is 1
The frequency of e is 1
The frequency of i is 1
The frequency of n is 1
The frequency of p is 2
The frequency of r is 1
The frequency of s is 1
The frequency of t is 1

Method 2
In this method, we create an array that can hold 256 values and initialize all indices to 0.

We will read the string iteratively and for each character, we increment the count.

Example –

If we reach a
We will increment the count of arr[97] to 1
Since ASCII of a is 97
Run
#include<bits/stdc++.h>
using namespace std;

int main() {
    char str[100] = "I am a String";
    
    // to store the count of each ascii character
    int frequency[256] = {0};
    
    int ascii;
    int i = 0;
    
    while (str[i] != '\0') {
        ascii = str[i];
        ++frequency[ascii];
        i++;
    }
   cout << "Frequency :" << endl;
   
   for (i = 1; i < 256; i++){ 
        if(frequency[i] > 0)
           cout << char(i) << " : "<< frequency[i] << endl;
   }
   return 0;
}
Output
Frequency :
  : 3
I : 1
S : 1
a : 2
g : 1
i : 1
m : 1
n : 1
r : 1
t : 1
Method 3
We use the inbuilt function count to calculate the count of each character in the ASCII range 1 – 256.

Run
#include<bits/stdc++.h>
using namespace std;
 
int main(){
    string str = "PrepInsta is the best";
    
    // checking frequency of each character in ASCII Table
    // ASCII has 256 in modern systems
    for(int i = 1; i < 256; i++)
    {
        int ch = (char) i;
        
        // inbuilt function to calculate count
        int freq = count(str.begin(), str.end(), ch);
        
        // only print if frequency > 0
        if(freq > 0){
            cout << (char) i << ": ";
            cout << freq << endl;
        }
        
    }
}
Output
: 3
I: 1
P: 1
a: 1
b: 1
e: 3
h: 1
i: 1
n: 1
p: 1
r: 1
s: 3
t: 3
Related Pages
Juggling algorithm for array rotation
 
Balanced Parenthesis Problem
 
Toggle each character in a string

Count the number of vowels

Length of the string without using strlen() function

Prime Course Trailer

Related Banners
Get PrepInsta Prime & get Access to all 200+ courses offered by PrepInsta in One Subscription

Get Prime
Method 4
This method uses Recursion in C++

Run
#include<bits/stdc++.h>
using namespace std;

// recursive function to get frequency of a character in a string
int getFrequency(char ch, string str)
{
    // base case
    // if string length becomes 0
    if (str.length() == 0)
        return 0;
    
    int count = 0;
 
    // check if the first character of
    // the given string == ch or not
    if (str[0] == ch)
        count++;
 
    // calling recursive function to find count of ch
    // in string by sending next index getting count
    // from index 1 to the end of the string
    count += getFrequency(ch, str.substr(1));
 
    return count;
}
 
int main(){
    string str = "PrepInsta is the best";
    
    // checking frequency of each character in ASCII Table
    // ASCII has 256 in modern systems
    for(int i = 1; i < 256; i++)
    {
        int result = getFrequency((char) i, str);
        
        // only print if frequency > 0
        if(result > 0){
            cout << (char) i << ": ";
            cout << result << endl;
        }
        
    }
}
Output
: 3
I: 1
P: 1
a: 1
b: 1
e: 3
h: 1
i: 1
n: 1
p: 1
r: 1
s: 3
t: 3
Method 5
This method uses an additional visited array.

Inspiration for this method has been taken from here –

C++ program to find the frequency of elements in an array

Run
#include<bits/stdc++.h>
using namespace std;

// Main function to run the program
int main() 
{ 
    string arr = "PrepInsta is the best";
    int n = sizeof(arr)/sizeof(arr[0]); 

    int visited[n];

    for(int i = 0; arr[i] != '\0'; i++){

        if(visited[i] != 1){
           int count = 1;
           for(int j = i + 1; j < n; j++){
              if(arr[i] == arr[j]){
                 count++;
                 visited[j] = 1;
              }
            }

            cout << arr[i] << " : " << count << endl;
         }
     }

    return 0; 
}
Output
P : 1
r : 1
e : 3
p : 1
I : 1
n : 1
s : 3
t : 3
a : 1
  : 3
i : 1
h : 1
b : 1
Method 6
This method sorts the string first and then counts the occurrences using last occurrence methods.

Inspiration for this method has been taken from here –

C++ program to find the frequency of elements in an array

Run
#include <iostream>
#include <algorithm>
using namespace std;
 
void countDistinct(char arr[], int n)
{

    sort(arr, arr + n);
 
    // Traverse the sorted array
    for (int i = 0; i < n; i++){
        int count = 1;

        // Move the index ahead whenever
        // you encounter duplicates
        while (i < n - 1 && arr[i] == arr[i + 1]){
            i++;
            count++;
        }
        
        cout << arr[i] << ": " << count << endl;
    }
 
}
 
// Driver program to test above function
int main()
{
    char arr[] = "prepinsta is the best";
    int n = sizeof(arr)/sizeof(arr[0]); 
    
    // send n-1 to remove '\0'
    countDistinct(arr, n-1);
    return 0;
}
Output
 : 3
a: 1
b: 1
e: 3
h: 1
i: 2
n: 1
p: 2
r: 1
s: 3
t: 3
