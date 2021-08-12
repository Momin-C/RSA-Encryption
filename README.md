<!-- PROJECT LOGO -->
<br />
  <p align="center">
  <a href="https://github.com/Momin-C/RSA-Encryption">
    <img src="images/Logo.png" alt="Logo" width="80" height="80">
  </a>
  <h3 align="center">RSA ENCRYPTION</h3>
  <p align="center">
    This program will encrypt a given input using RSA encryption
    <br />
    <a href="https://www.youtube.com/watch?v=z5l0-HlCo2c"><strong>Video Demo</strong></a>
    |
    <a href="images/ENCRYPTION.pdf"><strong>Encryption Infographic</strong></a>
    |
    <a href="images/Exploring Computer Science.pdf"><strong>Exploring Computer Science</strong></a>
  </p>
</p>

<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
    * [Developed Using](#developed-using)
* [Computer Science and Cryptography](#computer-science-and-cryptography)
* [Videos](#videos)
* [Usage](#usage)
* [Roadmap](#roadmap)
  * [Packages](#packages)
  * [Class Methods](#class-methods)
  * [Main Method](#main-method)
* [References](#references)
* [Contact](#contact)

<!-- ABOUT THE PROJECT -->
## About The Project

This project draws the connection between computer science research and encryption by obtaining a user input and using one of the most secure encryption methods (RSA) to encrypt the given input. The code is explained in the [Roadmap](#roadmap) section of the code and uses many packages, methods, loops, conditional statements, user input and output. This program enables the user to safely send messages to anyone and the end user can decrypt this using this program's built in decryption as well.

<!-- DEVELOPED USING -->
### Developed Using
This project was developed using the Atom text editor and was tested using Terminal.
* [Atom](https://atom.io)

<!-- COMPUTER SCIENCE AND CRYPTOGRAPHY -->
## Computer Science and Cryptography
Cryptography is the process where messages are converted into a secure form of numbers to prevent anyone from reading the message (except for the desired reader). Cryptography is used everywhere, from typing in your login information to sending messages to banking, with greater reliance on computers we have developed more advanced methods of encryption to fight against hacking and to protect information.

<!-- VIDEOS  -->
## Videos

Full in-depth use of this program can be found on this link below:

[https://www.youtube.com/watch?v=z5l0-HlCo2c](https://www.youtube.com/watch?v=z5l0-HlCo2c)

GIFs are below.
Inputting `true` to the final prompt

![](images/Encrypted1.gif)

Inputting `false` to the final prompt

![](images/Encrypted2.gif)

<!-- USAGE -->
## Usage

To use this file and test its encryption simply clone the CS-ISU repository onto your computer and run it using an IDE or a compiler of your choice.

NOTE: When running the program, it sometimes takes a while for it to ask for an input due to the large prime numbers being generated. If this is the case re-run the program until it asks for you to input a phrase to decrypt instantly.

```sh
git clone https://github.com/Momin-C/RSA-Encryption.git
```

<!-- ROADMAP -->
## Roadmap

<!-- PACKAGES -->
### Packages

To securely encrypt the given input, three packages/modules needed to be imported

```java
import java.util.*;
import java.math.BigInteger;
import java.security.SecureRandom;
```

To learn more about each package/module, their documentation is in the links below

* [java.util](https://docs.oracle.com/javase/8/docs/api/java/util/package-summary.html)
* [java.math.BigInteger](https://docs.oracle.com/javase/7/docs/api/java/math/BigInteger.html)
* [java.security.SecureRandom](https://docs.oracle.com/javase/8/docs/api/java/security/SecureRandom.html)

<!-- CLASS METHODS -->
### Class Methods

This section will explain in detail how the RSA encryption works

RSA encryption bases itself around prime numbers. the method twoPrimes() generates a secure random number using the java.security.secureRandom package. Big integer is used to create two prime numbers due to complex operations taking place that no data set can handle. These two prime numbers are selected and placed in a BigInteger array and then returned. Code can be seen below.

```java
public static BigInteger [] twoPrimes() {
    /* This method selects two random prime numbers in the length of 512 bits
     * appends these to a BigInteger array and returns it */
    Random rand = new SecureRandom();
    BigInteger primeOne = BigInteger.probablePrime(512, rand);
    BigInteger primeTwo = BigInteger.probablePrime(512, rand);
    BigInteger [] primesSelected = {primeOne,primeTwo};
    return primesSelected;
}//twoPrimes
```

RSA encryption involves the use of two keys, public and private. Aspects of the public key are used to encrypt the message and the private key is used to decrypt the messsage. The public key consists of 'n' which is the product of both the prime numbers and 'e' which is a small exponent. The private and public key aspects are determined below and the

```java
public static BigInteger publicKey(BigInteger [] primes){
    /* This method calculates the publicKey by obtaining the two primes
     * selected in the twoPrimes() method and multiplying them by eachother
     * this value is then returned */
    BigInteger publicKey = primes[0].multiply(primes[1]);
    return publicKey;
}//publicKey

public static BigInteger privateKeyNum(BigInteger [] primes){
    /* This method calculates "phi" or the private key number by obtaining
     * the two primes selected in twoPrimes(), subtracting each of them by 1 and multiplying
     * them by eachother and returns this value */
    BigInteger privateKeyNum = primes[0].subtract(BigInteger.ONE).multiply(primes[1].subtract(BigInteger.ONE));
    return privateKeyNum;
}//privateKeyNum

public static BigInteger smallExponent(BigInteger [] primes, BigInteger privateKeyNum){
    /* This method produces a small exponent which will be used to encrypt the string, it obtains
     * the two prime numbers and the private key number as its parameters, a random
     * number is then generated such that it is greater than 1, is less than the
     * private key number and its greatest GCF with the private key number is 1,
     * this value is then returned */
    BigInteger smallExponent;
    do {
        int num = (int)(privateKeyNum.intValue()*(Math.random()));
        smallExponent = BigInteger.valueOf(num);
    }
    while (smallExponent.compareTo(BigInteger.ONE) <= 0 || smallExponent.compareTo(privateKeyNum) >= 0 || !smallExponent.gcd(privateKeyNum).equals(BigInteger.ONE));
    return smallExponent;
}//smallExponent

public static BigInteger privateKey(BigInteger smallExponent, BigInteger privateKeyNum){
    /* This method obtains the small exponent and the private key number as its parameters
     * to calculate the private key by inversing the small exponent and modding
     * it by the private key number and returns it */
    BigInteger privateKey = smallExponent.modInverse(privateKeyNum);
    return privateKey;
}//privateKey
```

Input is then received from the user in the method getInput(). This string value is then converted into numbers in the numericalValue() method by converting each character into its ASCII code and adding 100 to it. This makes sure that each character's code is 3 digits making it to parse and convert back to string.

```java
public static String getInput(){
    /* This method asks the user to input a string they want to encrypt and returns it */
    System.out.print("Input the phrase you want to encrypt: ");
    String phrase = input.nextLine();
    return phrase;
}//getInput

public static BigInteger numericalValue(String phrase) {
    /* This method obtains the user's string they want to encrypt as its parameter, obtains its
     * ASCII code, appens that to a string and then converts the string to a BigInteger
     * which is then returned. The ASCII code has 100 added to it so each character has
     * three ASCII values making it able to decrypt */
    String numString = "";
    for (int index = 0; index<phrase.length(); index++){
        char indexCharacter = phrase.charAt(index);
        int alphaValue = (int)indexCharacter+100;
        numString+=alphaValue;
    }
    BigInteger num = new BigInteger(numString);
    return num;
}//numericalValue
```
Once these keys are collected, the string converted into a BigInteger is then encrypted.
```java
public static BigInteger encryptedData(BigInteger numericalValue, BigInteger smallExponent, BigInteger publicKey){
    /* This method obtains the numericalValue of the string, the small exponent
     * and the public key, it then encrypts the data by following the formula numerical
     * value ^ small exponent modulo public Key and returns this encrypted data */
    BigInteger encryptedData = numericalValue.modPow(smallExponent,publicKey);
    return encryptedData;
}//encryptedData
```
The data is then decrypted as well and converted back to string format
```java
public static BigInteger decryptedData(BigInteger encryptedData, BigInteger privateKey, BigInteger publicKey){
    /* This method obtains the encrypted data, the private key and the public key and
     * decrypts the data by raising the encrypted data to the power of the private key
     * and then modding it by the public key, this value is then returned */
    BigInteger decryptedData = encryptedData.modPow(privateKey,publicKey);
    return decryptedData;
}//decryptedData

public static String decryptedPhrase(BigInteger decryptedData){
    /* This method obtains the decrypted data and converts the decryptedData
     * to the original String by comparing the ASCII values to their respective
     * characters, this is subtracted by 100 as 100 was previously added and then
     * this string is returned */
    String decrypted = String.valueOf(decryptedData);
    String word = "";
    for (int index = 0; index < decrypted.length(); index+=3){
        int num = Integer.valueOf(decrypted.substring(index,index+3)) -100;
        word+=(char)num;
    }
    return word;
}//decryptedPhrase
```
User input decryption uses the two decryption methods as well but includes these two methods to get the keys from the user
```java
public static boolean decryptAnswer(){
    /* This method asks a user if they want to decrypt a given input
     * and returns this boolean value */
    System.out.println("Do you want the program to decrypt a given input? (true or false): ");
    boolean answer = input.nextBoolean();
    return answer;
}//decryptAnswer

public static BigInteger [] getData(){
    /* This method obtains the big integer to decrypt, the public
     * and private key then returns these three in a BigInteger array */
    System.out.println();
    System.out.println("Input BigInteger to decrypt: ");
    BigInteger toDecrypt = input.nextBigInteger();

    System.out.println();
    System.out.println("Input private key: ");
    BigInteger privateKey = input.nextBigInteger();

    System.out.println();
    System.out.println("Input public key: ");
    BigInteger publicKey = input.nextBigInteger();

    BigInteger [] data = {toDecrypt,privateKey,publicKey};
    return data;
}//getData
```
<!-- MAIN METHOD -->
### Main Method

The main method calls every method and assigns their return values to appropriate variables, the relevant variables are then printed. The main method also asks the user if they want to decrypt a given input, if true then the methods getData, decryptedData and decryptedPhrase are executed.
```java
public static void main(String args[]) {
    /* The main method calls every method and assigns their values to variables */

    //Calling all methods
    BigInteger [] primes = twoPrimes();
    BigInteger publicKey = publicKey(primes);
    BigInteger privateKeyNum = privateKeyNum(primes);
    BigInteger smallExponent = smallExponent(primes,privateKeyNum);
    String phrase = getInput();
    BigInteger privateKey = privateKey(smallExponent,privateKeyNum);
    BigInteger numericalValue = numericalValue(phrase);
    BigInteger encryptedData = encryptedData(numericalValue,smallExponent,publicKey);
    BigInteger decryptedData = decryptedData(encryptedData,privateKey,publicKey);
    String decryptedPhrase = decryptedPhrase(decryptedData);

    //Printing out the values
    System.out.println();
    System.out.println("ENCRYPTED:");
    System.out.println(encryptedData);

    System.out.println();
    System.out.println("PUBLIC KEY");
    System.out.println(publicKey);

    System.out.println();
    System.out.println("PRIVATE KEY");
    System.out.println(privateKey);

    System.out.println();
    System.out.println("DECRYPTED PHRASE");
    System.out.println(decryptedPhrase);

    //Asking user if they want to decrypt an integer
    System.out.println();
    boolean decryptAnswer = decryptAnswer();
    if (decryptAnswer){
        BigInteger [] inputtedData = getData();
        BigInteger decryptedDataInput = decryptedData(inputtedData[0],inputtedData[1],inputtedData[2]);
        String decryptedInput = decryptedPhrase(decryptedDataInput);
        System.out.println("Your decrypted phrase is: " + decryptedInput);
    }
}//main

```
<!-- REFERENCES -->
## References
I learned about RSA Encryption through the University of Waterloo's slideshows. Links to the slideshows can be seen below
* [Slideshow](https://cs.uwaterloo.ca/~cbruni/videos/Math135JanApr2016/CCCWeek9Pt1RSA.pdf)
* [Worked Example](https://cs.uwaterloo.ca/~cbruni/videos/Math135SeptDec2015/Lesson19RSA.pdf)

<!-- CONTACT -->
## Contact

Your Name - [@momin_c](https://instagram.com/momin_c) - hellomomins@yahoo.com

Project Link: [https://github.com/Momin-C/RSA-Encryption](https://github.com/Momin-C/RSA-Encryption)
