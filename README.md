# Dictionary Management System

A console-based dictionary application built in C++ using **Hash Tables with Chaining** for efficient word storage, retrieval, and management. This system demonstrates advanced data structures and file handling techniques.


##  Overview

This Dictionary Management System is a powerful console application that allows users to manage a dictionary of words and their meanings. Built using hash tables with chaining, it provides O(1) average-case time complexity for insertions, deletions, and lookups.

The system automatically loads dictionary data from a text file, maintains alphabetically sorted linked lists at each hash index, and persists all changes back to the file.

##  Features

###  Secure Authentication
- Login system with username and password validation
- 5-attempt limit before account lockout
- Persistent credential storage

###  Dictionary Operations
- **Insert Word**: Add new words with meanings to the dictionary
- **Search Word**: Quick lookup with O(1) average complexity
- **Delete Word**: Remove words from the dictionary
- **Update Meaning**: Modify existing word meanings
- **Auto-complete Suggestions**: Get top 10 word suggestions based on prefix

###  Data Management
- Automatic loading from `Dictionary.txt` file
- Real-time file updates after modifications
- Alphabetically sorted storage within hash buckets
- Duplicate word prevention

###  User Interface
- Color-coded console interface
- Clear menu navigation
- Loading animations and transitions
- User-friendly prompts and error messages

##  Data Structure

### Hash Table with Chaining

```
Hash Array (Size: 97)
│
├─[0] → NULL
├─[1] → NULL
├─[2] → NULL
│   ...
├─[97] → apple → apricot → astronaut → NULL
├─[98] → banana → bear → beautiful → NULL
│   ...
└─[122] → zebra → zoom → NULL
```

**Key Characteristics:**
- **Array Size**: 97 (based on ASCII value of 'a')
- **Hash Function**: `key % 97` where key = ASCII value of first character
- **Collision Resolution**: Chaining with sorted linked lists
- **Node Structure**: `{string word, string meaning, node* next}`

### Why Hash Table?
- **Fast Operations**: O(1) average-case for insert, search, delete
- **Efficient Memory**: Only allocates memory for stored words
- **Scalable**: Can handle thousands of words efficiently
- **Sorted Chains**: Maintains alphabetical order within each chain

##  System Requirements

### Minimum Requirements
- **Operating System**: Windows (uses `windows.h`)
- **Compiler**: GCC/MinGW with C++11 support or higher
- **RAM**: 512 MB
- **Storage**: 10 MB free space
- **Display**: Console/Terminal

### Recommended
- **Compiler**: GCC 11.x or Visual Studio 2019+
- **RAM**: 2 GB
- **IDE**: Visual Studio Code, Code::Blocks, or Dev-C++

##  Installation

### Step 1: Clone or Download
```bash
git clone <repository-url>
cd dictionary-management-system
```

### Step 2: Prepare Dataset
Create a `Dictionary.txt` file in the same directory with the format:
```
word1    meaning1
word2    meaning2
word3    meaning3
```

**Example `Dictionary.txt`:**
```
apple    a round fruit with red or green skin
book     a set of written pages bound together
computer electronic device for processing data
dog      a domesticated carnivorous mammal
elephant large mammal with trunk and tusks
```

### Step 3: Compile
```bash
# Using GCC/MinGW
g++ dictionary.cpp -o dictionary.exe

# Or compile with specific C++ version
g++ -std=c++11 dictionary.cpp -o dictionary.exe
```

### Step 4: Run
```bash
# Windows
dictionary.exe

# Or if using .out format
./dictionary
```

##  Usage

### Initial Setup
1. Ensure `Dictionary.txt` exists in the project directory
2. The file should contain words and meanings separated by spaces
3. Each entry should be on a new line

### Login
```
Default Credentials:
Username: 1234
Password: abc
```

### Main Menu Navigation

#### **Menu 1: Primary Options**
```
1. Insert a word     - Add new word to dictionary
2. Search for a word - Access search operations
3. Log out          - Exit the application
```

#### **Menu 2: Search Operations**
```
1. Search for a word    - Find and display meaning
2. Delete a word        - Remove word from dictionary
3. Update a word        - Modify existing meaning
4. Show suggestions     - Get word recommendations
5. Log out             - Return to main menu
```

### Example Usage Flow

**Adding a Word:**
```
Enter the word to insert: programming
Enter the meaning: creating software applications
→ Word inserted successfully.
```

**Searching a Word:**
```
Enter the word to search: programming
→ Meaning: creating software applications
```

**Getting Suggestions:**
```
Enter word: pro
→ Suggestions:
  program
  programming
  project
  promise
  property
  ...
```

**Updating a Word:**
```
Enter the word to update: programming
word found
enter new meaning of searched word:
→ writing code to create software
→ Word inserted successfully.
```

**Deleting a Word:**
```
Enter the word to delete: programming
→ Word is deleted.
```

