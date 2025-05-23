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
12. [Final Thoughts & Conclusion](#final-thoughts--conclusion)

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

## **Setup Instructions**
To set up and run the code, follow these steps:

### Clone the repository
   ```sh
   git clone https://github.com/sophieboyle1/computational-theory.git
   ```
### Navigate to the repository directory
   ```
   cd computational-theory
   ```

### Install dependencies
   ```
   pip install -r requirements.txt
   ```

Ensure you have Python 3.8 or later installed.
If you don’t have Jupyter installed, install it manually:

   ```
   pip install jupyter
   ```

### Open the Jupyter notebook
   ```
   jupyter notebook tasks.ipynb
   ```
- This will launch the Jupyter Notebook interface in your browser.

### Run the notebook cells
- Execute the code by running individual cells within the notebook.

---


## Task 1: Binary Representations

### **Overview**
In Task 1, I implemented four key functions to manipulate bits in a 32-bit unsigned integer. Bitwise operations are powerful tools often used in fields like cryptography, data compression, and algorithm optimization. While they can be tricky at first, mastering them provides a deeper understanding of how computers handle binary data.

The goal was to create functions that simulate operations commonly seen in cryptographic algorithms like SHA-256—rotating bits, making conditional choices, and computing majority values at the bit level.

---

### **Research and Insights**  

Bitwise operations are fundamental to **low-level computing**, playing a key role in **cryptography, data compression, networking, and graphics**. Unlike C, which strictly enforces fixed-width integers (e.g., 32-bit unsigned integers), Python **automatically expands integers as needed**. To correctly **simulate a 32-bit unsigned integer**, operations must include **bit masking** (`& 0xFFFFFFFF`) to discard excess bits ([Python Docs - Bitwise Operations](https://docs.python.org/3/library/stdtypes.html#bitwise-operations)).  

For **Task 1**, I implemented four key functions—**bitwise rotation (`rotl`, `rotr`), conditional selection (`ch`), and majority voting (`maj`)**—which are **widely used in cryptographic security and data manipulation** ([FIPS PUB 180-4 - SHA-256 Standard](https://csrc.nist.gov/publications/detail/fips/180/4/final)).  

---

### 🔐 **Bitwise Operations in Cryptography**  

Bitwise functions are crucial in cryptographic hash functions like **SHA-256**, where they enhance **diffusion** (spreading input bits widely) and **non-linearity** (making output difficult to reverse) ([Shannon’s Principles of Cryptographic Security](https://en.wikipedia.org/wiki/Diffusion_(cryptography))).  

- **`rotl(x, n)`, `rotr(x, n)`** – Used in cryptographic rounds to **shuffle bits efficiently**, ensuring that small input changes drastically alter the output.  
- **`ch(x, y, z)`** – Selects bits based on conditions, adding complexity and increasing non-linearity in hash functions.  
- **`maj(x, y, z)`** – Determines the majority bit at each position, reinforcing randomness and strengthening security ([Understanding Bitwise Operations in Cryptographic Algorithms](https://medium.com/%40conniezhou678/mastering-data-algorithm-part-30-mastering-bitwise-manipulation-in-python-81d03ff6f36d)).  
 

---

### 🚀 **Real-World Applications Beyond Cryptography**  

Bitwise operations extend beyond cryptographic security and play a major role in various fields, including **data compression, networking, and image processing**.  

- **Data Compression** – Algorithms like **Huffman coding** and **Run-Length Encoding (RLE)** use bitwise operations to pack data into smaller units, reducing storage space ([Data Compression Explained](https://www.cs.usfca.edu/~galles/visualization/huffman.html)).  

- **Networking & Protocols** – Protocols like **TCP/IP, IPv4, and Ethernet** use bitwise masks to efficiently store and manipulate header flags. For example, **subnet masks** in networking rely on **bitwise AND operations** to determine whether two IP addresses belong to the same network ([RFC 791 - Internet Protocol](https://tools.ietf.org/html/rfc791)).  

- **Graphics & Image Processing** – Bitwise operations help extract **RGB** color channels from a **24-bit pixel** value. Since color data is stored as **bit fields**, using bitwise shifts and masks is significantly faster than arithmetic operations.  
  ```python
  red = (pixel_value >> 16) & 0xFF  # Extracts the red component
  green = (pixel_value >> 8) & 0xFF  # Extracts the green component
  blue = pixel_value & 0xFF  # Extracts the blue component
   ```

### **Functions Implemented**

Each function plays a crucial role in cryptographic algorithms like **SHA-256**, where bitwise operations ensure **diffusion, non-linearity, and security** ([FIPS PUB 180-4 - SHA-256 Standard](https://csrc.nist.gov/publications/detail/fips/180/4/final)).  

1. **`rotl(x, n)` - Rotate Left**  
   Performs a **left circular shift** on a 32-bit unsigned integer `x` by `n` positions.  
   - Overflow bits **wrap around** to the rightmost positions.
   - Used in cryptographic hash functions (e.g., SHA-256) to **shuffle bits efficiently**, ensuring that small input changes drastically alter the output (avalanche effect).  
   - Example:  
     ```python
     rotl(0b0001, 2)  # Output: 0b0100
     ```
   
2. **`rotr(x, n)` - Rotate Right**  
   Performs a **right circular shift** on a 32-bit unsigned integer `x` by `n` positions.  
   - Overflow bits **wrap around** to the leftmost positions.
   - Used in cryptographic compression functions to **spread entropy** across bits, increasing randomness.  
   - Example:  
     ```python
     rotr(0b1000, 1)  # Output: 0b0100
     ```
   
3. **`ch(x, y, z)` - Choose Function**  
   A conditional selection function that picks bits based on `x`.  
   - If `x` has a **1**, it selects the corresponding bit from `y`.  
   - If `x` has a **0**, it selects the corresponding bit from `z`.  
   - Used in **SHA-256 compression functions** to introduce **non-linearity**, making hash outputs unpredictable ([SHA-2 Explained](https://en.wikipedia.org/wiki/SHA-2)).  
   - Example:  
     ```python
     ch(0b1010, 0b1111, 0b0000)  # Output: 0b1010
     ```

4. **`maj(x, y, z)` - Majority Function**  
   Determines the **majority bit** at each position among `x`, `y`, and `z`.  
   - If at least **two of the inputs** have `1`s at a given position, the output will be `1`.  
   - Used in cryptographic hashing to **reinforce randomness and security**, making the output difficult to reverse ([Understanding Bitwise Operations in Cryptographic Algorithms](https://medium.com/%40conniezhou678/mastering-data-algorithm-part-30-mastering-bitwise-manipulation-in-python-81d03ff6f36d)).  
   - Example:  
     ```python
     maj(0b1010, 0b1111, 0b0000)  # Output: 0b1010
     ```
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

## **Research and Insights** 🔬  

### **Understanding Hash Functions**  
Hash functions are fundamental in computing, serving critical roles in **data integrity, cryptography, and efficient data retrieval**. A hash function takes an input (e.g., a string) and converts it into a **fixed-length integer**, making it useful for quick lookups and ensuring **data consistency** ([Python Docs - Hash Functions](https://docs.python.org/3/library/hashlib.html)).  

Common applications of hashing include:  
- **Data Integrity** → Ensures that files and messages remain unchanged during transmission.  
- **Efficient Lookups** → Used in **hash tables and databases** to enable quick data retrieval ([MIT Lecture 4: Hashing](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/resources/lecture-4-hashing/)).  
- **Cryptographic Security** → Used in **password storage, digital signatures, and blockchain security** ([NIST FIPS PUB 180-4](https://csrc.nist.gov/publications/detail/fips/180/4/final)).  

---

### **Translating the C Function to Python**  
The original **C function** computes a hash using a **weighted sum** and a **modulo operation**. When translating it into **Python**, several key adaptations were required:  

- **Removing Pointers** → Python strings are immutable, so **direct character manipulation** with pointers is not possible. Instead, a **for loop** iterates over the string.  
- **Using ASCII Values** → The `ord()` function retrieves character ASCII values, replacing pointer-based access (`*s`).  
- **Maintaining Consistency** → The **modulo 101 operation** remains to **limit hash values** within a fixed range, ensuring consistent output across implementations ([Princeton Algorithms - Hashing](https://algs4.cs.princeton.edu/34hash/)).  

---

### **Why Hashing Matters for Performance**  
A well-designed hash function ensures **efficient storage and retrieval** by minimizing **collisions** (cases where different inputs produce the same hash). This is essential for cryptographic security and fast indexing in databases.  

- **Distributes values evenly** → Prevents clustering, which can slow down lookups.  
- **Uses prime numbers** → Constants like `31` and `101` in hashing algorithms help ensure **uniform distribution**, reducing predictable cycles and improving performance ([Effective Java - Item 11: HashCode](https://docs.oracle.com/en/java/)).  

---

### **Real-World Applications of Hashing**  
Hash functions play a crucial role in:  

- **Databases** → Hash-based indexing enables **constant-time lookups** in key-value stores like **Redis** and **MongoDB**.  
- **Cryptography** → Secure **password hashing** (e.g., **SHA-256, bcrypt**) prevents easy password recovery from stolen databases ([NIST Cryptographic Standards](https://csrc.nist.gov/publications/detail/fips/180/4/final)).  
- **File Verification** → Hashes such as **MD5, SHA-1, and SHA-256** are used to check file integrity by detecting **corruptions or unauthorized modifications**.  

📖 **Further Reading:**  
- [Python Docs - Hash Functions](https://docs.python.org/3/library/hashlib.html)  
- [MIT Lecture 4: Hashing from Introduction to Algorithms](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/resources/lecture-4-hashing/)  
- [Cryptographic Hashing Explained](https://crypto.stackexchange.com/questions/39680/why-do-hash-functions-need-padding)  


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

### **References**

| **Function / Concept**          | **Reference** | **Why It Was Used** |
|----------------------------------|---------------|----------------------|
| `hash_function`                 | [Oracle Docs - Effective Java (Item 11: HashCode)](https://docs.oracle.com/en/java/) | To understand why prime numbers like 31 are commonly used in hash code generation. |
| `hashlib.sha256()`             | [Python Docs - Hashing](https://docs.python.org/3/library/hashlib.html) | To understand how to generate SHA-256 hashes in Python. |
| SHA-256 leading zero analysis  | [MIT OpenCourseWare - Hash Functions](https://openlearninglibrary.mit.edu/) | To explore the theory and behavior of cryptographic hash functions. |
| Hash distribution concepts      | [Princeton - Hashing Functions](https://algs4.cs.princeton.edu/34hash/) | To understand uniform distribution and the role of primes in hash spread. |
| `%` (Modulo operation)         | [Python Docs - Modulo Operator](https://docs.python.org/3/reference/expressions.html#binary-arithmetic-operations) | To explain how modulo keeps hash values in a desired range. |

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

## **Research and Insights** 🔬

SHA-256 is a part of the **SHA-2 family** of cryptographic hash functions, designed for **data integrity, secure authentication, and digital signatures**. It is widely used in applications such as **password hashing, blockchain security, and digital certificates**.  

Before hashing, **messages must be padded** to ensure they conform to the **512-bit block size** required by the SHA-256 algorithm ([NIST FIPS PUB 180-4](https://csrc.nist.gov/publications/detail/fips/180/4/final)).  

Padding is essential because SHA-256 operates on **fixed-size blocks**. If the input message is too short, it must be **extended without introducing ambiguity**. This follows the **Merkle–Damgård construction**, a fundamental structure in cryptographic hash functions, which ensures that small input changes lead to drastically different hash outputs ([Cryptographic Hash Functions - Springer](https://link.springer.com/book/10.1007/978-3-319-21936-3)).

---

### **Why is Padding Necessary?**
1. **Ensures Message Length is a Multiple of 512 Bits**  
   - The **SHA-256 compression function** processes data in **512-bit chunks**.
   - If a message is shorter than 512 bits, it must be **padded** to maintain a consistent structure ([SHA-2 Specification - RFC 6234](https://tools.ietf.org/html/rfc6234)).  

2. **Prevents Collision & Length Extension Attacks**  
   - Without proper padding, an attacker could **append data** to an existing hash and manipulate it.  
   - SHA-256 adds a **length field** at the end, preventing adversaries from extending the hash without detection ([Understanding Length Extension Attacks](https://crypto.stackexchange.com/questions/3975/what-is-a-length-extension-attack-and-how-can-it-be-prevented)).  

3. **Follows the SHA-2 Specification**  
   - SHA-256 **strictly defines the padding process** in **FIPS PUB 180-4**.
   - Padding ensures **compatibility** with existing cryptographic standards, making SHA-256 widely accepted in **blockchain security, TLS/SSL encryption, and secure file verification**.  

📖 **Further Reading:**  
- [NIST FIPS PUB 180-4 – Secure Hash Standard](https://csrc.nist.gov/publications/detail/fips/180/4/final)  
- [Cryptographic Hashing and Padding Explained](https://crypto.stackexchange.com/questions/39680/why-do-hash-functions-need-padding)  
- [SHA-256 Padding – A Technical Breakdown](https://en.wikipedia.org/wiki/SHA-2#Padding)  

---

## **Functions Implemented**
To correctly apply **SHA-256 padding**, several functions were implemented. Each function handles a specific step in ensuring the message is properly formatted before hashing.

1. **Reading the File Contents**  
   - The function reads the input **as raw bytes** to ensure that **all data is processed accurately**.  
   - This is critical because **text encoding differences** (e.g., UTF-8 vs. ASCII) could lead to **hash mismatches**.

2. **Computing the Original Bit Length**  
   - Calculates the **exact length** of the input in bits.  
   - This length is later **appended as metadata** to prevent **hash extension attacks**.

3. **Appending the 1 Bit (`0x80` in Hex)**  
   - SHA-256 **always** requires messages to **end with a single `1` bit** (binary `10000000` or `0x80` in hex).  
   - This marks the **boundary** between the original message and the padding.  

4. **Adding Zero Padding**  
   - After the **1-bit marker**, **zero bits** (`0x00`) are appended **until the message is 448 bits mod 512**.
   - This ensures the message length is aligned before adding the **final length field**.

5. **Appending the Original Message Length**  
   - The **exact bit length** of the original message (before padding) is stored as a **64-bit big-endian integer**.  
   - This prevents **hash extension attacks** by ensuring the hash function cannot be manipulated post-processing.

6. **Extracting the Padding for Verification**  
   - This function isolates and extracts only the **padding bytes** to confirm the process was correctly applied.  
   - The extracted padding is **converted into a human-readable hexadecimal format** for debugging and validation.

Each function **strictly follows the SHA-2 specification**, ensuring the **input is securely processed** before the hashing algorithm executes.  

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

## **Research and Insights** 🔬  

Prime numbers are fundamental in **mathematics, cryptography, and computer science**, serving as the building blocks of **secure encryption, prime factorization, and efficient data structures**. Their **unique properties** make them essential for applications requiring **randomness, security, and irreversibility**.  

The **unpredictable distribution** of prime numbers plays a **critical role in cryptographic security**, ensuring **strong encryption mechanisms** and **resistance to attacks** ([NIST Cryptographic Standards](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)).  

---

### **Why Are Prime Numbers Important?**  
Prime numbers are the **building blocks of integers**, as stated in the **Fundamental Theorem of Arithmetic**:

> *Every integer greater than 1 can be uniquely expressed as a product of prime numbers.*

This **factorization property** makes primes **indispensable** in cryptography, particularly in algorithms that rely on **prime number factorization** for security, such as **RSA encryption** ([Introduction to Modern Cryptography, Katz & Lindell](https://www.cs.umd.edu/~jkatz/imc.html)).  

### 🔐 **Prime Numbers in Cryptography**  
The security of many cryptographic protocols relies on the difficulty of **factoring large prime numbers**. Modern encryption schemes like **RSA** and **Diffie-Hellman key exchange** depend on the **mathematical challenge of factoring the product of two large prime numbers**.

#### **1️⃣ Public Key Cryptography (RSA)**  
- The **RSA algorithm** generates keys by multiplying two **large prime numbers** (**p** and **q**).  
- The security of RSA depends on the **infeasibility of prime factorization**—a problem that **classical computers cannot efficiently solve for sufficiently large numbers**.  
- **Example:** A **2048-bit RSA key** is generated using two **1024-bit prime numbers**, ensuring **strong encryption** for sensitive data ([RSA Algorithm - NIST Guidelines](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-4.pdf)).  

#### **2️⃣ Elliptic Curve Cryptography (ECC)**  
- **ECC** uses properties of **prime numbers** in **modular arithmetic over elliptic curves**.  
- ECC provides **equivalent security** to RSA but with **smaller key sizes**, making it ideal for **resource-constrained devices (e.g., IoT, mobile security)**.  
- Example: A **256-bit ECC key** provides the **same security level** as a **3072-bit RSA key**, reducing computational overhead while maintaining encryption strength ([NSA Suite B Cryptography](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-56a.pdf)).  

#### **3️⃣ Primality Testing in Cryptography**  
Before using a number in cryptographic systems, it must be **verified as prime**.  
Common **primality tests** include:  
- **Miller-Rabin Test** → A **probabilistic** test commonly used for **large primes** in cryptographic applications ([Miller & Rabin, 1976](https://dl.acm.org/doi/10.1145/321892.321894)).  
- **AKS Primality Test** → A **deterministic** algorithm proving whether a number is prime in **polynomial time**.  
- **Fermat’s Little Theorem** → A **basic** test used as a **preliminary filter** before applying more rigorous primality checks.  

📖 **Further Reading:**  
- [RSA Encryption and Prime Numbers - MIT OpenCourseWare](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-875-cryptography-and-cryptanalysis-fall-2005/)  
- [NIST Guidelines on Cryptographic Primitives](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)  
- [Elliptic Curve Cryptography Explained](https://safecurves.cr.yp.to/)  

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

### **References**

| **Concept / Function**            | **Reference**                                                                 | **Why It Was Used** |
|-----------------------------------|-------------------------------------------------------------------------------|----------------------|
| **Trial Division Algorithm**      | [MIT OpenCourseWare - Number Theory](https://ocw.mit.edu/courses/mathematics/18-785-number-theory-i-fall-2021/) | To understand basic prime checking methods. |
| **Mathematical Primality Tests**  | [Princeton - Algorithms Textbook](https://algs4.cs.princeton.edu/home/)     | To compare different prime-checking techniques. |
| **Sieve of Eratosthenes**         | [Harvard - Computational Number Theory](https://people.seas.harvard.edu/~knill/teach/computationalnumbertheory2023/index.html) | To implement an optimized prime generation method. |
| **Cryptographic Prime Numbers**   | [NIST - Cryptographic Standards (FIPS 186-4)](https://csrc.nist.gov/publications/detail/fips/186/4/final) | To understand prime number use in encryption. |
| **Efficiency Analysis**           | [Stanford - Algorithm Complexity Lecture](https://web.stanford.edu/class/archive/cs/cs161/cs161.1168/lecture5.pdf) | To compare time complexity of different approaches. |


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

## **Research and Insights** 🔬  

Prime numbers play a **critical role** in cryptography and computational number theory. One particularly **important application** is the derivation of **hash function constants** using the **fractional part of square roots of primes**. This method is specifically used in cryptographic hash functions like **SHA-256**, where these constants enhance **security, diffusion, and unpredictability** ([NIST FIPS PUB 180-4](https://csrc.nist.gov/publications/detail/fips/180/4/final)).  

---
### **Why Prime Numbers?**  
Prime numbers possess **unique mathematical properties** that make them ideal for cryptographic applications:  

- **Unpredictability** → The distribution of prime numbers appears **random**, reducing the risk of patterns in cryptographic algorithms ([Hardy & Wright, *An Introduction to the Theory of Numbers*](https://global.oup.com/academic/product/an-introduction-to-the-theory-of-numbers-9780199219865)).  
- **Factorization Difficulty** → Many security protocols (e.g., **RSA encryption**) rely on the computational difficulty of factoring large prime numbers ([RSA Algorithm - NIST Guidelines](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.186-4.pdf)).  
- **Uniformity** → Constants derived from prime numbers ensure that hash functions avoid **predictable biases**, maintaining security against cryptographic attacks ([Understanding Cryptographic Hash Functions](https://crypto.stackexchange.com/questions/39680/why-do-hash-functions-need-padding)).  

---
### 🔢 **The Mathematical Formula**  

The constants in **SHA-256** are derived from the **fractional part of the square roots of prime numbers**. The calculation follows these steps:

1. **Extract the Fractional Part of a Square Root**  
   $$
   \text{frac}(\sqrt{p}) = \sqrt{p} - \lfloor \sqrt{p} \rfloor
   $$
   where \( p \) is a prime number.

2. **Scale the Fractional Part to a 32-bit Integer**  
   $$
   \text{frac32} = \lfloor (\text{frac}(\sqrt{p}) \times 2^{32}) \rfloor
   $$  
   This extracts the **first 32 bits** of the fractional part, converting it into a **cryptographic constant**.


### **📖 Further Reading:**  
- [NIST FIPS PUB 180-4 – Secure Hash Standard](https://csrc.nist.gov/publications/detail/fips/180/4/final)  
- [Cryptographic Hash Functions - Theory & Applications](https://crypto.stackexchange.com/questions/39718/how-are-hash-functions-derived)  
- [Prime Numbers & Cryptographic Security](https://crypto.stackexchange.com/questions/15701/why-are-prime-numbers-used-in-cryptography)  

---

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

- Loading a local text file of English words `(words_alpha.txt).`
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
with open("words_alpha.txt") as file:
    english_words = [line.strip() for line in file]

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
| **Dataset**                      | Random nonces generated on-the-fly.                | A fixed dataset of English words from a .txt file. |
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
- All words were loaded from a pre-cleaned local file, ensuring they were valid and usable without external verification.

---

## Testing

Testing ensures the correctness and efficiency of the implemented functions. This task required testing the computation of **SHA-256 hashes**, counting of **leading zero bits**, and verification of word validity.

### Test Coverage

| **Category**             | **Description**                                              | **Result**  |
|-------------------------|--------------------------------------------------------------|------------|
| **Basic Functionality**  | Ensured the SHA-256 hash function works and computes leading zero bits correctly for known words like "example" | ✅ Passed  |
| **Edge Case Handling**   | Tested edge cases such as very short words ("a") and long words | ✅ Passed  |
| **File Parsing** | Verified that words were correctly loaded and stripped from the local file | ✅ Passed  |
| **Performance**          | Measured time for processing the entire dataset of English words | ✅ Passed  |
| **Correct Output**       | Checked if words with the most leading zeros were correctly displayed with their hashes | ✅ Passed  |

---

### Running the Tests  

- All test cases are included in `tasks.ipynb` – simply run all cells
- No external setup is required. 

*(For a more detailed breakdown of test cases, see the notebook.)*

---

## References

### **References**

| **Function**                      | **Reference**                                                                                                  | **Why It Was Used**                                                                 |
|----------------------------------|----------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| `sha256_leading_zeros`           | [NIST (2015) - Secure Hash Standard (SHA-256)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf)    | To understand the SHA-256 hashing process and its standard specification.           |
| `sha256_leading_zeros`           | [Schneier, B. (1996) - Applied Cryptography](https://www.schneier.com/books/applied_cryptography/)           | To understand cryptographic hash functions and their properties like pre-image resistance. |
| `sha256_leading_zeros`           | [Princeton - Cryptography and Cryptanalysis Lecture](https://www.cs.princeton.edu/courses/archive/spr18/cos433/) | To understand the theoretical background of hash functions and their applications.  |
| `sha256_leading_zeros`           | [Nakamoto, S. (2008) - Bitcoin Whitepaper](https://bitcoin.org/bitcoin.pdf)                                   | To understand the concept of Proof-of-Work and how hashes with leading zeros are used in blockchain systems. |
| `english_words.txt`              | [dwyl/english-words GitHub](https://github.com/dwyl/english-words)                                           | Source of the plain text English word list.                                         |

---

## Task 7: Turing Machines

### Overview  
This task focuses on designing a **Turing Machine** that performs a simple yet fundamental operation: **adding 1 to a binary number**. The machine operates on a one-dimensional tape, simulating the behavior of an early computational model proposed by **Alan Turing** in 1936.

The binary number is read **from left to right**, with the **right-most digit treated as the least significant bit (LSB)**. The Turing Machine uses a set of predefined rules and transitions to:

- Locate the LSB
- Perform binary addition by flipping bits
- Handle **carry propagation**
- Deal with **overflow** by extending the tape

This task not only illustrates **Turing completeness**, but also reinforces the connection between theoretical models and practical computation.

The implementation demonstrates:
- A working simulation of a Turing Machine using Python.
- A state-based approach to modifying binary values.
- How basic arithmetic operations can be modeled through tape manipulation and state transitions.

---

## Research and Insights

A **Turing Machine** is a theoretical model of computation introduced by **Alan Turing in 1936**, used to formalize the concept of an algorithm or computable function. It operates using a **tape (infinite memory)**, a **head** that reads and writes symbols, and a **finite set of states** that define how the machine reacts to input symbols ([Turing, 1936](https://plato.stanford.edu/entries/turing-machine/)).

This task simulates binary addition by **incrementing a binary number by 1** using a Turing Machine model. It reinforces how even basic arithmetic operations can be reduced to simple mechanical steps using states and transitions.

### 💡 Why This Task Matters

- **Turing Completeness**: A Turing Machine can compute anything that is computable, including arithmetic, logic, and more complex operations ([Hopcroft & Ullman, 1979](https://www.cs.cornell.edu/~kozen/Papers/hu79.pdf)).
- **Foundational Theory**: Understanding Turing Machines provides the foundation for studying **automata theory**, **decidability**, and **computational complexity**.
- **Practical Simulation**: Though abstract, Turing Machine logic underpins concepts used in compilers, interpreters, and digital logic circuits ([Arora & Barak, 2009](https://theory.cs.princeton.edu/complexity/)).

### 🧠 How This Task Demonstrates Computation

In this simulation, a binary number such as `100111` is incremented to `101000` using the following logic:

- The machine moves to the **right-most bit** (LSB).
- It **flips `1`s to `0`s** until it finds a `0`, which it flips to `1`.
- If all bits are `1`, the machine **prepends a `1`** to represent **binary overflow**, similar to how arithmetic carry works in real systems.

This reflects the logic of **binary addition with carry propagation** and demonstrates how a simple set of instructions can simulate a real-world arithmetic operation.

📚 **Further Reading**:  
- [Stanford Encyclopedia of Philosophy – Turing Machines](https://plato.stanford.edu/entries/turing-machine/)  
- [Hopcroft & Ullman – Introduction to Automata Theory, Languages, and Computation](https://www.cs.cornell.edu/~kozen/Papers/hu79.pdf)  
- [Michael Sipser – Introduction to the Theory of Computation](https://www.amazon.com/Introduction-Theory-Computation-Michael-Sipser/dp/113318779X)  
- [Arora & Barak – Computational Complexity: A Modern Approach](https://theory.cs.princeton.edu/complexity/)

---

## Functions Implemented

The Turing Machine for binary incrementation is implemented using a Python class structure. It simulates a tape-based machine that reads and modifies binary digits one step at a time using simple logic and state transitions.

### 1. `__init__(self, input_binary)`
Initializes the Turing Machine:
- Converts the input binary string into a mutable tape (list of characters).
- Appends a blank symbol (`"_"`) to simulate infinite tape space.
- Sets the head to the **right-most non-blank symbol** (LSB).
- Initializes the machine state to `"Find_LSB"`.

> **Why?**  
> This sets up the machine to begin processing from the correct starting point, mimicking Turing Machine tape mechanics.

---

### 2. `__str__(self)`
Returns the final binary output as a string:
- Joins the tape and removes any trailing blanks for cleaner output.

---

### 3. `step(self)`
Performs a **single step** based on the current state:
- If the symbol under the head is `"1"`:
  - Change it to `"0"` and move the head left (carry propagation).
- If the symbol is `"0"`:
  - Change it to `"1"` and enter the `HALT` state (no carry needed).
- If the head moves past the left end (all bits were `"1"`):
  - Insert a `"1"` at the front to handle overflow (e.g., `111 → 1000`).

> 🔁 This function reflects the logic in the **state transition table** defined for Task 7.

---

### 4. `run(self)`
Runs the Turing Machine until it reaches the `HALT` state:
- Calls the `step()` method repeatedly.
- Returns the final binary string after all transitions are complete.

---

### Example Usage

```python
# Example usage
tm = TuringMachine("100111")
result = tm.run()
print(result)  # Output: 101000
```

## Comparison of Work

### Theoretical vs. Practical Implementation

This task involved simulating a **Turing Machine** for binary incrementation. While conceptually simple, it allowed for deeper comparison between **theoretical Turing Machine models** and **practical code implementations**.

| Aspect | Theoretical Turing Machine | Python Implementation |
|--------|-----------------------------|------------------------|
| **Tape** | Infinite in both directions | Simulated with a Python list, extended when overflow occurs |
| **Head Movement** | Moves left or right, reads and writes | Simulated via index manipulation |
| **State Transitions** | Governed by transition table | Implemented as a `step()` method within a class |
| **Halting** | Machine enters HALT state | `run()` method stops when state becomes `"HALT"` |
| **Overflow Handling** | Insert new `1` to left of tape | Achieved by `insert(0, "1")` in Python |

---

### ✅ Output Verification

The outputs of this implementation match expectations from standard **binary addition with carry**. For example:

| Input | Expected Output | Turing Machine Output |
|-------|------------------|------------------------|
| `100110` | `100111` | ✅ |
| `100111` | `101000` | ✅ |
| `111`    | `1000`   | ✅ |

All tests passed, and the state machine correctly handled edge cases including **carry propagation** and **overflow**.

---

### Learning Outcome

This comparison helped solidify the connection between **abstract computation theory** and **real-world programming**. It highlighted how even basic arithmetic operations like binary incrementation require thoughtful design when modeled through state transitions.

---

## Testing

To ensure correctness, I created test cases that cover standard and edge-case binary inputs. These tests verify that the Turing Machine correctly performs:

- **Binary incrementation**
- **Carry propagation**
- **Overflow handling**

### ✅ Test Coverage

| **Category**             | **Description**                                                                 | **Result**  |
|-------------------------|---------------------------------------------------------------------------------|-------------|
| **Basic Functionality** | Verified that the Turing Machine correctly increments standard binary numbers (e.g., `"100111"` → `"101000"`) | ✅ Passed   |
| **All 1s Input**         | Tested input like `"111"` to ensure the machine correctly handles carry overflow and extends the tape (`"111"` → `"1000"`) | ✅ Passed   |
| **Trailing Zeros**      | Checked if binary numbers ending in multiple zeros (e.g., `"1000"`) are incremented correctly without false carry | ✅ Passed   |
| **Single Bit Input**    | Ensured edge case with one-bit input (e.g., `"1"` or `"0"`) is handled correctly | ✅ Passed   |
| **Tape Expansion**      | Verified that the tape dynamically grows when needed to accommodate overflow     | ✅ Passed   |
| **Stability**           | Ensured no infinite loops or index errors occurred during execution             | ✅ Passed   |

### Sample Code Snippet

```
tm = TuringMachine("100111")
result = tm.run()
print(result)  # Output: "101000"
```

### Running the Tests  

- All test cases are included in `tasks.ipynb` – simply run all cells
- No external setup is required. 

*(For a more detailed breakdown of test cases, see the notebook.)*

---

## References

### **References**

| **Function / Concept**          | **Reference**                                                                                                    | **Why It Was Used**                                                                 |
|--------------------------------|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| `turning_machine_add_one`      | [Stanford Encyclopedia of Philosophy – Turing Machines](https://plato.stanford.edu/entries/turing-machine/)      | To understand the formal model of a Turing Machine and how it manipulates symbols.  |
| `turning_machine_add_one`      | [MIT OpenCourseWare – Introduction to Turing Machines](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-045j-automata-computability-and-complexity-spring-2011/) | For insights into how state transitions and tape operations simulate computation.    |
| **Binary Incrementation Logic**| [Structure and Interpretation of Computer Programs (Abelson & Sussman)](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html) | To explore binary arithmetic and carry propagation from a computational perspective. |
| **Overflow & Tape Expansion**  | [Sipser, M. – Introduction to the Theory of Computation](https://www.amazon.com/Introduction-Theory-Computation-Michael-Sipser/dp/113318779X) | To support understanding of infinite tape handling and formal computation rules.     |
| **State Transitions & Testing**| [Python Documentation – `unittest`](https://docs.python.org/3/library/unittest.html)                            | To structure automated tests and validate each scenario (e.g., overflow, edge cases).|


## Task 8: Computational Complexity

### Overview

This task focuses on analyzing the computational complexity of the Bubble Sort algorithm through a practical, exhaustive approach.

The core objective was to:
- Implement a **Bubble Sort** algorithm that counts the number of comparisons made.
- Apply it to **every permutation** of the list `[1, 2, 3, 4, 5]` (120 total permutations).
- Record and analyze the **number of comparisons** needed for each permutation.
- Use the results to understand **best-case, average-case, and worst-case** performance.

Bubble Sort is a simple comparison-based sorting algorithm that has a worst-case time complexity of **O(n²)**. While inefficient for large datasets, it's excellent for demonstrating sorting logic, comparison count analysis, and complexity trends.

This task allowed me to bridge theory with practice by validating Big-O behavior using real data. It also reinforced why understanding **input order** is critical when evaluating an algorithm’s efficiency.

---

## Research and Insights

Bubble Sort is one of the simplest sorting algorithms and is widely used in educational contexts to introduce the concept of computational complexity. It works by repeatedly comparing and swapping adjacent elements in a list until the entire list is sorted.

Although inefficient for large datasets due to its quadratic time complexity, Bubble Sort is a valuable tool for learning how algorithm performance varies depending on input structure. As described in [GeeksforGeeks – Bubble Sort](https://www.geeksforgeeks.org/bubble-sort/), the algorithm has:

- **Best-case complexity** of O(n) when the input is already sorted.
- **Average and worst-case complexity** of O(n²), especially for reverse-sorted or random input.

In this task, I explored these performance variations by exhaustively applying Bubble Sort to all 120 permutations of a 5-element list using `itertools.permutations` from the [Python itertools module](https://docs.python.org/3/library/itertools.html). This brute-force approach helped validate theoretical claims about time complexity with real data.

This analysis was inspired by methods of evaluating algorithm behavior discussed in [MIT OpenCourseWare – Sorting Complexity](https://ocw.mit.edu), which emphasizes using empirical data to deepen understanding of best, worst, and average-case performance.

Additionally, I used resources like [BuiltIn – Bubble Sort Explained](https://builtin.com) to better understand how simple optimizations (like early termination when no swaps occur) can significantly impact the algorithm’s performance on nearly sorted input.

---

## Functions Implemented

For this task, I implemented a customized version of the **Bubble Sort** algorithm that counts the number of **comparisons** made during sorting. This allowed for a detailed analysis of computational complexity across various input permutations.

### 🔧 `bubble_sort_count_comparisons(arr: list) -> tuple`
This function performs Bubble Sort on a given list and tracks the number of comparisons made during the process.

#### **Key Features:**
- **Comparison Counter**: Tallies each element-to-element comparison.
- **Early Termination**: If no swaps are made during a pass, the function exits early, optimizing performance for sorted lists.
- **Stable Sorting**: Maintains the relative order of elements with equal values.
- **Returns**: A tuple of the sorted list and the total comparison count.

#### Example:
```python
bubble_sort_count_comparisons([5, 4, 3, 2, 1])
# Output: ([1, 2, 3, 4, 5], 10)
```

This function was applied to all 120 permutations of the list `[1, 2, 3, 4, 5]` to measure and compare the number of comparisons needed for each, providing a comprehensive view of Bubble Sort's behavior across different input orders.

---

## Comparison of Work

Below is a comparison between the brute-force permutation analysis method used in this task and other common approaches to analyzing sorting complexity:

| **Approach**                         | **Description**                                                                 | **Use Case**                          | **Accuracy**                          | **Limitations**                              |
|-------------------------------------|---------------------------------------------------------------------------------|---------------------------------------|----------------------------------------|----------------------------------------------|
| Brute-Force Permutation Analysis    | Run the algorithm on every possible permutation of the input to gather exact metrics. | Used in this task for Bubble Sort     | Very high – every case is observed     | Only feasible for small n (e.g., n = 5)       |
| Theoretical Case Analysis           | Analyze algorithm based on best, average, and worst-case scenarios mathematically.     | Standard in textbooks and research     | High – based on asymptotic behavior    | Doesn't capture real-world edge cases         |
| Empirical Testing (Random Samples)  | Run algorithm on multiple random inputs to estimate average behavior.                  | Used in benchmarking                  | Moderate – depends on sample size      | Results may vary; lacks completeness          |
| Visualization-Based Analysis        | Use graphical tools to trace swaps and comparisons visually.                          | Helpful in education/demonstration    | Qualitative, not always quantitative   | Doesn't scale; lacks statistical depth        |

---

**Conclusion**:  
The **brute-force permutation analysis** method used in this task provides a **complete and quantifiable** understanding of Bubble Sort's behavior on a fixed-size input. While computationally intensive, it is well-suited for small datasets and reinforces complexity concepts through real data.

---

## Testing

To validate the correctness and performance of the Bubble Sort implementation, a series of tests were conducted to ensure reliable behavior across all expected input scenarios.

The tests focused on:

- ✅ **Correctness**: Confirming that the number of comparisons aligns with expected complexity.
- ✅ **Edge Case Handling**: Handling empty or single-element lists without errors.
- ✅ **Performance**: Ensuring stability across all 120 permutations of `[1, 2, 3, 4, 5]`.

### Test Coverage

| **Category**             | **Description**                                                                 | **Result**  |
|-------------------------|----------------------------------------------------------------------------------|-------------|
| **Basic Functionality** | Bubble Sort correctly sorts and counts comparisons for each permutation.         | ✅ Passed   |
| **Best Case**           | Already sorted list requires minimum comparisons (4 comparisons).                | ✅ Passed   |
| **Worst Case**          | Reverse sorted list hits the max comparisons (10 comparisons).                   | ✅ Passed   |
| **Average Case**        | Random permutations yield 6–9 comparisons, consistent with O(n²) complexity.     | ✅ Passed   |
| **Empty List**          | Algorithm handles `[]` without failure.                                          | ✅ Passed   |
| **Single Element**      | List with one item (`[1]`) returns 0 comparisons.                                | ✅ Passed   |
| **Stability**           | All 120 permutations execute without crashes or infinite loops.                  | ✅ Passed   |


### Running the Tests  

- All test cases are included in `tasks.ipynb` – simply run all cells
- No external setup is required. 

*(For a more detailed breakdown of test cases, see the notebook.)*

---

## References

| **Topic**               | **Reference**                                                                 | **Why It Was Used**                                                                 |
|------------------------|--------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Bubble Sort Algorithm   | [GeeksforGeeks – Bubble Sort](https://www.geeksforgeeks.org/bubble-sort/)     | To understand the step-by-step logic and behavior of Bubble Sort.                   |
| Algorithm Complexity    | [MIT OCW – Sorting Algorithms](https://ocw.mit.edu)                            | To confirm theoretical time complexities and comparison expectations.               |
| Permutations            | [Python Docs – itertools.permutations](https://docs.python.org/3/library/itertools.html#itertools.permutations) | To generate all 120 permutations of the 5-element list.                             |
| Optimization Techniques | [Real Python – Efficient Code](https://realpython.com)                        | Helped with optimizing the Bubble Sort (early exit condition).                      |
| Visualization Insight   | [CS50 – Sorting Visualizations](https://cs50.harvard.edu/)                    | Provided intuition for how Bubble Sort operates through animations and visuals.     |

---

---

## Final Thoughts & Conclusion

This notebook presents a comprehensive journey through key topics in **Computational Theory**, combining core principles with hands-on Python implementation. Each of the eight tasks explored a different aspect of how computers process, secure, and analyze information at a low level.

### Task Highlights

- **Task 1: Binary Representations**  
  Introduced essential bitwise operations such as rotations, majority, and choice — foundational in cryptography.

- **Task 2: Hash Functions**  
  Explored simple hashing techniques and the importance of prime constants in minimizing hash collisions.

- **Task 3: SHA-256 Padding**  
  Demonstrated how padding ensures that messages conform to fixed-length blocks required by cryptographic hash functions.

- **Task 4: Prime Numbers**  
  Compared deterministic and probabilistic methods for generating primes, showing their trade-offs in performance and accuracy.

- **Task 5: Roots**  
  Extracted 32-bit fractional root values from primes — constants used in cryptographic algorithms like SHA-256.

- **Task 6: Proof of Work**  
  Simulated a mining-like challenge by finding English words whose SHA-256 hashes begin with leading zero bits, connecting theory with blockchain concepts.

- **Task 7: Turing Machine**  
  Built a simple machine that incremented a binary number, reinforcing the fundamentals of state-based computation.

- **Task 8: Computational Complexity**  
  Analyzed the Bubble Sort algorithm across all permutations of a 5-element list, validating theoretical complexity with practical data.

### 📚 Key Takeaways

- Computational theory has real-world impact — from hashing and encryption to optimization and automation.
- Understanding bitwise logic, hashing mechanisms, and sorting complexity provides a strong foundation for fields like **cybersecurity**, **data science**, and **algorithm design**.
- Testing and edge case handling are critical in verifying the correctness and robustness of any implementation.
- Visualizing and measuring algorithm performance offers valuable insight into theoretical claims.

### 🚀 Final Reflection

From **bit manipulation to Turing completeness**, this notebook has strengthened my understanding of how computers "think" and operate. Each task challenged me to not only implement algorithms but also to understand their **underlying logic, applications, and limitations**. The experience has boosted my confidence in solving abstract computational problems with practical tools.

---





