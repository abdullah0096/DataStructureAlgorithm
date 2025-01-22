# Hash tables

- A Hash table is a data structure that stores data as <b>key-value</b> pairs.
    ```cpp
        | Roll No  | Name    | 
        |----------|---------|
        | 101      | Alice   |
        | 322      | Bob     |
        | 453      | Charlie |
        | 555      | Eve     |
    ```
    - To store the above data into a Hash table of `size=10`, Roll No is used as the key and given to a hash function to compute the index i.e. the slot where the key-value pair will be store in the Hash table:
    - Hash function : `key % size = index`  
        - 101 % `10` = 1 ---> index 1
        - 322 % `10` = 2 ---> index 2
        - 453 % `10` = 3 ---> index 3
        - 555 % `10` = 5 ---> index 5
    - Now if the following is to be inserted into the above Hash table : 
    ```cpp
        | Roll No  | Name    | 
        |----------|---------|
        | 111      | Dave    |
    ```
    - 111 % `10` = 1 is the index where the above is the be stored
    - Keys `101` and `111` hash to the same index `1` - this is known as `COLLISION`.

### Collision
Collisions occur when two keys hash to the same index. Collisions are handled using the following methods:

1. **Chaining**:
   - Makes use of a linked list or another data structure to store multiple values.
2. **Open Addressing**:
   - Searches for the next free slot in the hash table using one of the following:
     - Linear Probing, Quadratic Probing, Double Hashing.

In the above example of collision can be resolved using the following

- `Chaining`: Store 111 in a `linked list` at index 1.  
- `Linear Probing` : Check the next available slot in the array sequentially (moving linearly).  
    - In this case index 1 is occupied by 101, then check for 1+1 = 2
    - If index 2 is occupied, which in this case if then move to 2+1 = 3
    - Continue in linear manner till an empty slot if found
    - Thus insert `111 - Dave` at index 6
    - Causes primary clustering (long chains of occupied slots).
- `Quadratic Probing` : Use formula to determine an index
    - Formula : `new_index = (original_index + i²) % size`
        - `i` is the step/iteration number
        - original_index = 111 % 10 = 1
        - If index 1 is occupied, then check 1 + 1² = 2
        - If index 2 is occupied, then check 1 + 2² = 5
        - If index 5 is occupied, then check 1 + 3² = 10
        - Insert `111 - Dave` at index 10  
        - May fail to find an empty slot if the table is too full.
- `Double Hashing` : Use a second hash function to determine an index
    - Formula : `new_index = (original_index + i * h2(key)) % size`
    - `h2(key) = 1 + (key % (size - 1))`
    - More complex to implement, requires a good secondary hash function


### Hash function properties : 
- `Uniformity`: Should distribute keys evenly across the table to minimize collisions.
- `Efficiency`: Should be fast/efficient to compute.
- `Deterministic`: Always produces same output for same input (i.e. no randomness)


## Operations 

### 1. **Insertion**
   - Compute the hash code for the key.
   - Use the hash code to determine the index.
   - Store the key-value pair at the index.

### 2. **Search**
   - Compute the hash code for the key.
   - Check the index. If a collision resolution strategy is used, locate the key accordingly.

### 3. **Deletion**
   - Compute the hash code for the key.
   - Locate the key and remove it from the table.

### Time Complexities:
| Operation   | Average Case | Worst Case |
|-------------|--------------|------------|
| Search      | O(1)         | O(n)       |
| Insertion   | O(1)         | O(n)       |
| Deletion    | O(1)         | O(n)       |

## Applications of Hash Tables

- **Dictionaries/Maps**: Key-value pair storage.
- **Frequency Counting**: Counting occurrences in data.
- **Caching**: Quick retrieval of frequently accessed data.
- **Symbol Tables**: Used in compilers.

## Advantages and Limitations of Hash Tables

### Advantages
- **Fast lookups and insertions** (average-case constant time).
- Efficient for sparse data.
- Flexible for dynamic datasets.

### Limitations
- Dependence on a good hash function.
- Potential for collisions.
- Inefficient for ordered data.
- Iteration is not straightforward.

# Hash Tables in C++

- Hash table in C++ is `std::unordered_map` - Hash-based key-value container.

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, string> umap;

    // Insert
    umap[101] = "Alice";
    umap[322] = "Bob";

    // Access
    std::cout << umap[101] << "\n";

    // Iterate
    for( e : umap)
        std::cout << " roll :: " << e.first << "\t name :: " << e.second << std::endl;

    // Find
    if (umap.find(101) != umap.end()) {
        std::cout << "Alice exists.\n";
    }

    // Erase
    umap.erase(101);

    return 0;
}
```

## Miscellaneous
- Load Factor and Rehashing
    - **Load Factor**: Ratio of the number of elements to the table size.
    - **Rehashing**: When the load factor exceeds a threshold, the table resizes to maintain performance.

- Custom Hash Functions in C++
    ```cpp
    #include <iostream>
    #include <unordered_map>

    struct CustomHash {
        std::size_t operator()(const std::pair<int, int>& p) const {
            return std::hash<int>()(p.first) ^ std::hash<int>()(p.second);
        }
    };

    int main() {
        std::unordered_map<std::pair<int, int>, std::string, CustomHash> custom_map;

        custom_map[{1, 2}] = "Pair1";
        custom_map[{3, 4}] = "Pair2";

        for (const auto& [key, value] : custom_map) {
            std::cout << "(" << key.first << ", " << key.second << "): " << value << "\n";
        }

        return 0;
    }
    ```