##  File Structure

```
dictionary-management-system/
│
├── project.cpp           # Main source code
├── Dictionary.txt           # Word database (user-created)
├── LoginClass.txt          # Generated automatically (credentials)
├── README.md               # Documentation
│
└── (Generated during runtime)
    └── newDictionary.txt   # Temporary file during updates
```

### File Descriptions

**Dictionary.txt**
- Main database file
- Format: `word    meaning` (separated by spaces)
- Loaded at program startup
- Updated after insert/delete/update operations

**LoginClass.txt**
- Auto-generated on first run
- Stores login credentials
- Format: `id password email username`

##  How It Works

### 1. Hash Function
```cpp
int hashIndex(int key) {
    return key % 97;
}
```
- Converts first character to ASCII value
- Modulo 97 to get array index
- Example: 'a' (97) → index 0, 'z' (122) → index 25

### 2. Insertion Process
```
1. Check if word already exists → Prevent duplicates
2. Create new node with word and meaning
3. Calculate hash index from first character
4. Insert into sorted position in linked list
5. Update file with new data
```

### 3. Search Process
```
1. Calculate hash index from first character
2. Traverse linked list at that index
3. Compare each node's word with search term
4. Return meaning if found, else return "not found"
```

### 4. Deletion Process
```
1. Calculate hash index
2. Find node in linked list
3. Update pointers to bypass deleted node
4. Free memory
5. Update file
```

### 5. Update Process
```
1. Search for word
2. Delete old entry
3. Insert with new meaning
4. Update file
```

### 6. Suggestion Algorithm
```
1. Calculate hash index from prefix
2. Start from first word >= prefix in that chain
3. Collect next 10 words
4. Return as string
```

## ⏱️ Algorithm Complexity

| Operation | Average Case | Worst Case | Space Complexity |
|-----------|-------------|------------|------------------|
| Insert    | O(1)        | O(n)       | O(1)            |
| Search    | O(1)        | O(n)       | O(1)            |
| Delete    | O(1)        | O(n)       | O(1)            |
| Update    | O(1)        | O(n)       | O(1)            |
| Suggestions| O(10)      | O(n)       | O(10)           |
| Load File | O(n)        | O(n)       | O(n)            |

**Note**: Worst case occurs when all words hash to same index (rare with good distribution)

##  Login Credentials

**Default Admin Access:**
- **ID**: `1234`
- **Password**: `abc`


**Security Features:**
- Maximum 5 login attempts
- Account lockout after failed attempts
- Credentials stored in `LoginClass.txt`

##  Sample Dataset

Create `Dictionary.txt` with entries like:

```
abandon    give up completely
ability    capacity to do something
abstract   existing in thought or as an idea
achieve    successfully reach a goal
acquire    buy or obtain an asset
adaptive   able to adjust to new conditions
advance    move forward in position
advocate   publicly recommend or support
aesthetic  concerned with beauty
allocate   distribute resources for purpose
analyze    examine methodically and in detail
ancient    belonging to the very distant past
annual     occurring once every year
apparent   clearly visible or understood
approach   come near or nearer to something
```

**Tips for Dataset:**
- Use lowercase for consistency
- Keep meanings concise (1-2 sentences)
- Separate word and meaning with spaces/tabs
- One entry per line
- Include diverse words starting with different letters

## 🔧 Technical Details

### Class Structure

**`login` Class**
```cpp
- id: string
- user_password: string
- user_name: string
- user_email: string
+ login(): constructor
+ ~login(): destructor
+ check(id, pass): bool
```

**`Dictionary` Class**
```cpp
- arr[97]: node* array
+ Dictionary(): constructor
+ createNode(word, meaning): node*
+ hashIndex(key): int
+ insertion(word, meaning): void
+ insert(word, meaning): void
+ search(word): bool
+ deletion(word): bool
+ updateword(word): void
+ updateFile(): void
+ loadDictionary(): void
+ meaning(word): string
+ suggestion(word): string
```

**`node` Structure**
```cpp
- word: string
- meaning: string
- next: node*
```

### Key Algorithms

**Sorted Insertion in Linked List:**
```cpp
if (arr[i] == NULL || arr[i]->word >= ptr->word) {
    // Insert at beginning
    ptr->next = arr[i];
    arr[i] = ptr;
} else {
    // Find correct position
    while (newOne->next != NULL && newOne->next->word < ptr->word) {
        newOne = newOne->next;
    }
    // Insert in middle/end
    ptr->next = newOne->next;
    newOne->next = ptr;
}
```

**File Update Strategy:**
```cpp
1. Open input file (Dictionary.txt)
2. Create temporary output file (newDictionary.txt)
3. Traverse entire hash table
4. Write all entries to temporary file
5. Close both files
6. Delete original file
7. Rename temporary file to original name
```

---

*Happy Learning! 📚*
