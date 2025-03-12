# Computational Theory Assessment
## Sophie Boyle - G00410444
## Introduction

This repository contains solutions for the **Computational Theory** assessment. The goal of this project is to implement and analyze various computational functions, including bitwise operations, hash functions, and cryptographic techniques.

## 📚 **Table of Contents**  
1. [Project Structure](#project-structure)  
2. [Usage Instructions](#usage-instructions)  
3. [Tasks Overview](#tasks-overview)  
4. [Task 1: Binary Representations](#task-1-binary-representations)  
5. [Task 2: Hash Functions](#task-2-hash-functions)  
6. [Task 3: Cryptographic Functions](#task-3-cryptographic-functions)  
7. [Task 4: Prime Numbers](#task-4-prime-numbers)  
8. [Task 5: Roots](#task-5-roots)  
9. [Task 6: Proof of Work](#task-6-proof-of-work)  
10. [Task 7: Turing Machines](#task-7-turing-machines)  
11. [Task 8: Computational Complexity](#task-8-computational-complexity)  
12. [References](#references)  
13. [Conclusion](#conclusion)  

**Each task is structured as follows:**  
- **Overview**  
- **Research and Insights**  
- **Functions Implemented**
- **Comparison of Work**
- **Testing**  
- **References**  

---

## **Project Structure**

The repository is organized as follows:

- `tasks.ipynb`: Jupyter notebook containing solutions for all tasks and tests.
- `README.md`: This README file with an overview, research, and instructions.
- `.gitignore`: Specifies files and directories to ignore in Git.
- `requirements.txt`: Lists dependencies required to run the project.

## **Usage Instructions**
To run the code and tests, follow these steps:

### Clone the repository
   ```sh
   git clone <https://github.com/sophieboyle1/computational-theory>
   ```

### Navigate to the repository directory
   ```sh
   cd <https://github.com/sophieboyle1/computational-theory>
   ```

### Open the Jupyter notebook
   ```sh
   jupyter notebook tasks.ipynb
   ```
- This will launch the notebook where you can run individual cells.

### Run the notebook cells
- Execute the solutions directly within the Jupyter Notebook.

---

## Task 1: Binary Representations

### **Overview**
In Task 1, I implemented four key functions to manipulate bits in a 32-bit unsigned integer. Bitwise operations are powerful tools often used in fields like cryptography, data compression, and algorithm optimization. While they can be tricky at first, mastering them provides a deeper understanding of how computers handle binary data.

The goal was to create functions that simulate operations commonly seen in cryptographic algorithms like SHA-256—rotating bits, making conditional choices, and computing majority values at the bit level.

---

### **Research and Insights**  

Bitwise operations are fundamental in **low-level computing**, used in **cryptography, data compression, networking, and graphics**. Since Python does not enforce fixed-width integers like C, **bit masking (`& 0xFFFFFFFF`)** is required to correctly simulate **32-bit unsigned integers**.

For Task 1, I implemented four key functions—**bitwise rotation (`rotl`, `rotr`), conditional selection (`ch`), and majority voting (`maj`)**—all of which play crucial roles in **cryptographic security and data manipulation**.

---

### 🔐 **Bitwise Operations in Cryptography**  

The functions in Task 1 are widely used in cryptographic hash functions like **SHA-256**, where bitwise operations ensure **diffusion** (spreading input bits widely) and **non-linearity** (making output unpredictable).  

- **`rotl(x, n)`, `rotr(x, n)`** – Used in cryptographic rounds to efficiently mix bits.  
- **`ch(x, y, z)`** – Selects bits based on conditions, adding complexity to hashing functions.  
- **`maj(x, y, z)`** – Determines the majority bit at each position, ensuring unpredictable outputs.  

📖 **Further Reading:**  
- [FIPS PUB 180-4: Secure Hash Standard (NIST)](https://csrc.nist.gov/publications/detail/fips/180/4/final)  
- [Understanding Bitwise Operations in Cryptographic Algorithms](https://medium.com/%40conniezhou678/mastering-data-algorithm-part-30-mastering-bitwise-manipulation-in-python-81d03ff6f36d)  

---

### 🚀 **Real-World Applications Beyond Cryptography**  

Bitwise operations go far beyond cryptographic security and play a major role in:  

- **Data Compression** – Algorithms like **Huffman coding** use bitwise packing to reduce storage.  
- **Networking & Protocols** – TCP/IP headers store flags using bitwise masks for fast packet processing.  
- **Graphics & Image Processing** – Extracting RGB channels from a pixel value using bitwise masking:  
  ```python
  red = (pixel_value >> 16) & 0xFF  # Extracts the red component
---

### **Functions Implemented**

1. **`rotl(x, n)` - Rotate Left**  
   Rotates the bits of a 32-bit unsigned integer `x` to the left by `n` positions.  
   - Overflow bits wrap around to the rightmost positions.
   - Example: `rotl(0b0001, 2)` → `0b0100`.

2. **`rotr(x, n)` - Rotate Right**  
   Rotates the bits of a 32-bit unsigned integer `x` to the right by `n` positions.  
   - Overflow bits wrap around to the leftmost positions.
   - Example: `rotr(0b1000, 1)` → `0b0100`.

3. **`ch(x, y, z)` - Choose Function**  
   The function conditionally selects bits based on the value of `x`.  
   - Where `x` has `1`s, it chooses the corresponding bits from `y`.  
   - Where `x` has `0`s, it chooses the corresponding bits from `z`.
   - Example: `ch(0b1010, 0b1111, 0b0000)` → `0b1010`.

4. **`maj(x, y, z)` - Majority Function**  
   Determines the majority bit at each position among `x`, `y`, and `z`.  
   - If at least two of the inputs have `1`s at a given position, the output will have a `1`.
   - Example: `maj(0b1010, 0b1111, 0b0000)` → `0b1010`.

---

### Comparison of Work

Bitwise operations are crucial in cryptographic applications, especially in hashing functions like SHA-256. This table compares the implemented methods with alternative approaches and references similar work.

| **Approach**                   | **Description** | **Use in Cryptography** | **Limitations** |
|--------------------------------|----------------|--------------------------|-----------------|
| **Implemented: ROTL & ROTR (Bitwise Rotations)** | Circularly shifts bits left or right without losing data. | Used in SHA-256 and other cryptographic algorithms to ensure bit diffusion and security. | Slightly slower than direct shifts but ensures all bits are preserved. |
| **Implemented: CH (Choice Function)** | Selects bits from y where x has 1s, otherwise selects from z. | Ensures non-linearity in SHA-256, making outputs unpredictable. | Computationally heavier than simple bitwise AND/OR. |
| **Implemented: MAJ (Majority Function)** | Returns the majority bit from three inputs. | Used in SHA-256 to introduce randomness and improve hashing security. | Requires more bitwise operations than a direct comparison. |
| **Alternative: Bitwise Shift (<<, >>)** | Directly shifts bits left or right. | Faster for simple manipulations but not secure for cryptographic use. | Discards bits instead of rotating, leading to data loss. |
| **Alternative: Lookup Tables for Rotation** | Precomputed rotations stored in memory. | Optimized for hardware-based cryptographic applications. | Uses extra memory, making it impractical for constrained environments. |
| **Alternative: XOR-Based Manipulations** | Some CH/MAJ functions can be rewritten using XOR operations. | Can be optimized for specific architectures. | More instructions needed, increasing computational overhead. |

### References to Similar Work 
- **OpenSSL SHA-256 Implementation** – Uses bitwise operations for efficient cryptographic hashing.  
  [🔗 Link](https://github.com/openssl/openssl/blob/master/crypto/sha/sha256.c)  
- **Java Cryptography API (JCA)** – Implements similar bitwise logic in secure hashing functions.  
  [🔗 Link](https://docs.oracle.com/javase/8/docs/technotes/guides/security/crypto/CryptoSpec.html)  

---

### **Testing**
All functions have been **fully tested** in the **Jupyter Notebook (`tasks.ipynb`)** using Python’s built-in **unittest** module.  

### Test Coverage

| **Category**            | **Description** | **Result** |
|-------------------------|----------------|-----------|
| ✅ **Standard cases**    | Checking expected outputs for bitwise rotations (`rotl`, `rotr`), conditional selection (`ch`), and majority logic (`maj`). | ✅ Passed |
| ✅ **Edge cases**        | Rotations by **0** and **32 positions**, alternating bit patterns, and large values. | ✅ Passed |
| ✅ **Error handling**    | Ensuring negative values and out-of-range numbers are handled correctly. | ✅ Passed |
| ✅ **Bitwise correctness** | Verified results using **manual bitwise calculations**. | ✅ Passed |



### Running the Tests
- All tests are included in **`tasks.ipynb`** – simply run all cells.
- No external setup is required.  

*(For a more detailed breakdown of test cases, see the notebook.)*

### **References**

| **Function** | **Reference** | **Why It Was Used** |
|--------------|---------------|----------------------|
| `rotl`       | [Python Docs - Bitwise Operators](https://docs.python.org/3/library/stdtypes.html#bitwise-operations) | To understand shifting behavior and syntax. |
|              | [Stack Overflow - Bit Manipulation](https://stackoverflow.com/questions/2632520/why-doesnt-bitwise-or-in-python-return-what-i-expect) | To handle 32-bit masking. |
| `rotr`       | [Python Docs - Bitwise Operators](https://docs.python.org/3/library/stdtypes.html#bitwise-operations) | To understand right shift behavior. |
|              | [Wikipedia - Circular Shift](https://en.wikipedia.org/wiki/Circular_shift) | To handle bit wrap-around correctly. |
| `ch`         | [FIPS PUB 180-4](https://csrc.nist.gov/publications/detail/fips/180/4/final) | To get the formula for the `ch` function. |
|              | [Python Docs - Bitwise AND/OR](https://docs.python.org/3/library/stdtypes.html#bitwise-and) | To correctly implement bitwise logic in Python. |
| `maj`        | [FIPS PUB 180-4](https://csrc.nist.gov/publications/detail/fips/180/4/final) | To get the formula for the `maj` function. |
|              | [Python Docs - Bitwise AND/OR](https://docs.python.org/3/library/stdtypes.html#bitwise-and) | To understand bitwise AND/OR operations in Python. |


## Task 2: Hash Functions

### **Overview**

This task explores **hash functions**, which are essential for cryptography, data integrity, and efficient data structures like hash tables.  

The main objectives of this task are:  

- Convert a given C hash function into Python while maintaining efficiency and correctness.  
- Test the Python implementation with various inputs to ensure deterministic hashing.  
- Analyze why 31 and 101 were chosen in the function.  

### What is a Hash Function?  
A hash function takes an input (e.g., a string) and converts it into a fixed-size integer. An ideal hash function should be:  

- Efficient → Quickly compute a **unique hash** for an input.  
- Deterministic → The same input **always produces** the same hash value.  
- Uniform → Hash values should be **well-distributed** to minimize collisions.  

### Why is Hashing Important?  
Hashing plays a crucial role in various applications, including:  

- Cryptography → Hashing secures passwords, digital signatures, and cryptographic protocols.  
- Data Integrity → Hash functions verify that data has not been altered (e.g., file checksums).  
- Efficient Lookups → Hash tables provide fast access to stored data (used in Python dictionaries). 

---

## Research and Insights 🔬  

### Understanding Hash Functions  
Hash functions are essential in computing, used for **data integrity, cryptography, and efficient data storage**. A hash function takes an input (e.g., a string) and converts it into a **fixed-length** integer, making it useful for fast lookups and detecting data modifications.  

Common applications of hashing:  
- **Data Integrity** → Ensures that files and messages have not been altered.  
- **Efficient Lookups** → Used in hash tables to enable quick data retrieval.  
- **Cryptographic Security** → Protects sensitive information like passwords by making data irreversible.  

### Translating the C Function to Python  
The original C function computes a hash using a **weighted sum** and a **modulo operation**. When converting it to Python, several adaptations were needed:  
- **Removing Pointers** → Python strings are immutable, so we use a `for` loop instead of `char *s`.  
- **Using ASCII Values** → The `ord()` function retrieves character ASCII values, replacing `*s`.  
- **Maintaining Consistency** → The modulo 101 operation is kept to **limit hash values** to a fixed range.  

### Why Hashing Matters in Performance  
Hashing ensures **efficient storage and retrieval** by minimizing **collisions** (when different inputs produce the same hash). A well-designed hash function:  
- **Distributes values evenly** → Prevents clustering, which can slow down lookups.  
- **Uses prime numbers** → Numbers like `31` and `101` reduce predictable cycles in hashing, improving performance.  

### Real-World Applications of Hashing  
- **Databases** → Indexing to speed up data searches.  
- **Cryptography** → Secure password storage and digital signatures.  
- **File Verification** → Checking for data corruption using hash checksums.  

📖 **Further Reading:**  
- [Python Docs - Hash Functions](https://docs.python.org/3/library/hashlib.html) 
- [Lecture 4: Hashing from MIT's Introduction to Algorithms course](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/resources/lecture-4-hashing/)

---

### Testing

| **Category**              | **Description** | **Result** |
|---------------------------|----------------|-----------|
| ✅ **Basic Cases**        | Ensures that hashing common words like `"hello"`, `"world"`, and `"python"` produces expected values. | ✅ Passed |
| ✅ **Edge Cases**         | Tests include hashing an **empty string**, **single-character strings**, and **long strings** to check function stability. | ✅ Passed |
| ✅ **Collision Handling** | Verifies that different words (e.g., `"apple"` and `"orange"`) do not produce the same hash value, reducing the likelihood of collisions. | ✅ Passed |
| ✅ **Consistency Check**  | Runs the hash function multiple times on the same input to ensure it consistently produces the same output. | ✅ Passed |


---

### **Running the Tests**  
- All tests are included in **`tasks.ipynb`** – simply run all cells.  
- No external setup is required.  

*(For a more detailed breakdown of test cases, see the notebook.)*

---

### **References**

| **Function** | **Reference** | **Why It Was Used** |
|--------------|---------------|----------------------|
| `hash_function` | [Oracle Docs - Effective Java (Item 11: HashCode)](https://docs.oracle.com/en/java/) | To understand why prime numbers like 31 are commonly used in hashing. |
|              | [Python Docs - Hashing](https://docs.python.org/3/library/hashlib.html) | To understand Python’s built-in hashing functions and techniques. |
|              | [MIT OpenCourseWare - Hash Functions](https://openlearninglibrary.mit.edu/) | To explore the theoretical background of hash functions and their applications. |
|              | [Princeton - Hashing Functions](https://algs4.cs.princeton.edu/34hash/) | To understand uniform distribution and how prime moduli improve hash distribution. |
|              | [Python Docs - Modulo Operator](https://docs.python.org/3/reference/expressions.html#binary-arithmetic-operations) | To understand how Python’s modulo operation ensures hash values remain within range. |

---

## Task 3: SHA256

### Overview

SHA-256 is a widely used cryptographic hash function that provides data integrity and security. A key step in the hashing process is message padding, which ensures that the input data conforms to the SHA-256 block size of 512 bits before being processed.

The padding process follows a structured format:

- Append a single 1 bit (0x80 in hex) to the message.
- Add zero bits until the message length is 64 bits short of a multiple of 512.
- Append the original message length as a 64-bit big-endian integer.

Padding is required to maintain the security properties of SHA-256. It ensures that messages fit neatly into 512-bit blocks, preventing ambiguities and vulnerabilities. Without this step, the hash function would not be able to process inputs of varying lengths securely.

The method follows the exact structure described in the NIST SHA-2 specification, ensuring compliance with cryptographic standards.

---

### Research and Insights 🔬

SHA-256 is part of the SHA-2 family of cryptographic hash functions and is widely used for securing data, verifying integrity, and digital signatures. Before the hashing process, messages need to be **padded** to fit into 512-bit blocks.  

Padding is crucial because SHA-256 processes data in fixed-size blocks. If a message is shorter than a full block, padding ensures that the structure is maintained without ambiguity. This follows the Merkle–Damgård construction, which allows for secure hash functions to operate on variable-length inputs.  

#### Why is Padding Necessary?
1. **Ensures Message Length is a Multiple of 512 Bits**  
   - The SHA-256 compression function processes data in **512-bit chunks**.  
   - If a message is too short, it needs to be extended while preserving uniqueness.  

2. **Prevents Collision & Length Extension Attacks**  
   - Without proper padding, attackers could manipulate hashes by appending additional data.  
   - Adding a length field at the end makes it difficult to extend an existing hash.  

3. **Follows the SHA-2 Specification**  
   - Padding must conform to the exact structure outlined in **FIPS PUB 180-4**.  
   - This ensures **compatibility** with cryptographic implementations.  

📖 **Further Reading:** 
- [NIST FIPS PUB 180-4 – Secure Hash Standard](https://csrc.nist.gov/publications/detail/fips/180/4/final)
- [Cryptographic Hashing and Padding Explained](https://crypto.stackexchange.com/questions/39680/why-do-hash-functions-need-padding)
- [SHA-256 Padding – A Technical Breakdown](https://en.wikipedia.org/wiki/SHA-2#Padding)

---

### Functions Implemented

To correctly apply SHA-256 padding, several functions were implemented, each handling a specific step of the process.

1. **Reading the file contents**  
   The function reads the input file as raw bytes to ensure all data is processed correctly.

2. **Computing the original bit length**  
   The function calculates the length of the input in bits, which is later appended to the message as part of the padding process.

3. **Appending the 1 bit**  
   SHA-256 requires the input to end with a single 1 bit (0x80 in hex) to clearly mark the message boundary.

4. **Adding zero padding**  
   After the 1 bit is added, zeros are appended to align the message to 448 bits modulo 512.

5. **Appending the original message length**  
   The final step is appending the original message length as a 64-bit big-endian integer to the end of the padded message.

6. **Extracting the padding**  
   This function isolates and extracts only the padding bytes, converting them into a human-readable hexadecimal format.

Each function ensures compliance with the NIST SHA-2 specification, allowing the input to be securely processed by the SHA-256 hash function.

---

### Testing

The padding implementation was thoroughly tested to ensure correctness and adherence to the SHA-256 specification. The following test cases were used:


| **Category**               | **Description** | **Result** |
|----------------------------|----------------|-----------|
| ✅ **Reading file contents** | Ensured that the file was read accurately as raw bytes. | ✅ Passed |
| ✅ **Computing bit length**  | Confirmed that the original length in bits matched expectations for various input sizes. | ✅ Passed |
| ✅ **Appending the 1 bit**   | Verified that a single 1 bit (0x80 in hex) was appended correctly. | ✅ Passed |
| ✅ **Zero padding length**   | Checked that the padding brought the total length to 448 bits mod 512. | ✅ Passed |
| ✅ **Appending original length** | Confirmed that the final padded message included the original bit length in the correct format. | ✅ Passed |
| ✅ **Extracting padding**    | Ensured that the extracted padding matched the expected hex representation. | ✅ Passed |


### **Running the Tests**  
- All tests are included in **`tasks.ipynb`** – simply run all cells.  
- No external setup is required.  

*(For a more detailed breakdown of test cases, see the notebook.)*

---

### References

| **Function**              | **Reference**                                                                                  | **Why It Was Used**                                                        |
|----------------------------|-----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| `read_file`               | [Python Docs - File Input and Output](https://docs.python.org/3/tutorial/inputoutput.html)     | To understand how to read binary data from a file in Python.              |
| `compute_original_bit_length` | [Python Docs - len() function](https://docs.python.org/3/library/functions.html#len)       | To calculate the length of the data in bytes.                             |
| `append_one_bit`          | [NIST - SHA-256 Specification](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)     | To follow the exact steps for padding a message according to SHA-256.     |
| `add_zero_padding`        | [NIST - SHA-256 Specification](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)     | To ensure that the message length is correct before hashing.              |
| `append_original_length`  | [Python Docs - int.to_bytes()](https://docs.python.org/3/library/stdtypes.html#int.to_bytes)   | To convert an integer into a 64-bit big-endian format for SHA-256 padding.|
| `extract_padding`         | [Python Docs - String Formatting](https://docs.python.org/3/library/string.html#format-specification-mini-language) | To format the padding bytes as a readable hexadecimal string.            |

---

## Task 4: Prime Numbers

### Overview
Prime numbers play a fundamental role in number theory and cryptography. They are the building blocks of all integers, as described in the **Fundamental Theorem of Arithmetic**, which states that every integer greater than 1 can be uniquely represented as a product of prime numbers.

This task involves calculating the first **100 prime numbers** using two well-established and efficient algorithms:

1. **Trial Division Algorithm** – A simple but computationally expensive method for checking the primality of a number.
2. **Sieve of Eratosthenes** – An optimized algorithm for efficiently generating prime numbers in bulk.

Each algorithm has different use cases:
- **Trial Division** is useful when checking the primality of individual numbers, especially in cryptographic applications.
- **Sieve of Eratosthenes** is highly efficient for generating large lists of primes, making it a preferred choice for number theory and computational applications.

### Implementation Goals
✔️ Implement two algorithms for prime number generation.  
✔️ Optimize computations where possible (e.g., skipping even numbers, reducing unnecessary checks).  
✔️ Compare and analyze the efficiency of both approaches.  

### Justification for Selection
These two algorithms are widely used in computational mathematics and cryptography:
- The **Trial Division** method is a fundamental approach that is often used in cryptographic key validation.
- The **Sieve of Eratosthenes** is an essential technique for quickly generating prime numbers, which are crucial in applications such as **RSA encryption** and **hashing functions**.

## Research and Insights

Prime numbers play a fundamental role in mathematics, particularly in **number theory, cryptography, and computer science**. Their unique properties make them essential for secure communications, data encryption, and computational algorithms.

---

### Why Are Prime Numbers Important?
Prime numbers are the **building blocks** of integers, as stated in the **Fundamental Theorem of Arithmetic**:

> *Every integer greater than 1 can be uniquely expressed as a product of prime numbers.*

This property makes prime numbers essential in factorization-based cryptography(e.g., RSA encryption). Their unpredictable distribution also provides security advantages in cryptographic algorithms.

---

### Prime Numbers in Cryptography
Cryptographic security often relies on the difficulty of **factoring large prime numbers**. Modern encryption techniques, such as RSA and Diffie-Hellman key exchange, are built upon **the infeasibility of factorizing the product of two large primes**.

#### **Public Key Cryptography (RSA)**
- RSA encryption uses the product of two large primes (**p** and **q**) as part of its key generation.
- The security of RSA depends on the difficulty of **prime factorization**—a problem that classical computers cannot efficiently solve for large numbers.
- Example: A 2048-bit RSA key consists of two 1024-bit prime numbers.

#### **Elliptic Curve Cryptography (ECC)**
- ECC uses properties of prime numbers in modular arithmetic on elliptic curves.
- Provides the same level of security as RSA with **smaller key sizes**, making it efficient for **mobile and IoT security**.

#### **Primality Testing in Cryptography**
Before using a number in cryptography, it must be verified as prime.  
Common tests include:
- **Miller-Rabin Test** (Probabilistic)
- **AKS Primality Test** (Deterministic)
- **Fermat’s Little Theorem** (Basic)

---

### Prime Number Algorithms: Trial Division vs. Sieve of Eratosthenes
Finding prime numbers efficiently is a major challenge in computational mathematics.  
Two well-known approaches are **Trial Division** and the **Sieve of Eratosthenes**.

#### 1.**Trial Division Algorithm**
The **Trial Division method** determines if a number **n** is prime by checking divisibility from **2 up to** \( \sqrt{n} \).

##### **Steps:**
1. If \( n \) is **2 or 3**, return **True** (smallest primes).
2. If \( n \) is even or divisible by 3, return **False**.
3. Loop through odd numbers from **5** to **√n**, checking divisibility.

##### ✅ **Advantages:**
- Simple to understand and implement.
- Good for small numbers.

##### ❌ **Disadvantages:**
- **Slow for large numbers** (Time complexity: \( O(\sqrt{n}) \)).
- **Inefficient** when generating many primes.

---

#### **Sieve of Eratosthenes**
The **Sieve of Eratosthenes** is an efficient way to find all prime numbers up to a given limit **N**.

#### **Steps:**
1. Create a boolean list of **N + 1** elements, all initially **True**.
2. Mark **multiples of each prime** as **False** (starting from 2).
3. Continue marking until reaching \( \sqrt{N} \).
4. The remaining **True** indices correspond to **prime numbers**.

##### ✅ **Advantages:**
- Extremely fast for finding **many** primes.
- **Time complexity:** \( O(n \log \log n) \), much faster than Trial Division.

##### ❌ **Disadvantages:**
- Uses more **memory** than Trial Division.
- **Inefficient for checking a single prime number**.

---

### Comparing the Two Algorithms

| **Feature**            | **Trial Division**        | **Sieve of Eratosthenes**  |
|------------------------|-------------------------|---------------------------|
| **Best Use Case**      | Checking **one number** for primality | Generating **many** primes efficiently |
| **Time Complexity**    | \( O(\sqrt{n}) \)       | \( O(n \log \log n) \) |
| **Space Complexity**   | \( O(1) \) (constant)   | \( O(n) \) (array storage) |
| **Efficiency**         | Slow for large \( n \)  | Very fast for large \( n \) |
| **Practical Use**      | Cryptographic validation (RSA keys) | Number theory, bulk prime generation |

---

### **Which One Should You Use?**
- **Use Trial Division** when verifying if one number is prime (e.g., cryptography).
- **Use Sieve of Eratosthenes** when generating many primes efficiently.

---

### Further Reading
- [🔗 NIST Primality Testing Guidelines](https://csrc.nist.gov)
- [🔗 RSA Cryptography Explained](https://en.wikipedia.org/wiki/RSA_(cryptosystem))
- [🔗 Efficient Prime Finding (MIT OpenCourseWare)](https://ocw.mit.edu)

---

## Functions Implemented

### How It Works
The **Trial Division Algorithm** is a straightforward approach to checking if a number is prime:
1. If \( n \leq 1 \), return **False** (since 1 is not prime).
2. Check divisibility by **2**:
   - If \( n \) is even and greater than 2, return **False**.
3. Check odd divisors from **3** to \( \sqrt{n} \):
   - If \( n \) is divisible by any number in this range, return **False**.
4. If no divisors are found, return **True** (the number is prime).

### Optimizations
- **Even number elimination** – After checking 2, only odd numbers are tested.
- **Square root limit** – Reduces unnecessary checks by only testing up to \( \sqrt{n} \).
- **Early exit condition** – As soon as a divisor is found, the function stops execution.

### Use Cases
- **Cryptographic Key Validation** – Checking if a given number is prime.
- **Mathematical Computations** – Used in number theory for factorization problems.

### Example Usage
```python
is_prime_trial(29)  # Returns True (29 is prime)
is_prime_trial(30)  # Returns False (30 is not prime)
```

### Performance

| **Input Size \( n \)**  | **Time Complexity** |
|----------------------|----------------|
| Small values (e.g., 2-100)  | \( O(\sqrt{n}) \) – Fast |
| Large values (e.g., cryptographic primes)  | \( O(\sqrt{n}) \) – Inefficient |

The **Trial Division Algorithm** is effective for checking individual primes but not efficient for generating large lists of primes. To solve this, we use the Sieve of Eratosthenes, covered in the next section.

## Sieve of Eratosthenes

The **Sieve of Eratosthenes** is a highly efficient algorithm used to find **all prime numbers up to a given limit**. It eliminates non-prime numbers by iteratively marking the multiples of each prime starting from **2**.

### Key Functions

- **`sieve_of_eratosthenes(limit)`** – Generates a list of prime numbers **up to** a given limit.
- **`first_n_primes_sieve(n)`** – Extracts the **first `n` prime numbers** from the computed sieve.

---

### `sieve_of_eratosthenes(limit)`

This function initializes a **boolean list** where each index represents a number. Initially, all numbers are assumed to be **prime** (`True`), except for **0 and 1**, which are set to `False`. 

The algorithm:
1. Iterates from **2** to \( \sqrt{n} \).
2. If the current number is **still prime**, it marks all its multiples as **non-prime**.
3. The remaining numbers marked as `True` are the **prime numbers**.

**Optimized to run in \( O(n \log \log n) \) time complexity**, making it significantly faster than **Trial Division**.

---

### `first_n_primes_sieve(n)`

This function extracts **the first `n` prime numbers** from the sieve.

It:
1. Calls `sieve_of_eratosthenes(limit)` with a sufficiently large limit.
2. Extracts indices of all numbers that remain **marked as prime**.
3. Returns **only the first `n` primes**.

**Efficient for generating large prime sets in bulk.**

---

### Performance Comparison

| Feature                | Sieve of Eratosthenes |
|------------------------|----------------------|
| **Best Use Case**      | Generating large sets of primes |
| **Time Complexity**    | \( O(n \log \log n) \) |
| **Space Complexity**   | \( O(n) \) |
| **Speed**              | Very fast for large \( n \) |
| **Use in Cryptography**| Bulk prime number generation |

---

### Summary
The **Sieve of Eratosthenes** is an essential algorithm in computational mathematics and cryptography. It significantly outperforms Trial Division for generating multiple primes but requires more memory due to its array-based implementation.

## Comparison of Work

The **Trial Division** and **Sieve of Eratosthenes** algorithms serve different purposes in prime number computation. The table below compares their efficiency, best use cases, and trade-offs.

---

### Algorithm Comparison

| Feature                 | Trial Division               | Sieve of Eratosthenes       |
|-------------------------|----------------------------|----------------------------|
| **Best Use Case**       | Checking if a single number is prime | Finding multiple prime numbers efficiently |
| **Time Complexity**     | \( O(n) \) per number       | \( O(n \log \log n) \)       |
| **Space Complexity**    | \( O(1) \) (minimal memory usage) | \( O(n) \) (stores prime markers) |
| **Speed**               | Slow for large \( n \)      | Very fast for large \( n \) |
| **Use in Cryptography** | Key validation, primality tests | Bulk prime generation for cryptographic applications |
| **Scalability**         | Poor for large numbers      | Scales efficiently with larger inputs |
| **Implementation Complexity** | Simple, easy to implement | Requires memory allocation but highly optimized |

---

**Final Verdict:**  
For large-scale applications, **Sieve of Eratosthenes** is far superior in performance, whereas **Trial Division** remains useful for single-number primality tests.

---

## Testing

To validate the correctness and efficiency of both **Trial Division** and **Sieve of Eratosthenes**, a comprehensive set of test cases was executed. These tests ensure accuracy, efficiency, and robustness under various conditions.

### Test Coverage

| **Category**             | **Description**                                              | **Result**  |
|-------------------------|--------------------------------------------------------------|------------|
| **Basic Prime Checks**  | Verified prime detection for small known primes (e.g., 2, 3, 5, 7, 11)  | ✅ Passed  |
| **Edge Cases**          | Tested limits like \( n = 1 \), even numbers, and prime boundaries | ✅ Passed  |
| **Efficiency Testing**  | Measured execution time for generating the first **100** primes  | ✅ Passed  |
| **Large Input Handling** | Ensured algorithms work efficiently for numbers up to **10⁶** | ✅ Passed  |
| **Consistency Check**   | Repeated runs produce identical results, confirming determinism | ✅ Passed  |

---

### Key Observations

- **Trial Division** was accurate but slow for large numbers.
- **Sieve of Eratosthenes** was significantly faster for generating large prime lists.
- Both algorithms correctly identified all primes, confirming their correctness.
- Performance tests showed that the Sieve scales better as \( n \) increases.

**Conclusion:**  
While both methods are correct, the **Sieve of Eratosthenes** is far more efficient when computing large prime sets.

### Running the Tests

All tests are included in `tasks.ipynb`.  
To run them, simply **execute all cells** in the Jupyter Notebook.

---

## References

To ensure correctness, efficiency, and best practices, the following references were used in the implementation and analysis of prime number generation.

| **Concept / Function**            | **Reference**                                    | **Why It Was Used** |
|-----------------------------------|------------------------------------------------|----------------------|
| **Trial Division Algorithm**      | MIT OpenCourseWare - Number Theory            | To understand basic prime checking methods. |
| **Mathematical Primality Tests**  | Princeton - Algorithm Design Manual           | To compare different prime-checking techniques. |
| **Sieve of Eratosthenes**         | Harvard Computational Number Theory Research  | To implement an optimized prime generation method. |
| **Cryptographic Prime Numbers**   | NIST - Cryptographic Standards                | To understand prime number use in encryption. |
| **Efficiency Analysis**           | Stanford Algorithms - Complexity Analysis     | To compare time complexity of different approaches. |

---


## Task 5: Roots

### Overview  
In cryptographic applications like **SHA-256**, certain constants are derived from prime numbers by extracting the **first 32 bits of the fractional part** of their **square roots**. These values help ensure **uniform distribution** and **high entropy**, making them suitable for cryptographic security.  

To compute these values, the process involves:  
- Generating the first 100 prime numbers using the **Sieve of Eratosthenes**.  
- Calculating the square root of each prime.  
- Extracting the **fractional part** of the square root.  
- Scaling this value to **32 bits** using \(2^{32}\).  
- Converting the result into a **hexadecimal representation**.  

This approach provides cryptographic constants that are **non-repeating** and **well-distributed**, making them ideal for secure hashing algorithms.  

---

### Research and Insights  

Prime numbers play a fundamental role in cryptography and computational number theory. The approach of extracting the **first 32 bits of the fractional part** of square roots is specifically used in cryptographic hash functions like **SHA-256**, where these constants help strengthen security.  

#### Why Prime Numbers?  
Prime numbers have unique mathematical properties that make them suitable for cryptographic applications:  
- **Unpredictability** – Their distribution is irregular, reducing patterns in cryptographic algorithms.  
- **Factorization Difficulty** – Many security protocols (e.g., RSA encryption) rely on the difficulty of factoring large primes.  
- **Uniformity** – Prime-derived constants ensure that hash functions avoid predictable biases.  

#### 🔢 The Mathematical Formula  
The process follows the formula:

$$
\text{frac}(p) = p - \lfloor p \rfloor
$$

$$
\text{frac32} = \lfloor \text{frac}(p) \times 2^{32} \rfloor
$$

This computation extracts a **32-bit unsigned integer** from the fractional part of the square root of a prime number, ensuring high entropy and non-repeating constants.  

#### Cryptographic Relevance  
In **SHA-256**, the first 8 computed values directly correspond to the **initial hash values** used in the algorithm:  

| Prime | Approx. √p | Fractional Part | First 32 Bits (Hex) |
|-------|------------|----------------|----------------------|
| 2     | 1.414213  | 0.414213       | `0x6a09e667`        |
| 3     | 1.732051  | 0.732051       | `0xbb67ae85`        |
| 5     | 2.236068  | 0.236068       | `0x3c6ef372`        |
| 7     | 2.645751  | 0.645751       | `0xa54ff53a`        |
| 11    | 3.316625  | 0.316625       | `0x510e527f`        |
| 13    | 3.605551  | 0.605551       | `0x9b05688c`        |
| 17    | 4.123106  | 0.123106       | `0x1f83d9ab`        |
| 19    | 4.358899  | 0.358899       | `0x5be0cd19`        |

These values serve as initial hash constants in SHA-256, reinforcing the importance of prime-derived numbers in cryptographic security.

---

## Functions Implemented

For this task, two primary functions were implemented:

1. **Prime Number Generation** – Using the **Sieve of Eratosthenes** to efficiently find the first 100 prime numbers.  
2. **Fractional Part Extraction** – Computing the first 32 bits of the **fractional part** of the square root of each prime number.

---

### 1. Generating Prime Numbers with Sieve of Eratosthenes  
The Sieve of Eratosthenes is an optimized algorithm that marks non-prime numbers by eliminating multiples of each prime.

#### **Steps:**
- Initialize a boolean list where all numbers are assumed to be prime.
- Mark multiples of each prime starting from `2` as non-prime.
- Continue the process up to `√n`, marking non-primes.
- Extract the first 100 prime numbers.

**Code Snippet:**  
```python
primes = sieve_of_eratosthenes(600)[:100]  # Get first 100 prime numbers
```

### 2. Extracting 32-Bit Fractional Part

Once prime numbers are generated, I computed the **first 32 bits** of the **fractional part** of their **square roots**.

#### **Steps:**
1. Compute the **square root** of each prime.
2. Extract the **fractional part** by subtracting the integer part.
3. Multiply by **2³²** to scale the fraction.
4. Convert to an **integer** to extract the first **32 bits**.

#### **Code Snippet:**
```python
frac_part = math.sqrt(n) - math.floor(math.sqrt(n))
frac32 = int(frac_part * 2**32)  # Extract first 32 bits
```

### 3. Computing & Displaying Results

After computing the **32-bit fractional values**, the results are stored in a dictionary and displayed in a structured format.

#### **Code Snippet:**
```python
results = {p: hex(first_32_frac_bits(p)) for p in primes}
```

### 📊 Results Table

To present the results clearly, a **table format** is used:

| Prime | Fractional Part (Hex) |
|-------|----------------------|
| 2     | 0x6a09e667          |
| 3     | 0xbb67ae85          |
| 5     | 0x3c6ef372          |
| 7     | 0xa54ff53a          |
| 11    | 0x510e527f          |
| 13    | 0x9b05688c          |
| 17    | 0x1f83d9ab          |
| 19    | 0x5be0cd19          |

---

## Comparison of Work

The approach for Task 5 involves extracting the first 32 bits of the fractional part of the square roots of the first 100 prime numbers. This method is chosen because it provides constants that are:

- **Well-distributed** and **non-repeating**, essential for cryptographic security.
- **Mathematically derived** from prime numbers, ensuring reproducibility and robustness.

Below is a comparison between this method and alternative approaches:

| **Approach**                         | **Description**                                                                                         | **Use in Cryptography**            | **Efficiency**                       | **Limitations**                                            |
|--------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------|--------------------------------------|-----------------------------------------------------------|
| **Square Root Fractional Extraction** | Compute `sqrt(p)`, extract its fractional part, scale by \(2^{32}\), and convert to a 32-bit integer.    | Used for SHA-256 initial hash values. | Efficient for fixed-size inputs (100 primes). | Depends on floating-point precision.                    |
| **Cube Root Fractional Extraction**   | Apply the same process to the cube roots of primes.                                                     | Used in some hash function variants.   | Comparable in efficiency.            | Yields different constants; not standard for SHA-256.     |
| **Random Constant Generation**        | Generate constants using pseudo-random numbers.                                                       | Occasionally used, but less secure. | Very fast.                           | Lacks a mathematical basis and may introduce bias.      |

**Conclusion:**  
The **square root fractional extraction** method is preferred due to its strong **mathematical foundation** and its proven use in generating the **SHA-256 initialization constants**. This method balances efficiency with security, making it an ideal choice for cryptographic applications.

---

## Testing

To ensure the correctness and reliability of the **fractional extraction method**, a comprehensive set of test cases was conducted. These tests validate the accuracy of the computed **first 32-bit fractional parts** of square roots, ensuring alignment with **SHA-256 constants**.

---

### Test Coverage  

| **Category**               | **Description**                                                      | **Result**  |
|----------------------------|----------------------------------------------------------------------|------------|
| **Basic Fraction Checks**   | Verified correct fractional extraction for small primes (e.g., 2, 3, 5, 7) | ✅ Passed  |
| **Edge Cases**             | Tested with **1**, non-primes, and floating-point precision issues | ✅ Passed  |
| **Scaling Precision**      | Ensured values are scaled **correctly** to 32-bit representation | ✅ Passed  |
| **Comparison with SHA-256 Constants** | Verified that extracted values match the **SHA-256 initial hash constants** | ✅ Passed  |
| **Consistency Check**      | Repeated calculations yield the **same** results across multiple runs | ✅ Passed  |

---

### Key Observations  

- The **fractional extraction method** accurately isolates and scales the correct bits.  
- Values computed **match the known SHA-256 constants** for the first few primes.  
- **Precision is maintained** across all tested primes, with no rounding or floating-point errors.  
- The approach is **efficient** and executes quickly for 100+ prime numbers.  

**Conclusion:**  
The **32-bit fractional extraction method** successfully computes cryptographic constants **accurately** and **consistently**. These results align with SHA-256's initialization values, reinforcing its correctness.

### Running the Tests  

- All test cases are included in `tasks.ipynb` – simply run all cells
- No external setup is required. 

*(For a more detailed breakdown of test cases, see the notebook.)*

---

## References

This section provides references to relevant materials that support the concepts, algorithms, and methods used in **Task 5: Roots**.

| **Reference** | **Description** | **Why It Was Used?** |
|--------------|----------------|----------------------|
| [NIST FIPS PUB 180-4](https://csrc.nist.gov/publications/detail/fips/180/4/final) | Secure Hash Standard (SHA-256) | Describes how SHA-256 constants are derived from prime numbers. |
| [Cryptographic Hashing Explained](https://en.wikipedia.org/wiki/Cryptographic_hash_function) | Overview of cryptographic hash functions | Provides background on hash initialization constants and their significance. |
| [Python Math Module](https://docs.python.org/3/library/math.html) | Python's `math` module documentation | Used for computing **square roots** and extracting fractional parts. |
| [Sieve of Eratosthenes - Princeton Algorithms](https://algs4.cs.princeton.edu/15uf/) | Efficient prime number generation | Used to generate the **first 100 primes** efficiently. |
| [SHA-256 Initial Constants](https://en.bitcoin.it/wiki/SHA-256) | Bitcoin Wiki explanation of SHA-256 constants | Validates computed values against SHA-256 predefined constants. |
| [Floating Point Precision - IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) | IEEE 754 floating-point standard | Ensures correct handling of fractional calculations and precision. |

---

### Key Takeaways  

- **SHA-256 constants** originate from the **fractional part of prime square roots** as per **NIST FIPS PUB 180-4**.  
- The **Sieve of Eratosthenes** efficiently generates prime numbers, as supported by **Princeton's Algorithm Guide**.  
- **Python's `math` module** enables accurate computation of **square roots** and **fractional extraction**.  
- **IEEE 754 floating-point standard** ensures precision when scaling and extracting 32-bit values.  

By utilizing these references, the implementation aligns with **industry standards** and **best practices** in cryptographic computations.  

---

## Task 6: Proof of Work

### Overview

In cryptographic applications like **SHA-256**, hash functions produce **fixed-length outputs** that appear random. However, a unique property of hash outputs is the occurrence of **leading zero bits**, which is a key factor in **Proof-of-Work** systems used in **blockchain mining**.

To explore this phenomenon, this task involves:

- Retrieving a dataset of **English words**.
- Computing the **SHA-256 hash** of each word.
- Converting the hash to its **binary representation**.
- Counting the number of **leading zero bits**.
- Identifying words with the **highest number of leading zeros**.

Since SHA-256 is a **cryptographic hash function**, the number of leading zeroes in any given hash is **probabilistic** and depends entirely on the properties of the input word. Words that naturally align with this structure may exhibit more leading zeroes, though this is not deterministic.

This approach demonstrates **pre-image resistance**—a fundamental principle of cryptographic security—while also simulating aspects of **Proof-of-Work mining**, where computational effort is required to discover valid hashes.

---

## Research & Insights

### Hashing & Leading Zeroes  
SHA-256, a **cryptographic hash function** standardized by **NIST** [(NIST, 2015)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf), generates **fixed-length (256-bit) hashes** that exhibit random-like behavior. Due to this randomness, some hashes naturally begin with a sequence of **leading zero bits**—a property exploited in **Proof-of-Work mining** (e.g., Bitcoin).

- **Probability & Distribution:**  
  Since SHA-256 is designed to be **uniformly distributed**, the likelihood of a hash starting with `n` leading zeros follows an exponential probability of **\( 2^{-n} \)** [(IACR, 2010)](https://eprint.iacr.org/2010/548.pdf).
  
- **Significance in Cryptography:**  
  - **Pre-image resistance** ensures that predicting or manipulating input words to produce leading zeroes is infeasible [(Shoup, 2009)](https://shoup.net/ntb/).
  - **Hash uniqueness** means that minor input changes drastically alter the hash output (avalanche effect).

### Proof-of-Work Relevance  
In blockchain systems, miners compete to **find a nonce** that results in a hash with a specified number of **leading zeroes**. This process:  
- **Regulates mining difficulty** dynamically.  
- **Prevents network spam** by enforcing computational costs.  
- **Ensures consensus** in decentralized networks.  

While this task does **not involve nonce-based mining**, it **mirrors** the concept by searching for **English words** that naturally exhibit more leading zeroes in their SHA-256 hash.

📌 **Reference:** Nakamoto, S. (2008). *Bitcoin: A Peer-to-Peer Electronic Cash System.* [Bitcoin Whitepaper](https://bitcoin.org/bitcoin.pdf).

### Observations from Word Analysis  
- Some **longer words** exhibited **more leading zeroes**, but this was **not a strict pattern**.  
- The **character composition** (e.g., frequency of vowels/consonants) seemed to influence outcomes in unpredictable ways.  
- **Dictionary-based filtering** ensured that only valid words were considered, reinforcing real-world applicability.  

📌 **Reference:** Stallings, W. (2016). *Cryptography and Network Security.* Pearson Education. 


---

## Functions Implemented  

This task required implementing key functions to analyze **SHA-256 hashes** of English words and determine which had the highest number of **leading zero bits**. The functions were designed to efficiently compute, store, and compare hash results.

### 1. Computing SHA-256 Hash & Leading Zero Count  
A function was implemented to compute the **SHA-256 hash** of a given word and count the number of **leading zero bits** in its binary representation.

#### **Key Steps:**  
- Compute the SHA-256 hash using Python’s `hashlib` module.
- Convert the **hexadecimal hash** to a **binary string** (256-bit representation).
- Count the number of **leading zero bits**.

#### **Code Snippet:**
```python
hash_hex = hashlib.sha256(word.encode()).hexdigest()  
hash_bin = bin(int(hash_hex, 16))[2:].zfill(256)  
leading_zeros = len(hash_bin) - len(hash_bin.lstrip('0'))
```

### 2. Processing a Dictionary of Words  
To efficiently find words with the most leading zeroes, I used an English word dataset and processed each word to compute its leading zero count.

#### **Key Steps:**  
- Loaded an English word dataset (from NLTK).
- Computed the **leading zero count** for each word.
- Stored the results in a dictionary for easy comparison.

#### **Code Snippet:**
```python
word_hashes = {word: sha256_leading_zeros(word) for word in english_words}
```

### 3. Finding the Best Candidates  
Once all words were processed, the next step was to identify the word(s) with the highest number of leading zero bits. This was done by:

- Computing the **maximum leading zero count**.
- Extracting the words that matched this maximum count.

#### **Key Steps:**  
- Find the **maximum number of leading zero bits** from the computed results.
- Extract all words that have this maximum count.

#### **Code Snippet:**
```python
max_zeros = max(word_hashes.values())
best_words = [word for word, zeros in word_hashes.items() if zeros == max_zeros]
```

### 4. Verifying Word Validity  
It was important to ensure that the words with the highest number of leading zeroes were valid English words. To achieve this, the words were checked against the **NLTK word corpus** to confirm their validity.

#### **Key Steps:**  
- Used **NLTK's word corpus** to verify the validity of each word.
- Only **valid words** were considered for final output.

#### **Code Snippet:**
```python
def is_valid_word(word):
    return word.lower() in words.words()
```

### 5. Displaying Results  
Finally, I displayed the word(s) with the highest leading zero bits, including their corresponding **SHA-256 hash** and the number of leading zero bits.

#### **Key Steps:**  
- Display the words with the **most leading zeros**.
- Show their **SHA-256 hash** and the number of **leading zero bits**.

#### **Code Snippet:**
```python
for word in best_words[:10]:  # Display first 10 words with most leading zeroes
    print(f"Word: {word}, Leading Zeros: {max_zeros}, SHA-256: {hashlib.sha256(word.encode()).hexdigest()}")
```

## Comparison of Work

| **Aspect**                      | **Blockchain Mining**                              | **This Task**                                         |
|----------------------------------|----------------------------------------------------|------------------------------------------------------|
| **Goal**                         | Find a nonce that results in a hash with leading zeros. | Find words with the highest number of leading zero bits in their SHA-256 hash. |
| **Method**                       | Generate random nonces and hash them to meet difficulty requirements. | Hash predefined English words and analyze their leading zero bits. |
| **Dataset**                      | Random nonces generated on-the-fly.                | A fixed dataset of English words from the NLTK corpus. |
| **Computational Expense**        | High, requires significant processing power (e.g., ASICs, GPUs). | Moderate, processes a predefined dataset of words. |
| **Difficulty Regulation**        | Adjusted dynamically by the network.               | Not applicable, but involves computing hash properties of words. |
| **Cryptographic Focus**          | Ensures network security via Proof-of-Work.        | Examines the randomness of hash functions and how certain words align with SHA-256. |
| **Hash Function Used**           | SHA-256                                           | SHA-256                                                |
| **Outcome**                      | A valid block is mined with a hash that has a certain number of leading zeros. | Identification of words with the highest number of leading zero bits in their hash. |
| **Efficiency**                   | Efficient at finding nonces through parallelism and large-scale computations. | Moderate in efficiency; larger dictionaries require more computation but can be optimized. |
| **Relevance to Cryptography**    | Critical to secure decentralized networks.         | Demonstrates hash randomness and cryptographic unpredictability. |

### Conclusion
While both blockchain mining and this task use **SHA-256** hashes, the objectives and methods differ significantly. **Blockchain mining** focuses on generating nonces with the required hash properties to secure a network, while this task demonstrates how certain English words naturally align with cryptographic hash functions and their inherent randomness.

---

### Key Observations

- **Edge cases** such as short words and repeated characters were handled appropriately.
- **Performance** was good for processing a dictionary of words, but could be optimized further for larger datasets (e.g., by using parallel processing).
- All **valid words** were correctly verified against the NLTK dictionary, ensuring real-world applicability of the results.

---

## Testing

Testing ensures the correctness and efficiency of the implemented functions. This task required testing the computation of **SHA-256 hashes**, counting of **leading zero bits**, and verification of word validity.

### Test Coverage

| **Category**             | **Description**                                              | **Result**  |
|-------------------------|--------------------------------------------------------------|------------|
| **Basic Functionality**  | Ensured the SHA-256 hash function works and computes leading zero bits correctly for known words like "example" | ✅ Passed  |
| **Edge Case Handling**   | Tested edge cases such as very short words ("a") and long words | ✅ Passed  |
| **Dictionary Verification** | Verified that only valid words from the NLTK corpus are processed | ✅ Passed  |
| **Performance**          | Measured time for processing the entire dataset of English words | ✅ Passed  |
| **Correct Output**       | Checked if words with the most leading zeros were correctly displayed with their hashes | ✅ Passed  |

---

### Running the Tests  

- All test cases are included in `tasks.ipynb` – simply run all cells
- No external setup is required. 

*(For a more detailed breakdown of test cases, see the notebook.)*

---

## References

| Function                          | Reference                                                      | Why It Was Used                                                                 |
|-----------------------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| `sha256_leading_zeros`            | NIST (2015) - *Secure Hash Standard (SHA-256)*                 | To understand the SHA-256 hashing process and its standard specification.      |
| `sha256_leading_zeros`            | Schneier, B. (1996) - *Applied Cryptography*                   | To understand cryptographic hash functions and their properties (like pre-image resistance). |
| `is_valid_word`                   | NLTK Docs - *NLTK Word Corpus*                                | To ensure that the words tested for leading zeros are valid English words.    |
| `sha256_leading_zeros`            | Princeton University (2018) - *Cryptography and Cryptanalysis Lecture* | To understand the theoretical background of hash functions and their applications. |
| `is_valid_word`                   | Python Docs - *String Methods*                                 | To verify that words are converted correctly and checked against the NLTK corpus. |
| `sha256_leading_zeros`            | Nakamoto, S. (2008) - *Bitcoin: A Peer-to-Peer Electronic Cash System* | To understand the concept of Proof-of-Work and how hashes with leading zeros are used in blockchain systems. |


## Task 7
### Turing Machines

## Task 8
### Computational Complexity