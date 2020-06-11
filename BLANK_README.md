<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->

<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/Momin-C/CS-ISU">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">YOUR_TITLE</h3>

  <p align="center">
    YOUR_SHORT_DESCRIPTION
    <br />
    <a href="https://github.com/Momin-C/CS-ISU"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/Momin-C/CS-ISU">View Demo</a>
    ·
    <a href="https://github.com/Momin-C/CS-ISU/issues">CS-ISUrt Bug</a>
    ·
    <a href="https://github.com/Momin-C/CS-ISU/issues">Request Feature</a>
  </p>
</p>



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
* [Usage](#usage)
* [Roadmap](#roadmap)
  * [Packages](#packages)
  * [Class Methods](#class-methods)
  * [Main Method](#main-method)
* [Videos](#videos)
* [Contact](#contact)



<!-- ABOUT THE PROJECT -->
## About The Project

[![Product Name Screen Shot][product-screenshot]](https://example.com)

This project uses one of the most secure and common methods of encryption (RSA) to encrypt a given user input. It also asks the user if they want to decrypt a given input. The next sections explain how the encryption works.

<!-- USAGE -->
## Usage

To use this file and test its encryption simply clone the CS-ISU onto your computer and run it using an IDE or a compiler of your choice

```sh
git clone https://github.com/Momin-C/CS-ISU.git
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

<!-- MAIN METHOD -->
### Main Method

Main method goes here

<!-- VIDEOS  -->
## Videos

The program accepts any keyboard input that has an ASCII value, this means special characters, upper-case, lower-case and more. Videos can be seen below using different inputs with different cases and special characters.


<!-- CONTACT -->
## Contact

Your Name - [@momin_c](https://twitter.com/momin_c) - hellomomins@yahoo.com

Project Link: [https://github.com/Momin-C/CS-ISU](https://github.com/Momin-C/CS-ISU)


<!-- MARKDOWN LINKS & IMAGES -->
[product-screenshot]: images/screenshot.png
