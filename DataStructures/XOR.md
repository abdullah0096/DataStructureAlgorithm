# XOR Operator

The XOR (exclusive OR) operator is a binary operator that is commonly used in computer science and mathematics. It operates on two bits and outputs `1` if the bits are different and `0` if they are the same.

---

## **XOR - Truth Table**
| A | B | A ⊕ B |
|---|---|-------|
| 0 | 0 |   0   |
| 0 | 1 |   1   |
| 1 | 0 |   1   |
| 1 | 1 |   0   |


## XOR : Properties

- **Identity Property**
    - XOR with `0` leaves the operand unchanged: \[ A ⊕ 0 = A \]
- **Self-Inverse Property**
    - XOR with itself always results in `0`: \[ A ⊕ A = 0 \]
- **Associative Property**
    - The XOR operator is associative: \[ (A ⊕ B) ⊕ C = A ⊕ (B ⊕ C) \]
- **Inversion Property**
    - XOR inverts the bits of a number, i.e., flips 0 to 1 and 1 to 0.
    - XOR with 1 acts as a `bitwise NOT` operation.
    - \[ A ⊕ 1 = ~A \]
        ```cpp
          1010  (N) 
        ⊕ 1111  (M)
        -----------------
          0101  (Result)
        ```
- **Commutative Property**
    - The XOR operator is commutative i.e. order is not important.
    - \[ A ⊕ B = B ⊕ A \]

- **XOR as Addition Without Carry**
    - In binary arithmetic, XOR can be viewed as addition without carry.

- **Double Application (Cancelation Property)**
    - Applying XOR twice with the same value cancels the effect: \[ (A ⊕ B) ⊕ B = A \]
    - `Encryption`: XOR with 1 or another bit pattern to obscure data, then XOR with the same pattern to retrieve the original.
        - A ⊕ B = C => C ⊕ B = A

- ## **XOR in Bit Manipulation**
    - XOR is widely used in programming, especially for:
    - Swapping variables without a temporary variable:
        ```cpp
        a = a ^ b;
        b = a ^ b;
        a = a ^ b;
        ```

- ## **XOR and Bitwise Masks**
    -   XOR can toggle specific bits when used with a mask:
        - If \( mask = 1 \) at a position, the bit toggles.
        - If \( mask = 0 \) at a position, the bit remains unchanged.
            ```cpp
              10101010  (N) 
          ⊕ 00001111  (M)
             --------------
              10100101  (Result)
            ```

## XOR - Application
- Finding the single unique number in an array where all others appear twice.
- Toggling specific bits in a binary number.

These properties make XOR a powerful and versatile operator in both theoretical and practical contexts.
