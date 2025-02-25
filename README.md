# Computational Theory Assessment
## Sophie Boyle - G00410444
## Introduction

This repository contains solutions for the **Computational Theory** assessment. The goal of this project is to implement and analyze various computational functions, including bitwise operations, hash functions, and cryptographic techniques.

## 📚 **Table of Contents**  
1. [Project Structure](#project-structure)  
2. [Usage Instructions](#usage-instructions)  
3. [Task 1: Binary Representations](#task-1-binary-representations)  
4. [Task 2: Hash Functions](#task-2-hash-functions)  
5. [Task 3: Cryptographic Functions](#task-3-cryptographic-functions)  
6. [References](#references)  

**Each task is structured as follows:**  
- **Overview**  
- **Research and Insights**  
- **Functions Implemented**  
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

### **Testing**
All functions have been **fully tested** in the **Jupyter Notebook (`tasks.ipynb`)** using Python’s built-in **unittest** module.  

### Test Coverage
- ✅ **Standard cases** – Checking expected outputs for bitwise rotations (`rotl`, `rotr`), conditional selection (`ch`), and majority logic (`maj`).
- ✅ **Edge cases** – Rotations by **0** and **32 positions**, alternating bit patterns, and large values.
- ✅ **Error handling** – Ensuring negative values and out-of-range numbers are handled correctly.
- ✅ **Bitwise correctness** – Verified results using **manual bitwise calculations**.

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

## Task 3
### SHA256

## Task 4
### Prime Numbers

## Task 5
### Roots

## Task 6
### Proof of Work

## Task 7
### Turing Machines

## Task 8
### Computational Complexity