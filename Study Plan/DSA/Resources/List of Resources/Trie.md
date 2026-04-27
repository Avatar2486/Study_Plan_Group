# Trie

Priority: Medium
Status: Not started

---

# 🧠 What is a Trie?

A **Trie (pronounced "try")** is a tree-like **prefix data structure** used for efficient retrieval of strings, especially when they share common prefixes — often used in problems involving:

- **Autocomplete**
- **Dictionary matching**
- **Prefix search**
- **Spell check**
- **IP routing (binary trie)**

---

## 📦 Real-world Analogy

Think of a **Trie like a phonebook**. If you want to find names starting with "Ann", you follow:

```
Root → A → N → N

```

From there, all possible completions (Anna, Annie, Annabel) are below that node.

---

## 🔧 How a Trie Works Internally

Each Trie node typically stores:

```
class TrieNode {
  Map<Character, TrieNode> children;
  boolean isEndOfWord;
}

```

Key operations:

1. **Insert(word)** – Add a word to the trie.
2. **Search(word)** – Check if exact word exists.
3. **StartsWith(prefix)** – Check if any word starts with a prefix.

---

## 👨‍💻 Basic Implementation (JavaScript-style pseudocode)

```
class TrieNode {
  constructor() {
    this.children = {};     // Map of characters to children
    this.isEnd = false;     // End-of-word marker
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;
    for (let ch of word) {
      if (!node.children[ch]) node.children[ch] = new TrieNode();
      node = node.children[ch];
    }
    node.isEnd = true;
  }

  search(word) {
    let node = this._traverse(word);
    return !!node && node.isEnd;
  }

  startsWith(prefix) {
    return !!this._traverse(prefix);
  }

  _traverse(str) {
    let node = this.root;
    for (let ch of str) {
      if (!node.children[ch]) return null;
      node = node.children[ch];
    }
    return node;
  }
}

```

---

# 🎯 FAANG-Level Trie Questions on LeetCode (Categorized)

---

## 🟢 **Beginner / Easy**

These help you get comfortable with the Trie structure.

| Problem | Link | Tags |
| --- | --- | --- |
| 208. Implement Trie (Prefix Tree) | [🔗 Link](https://leetcode.com/problems/implement-trie-prefix-tree) | Trie, Design |
| 14. Longest Common Prefix | [🔗 Link](https://leetcode.com/problems/longest-common-prefix) | Strings, Trie optional |
| 720. Longest Word in Dictionary | [🔗 Link](https://leetcode.com/problems/longest-word-in-dictionary) | Trie, DFS |

---

## 🟡 **Intermediate / Medium**

More complex usage — may combine Trie with DFS/BFS or sorting.

| Problem | Link | Tags |
| --- | --- | --- |
| 421. Maximum XOR of Two Numbers in an Array | [🔗 Link](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array) | Trie, Bit Manipulation |
| 648. Replace Words | [🔗 Link](https://leetcode.com/problems/replace-words) | Trie, HashSet |
| 211. Design Add and Search Words Data Structure | [🔗 Link](https://leetcode.com/problems/design-add-and-search-words-data-structure) | Trie, DFS |
| 212. Word Search II | [🔗 Link](https://leetcode.com/problems/word-search-ii) | Trie, Backtracking, DFS |

---

## 🔴 **Advanced / Hard**

These appear in actual FAANG interviews. Involve optimization, clever pruning, or non-obvious Trie usage.

| Problem | Link | Tags |
| --- | --- | --- |
| 336. Palindrome Pairs | [🔗 Link](https://leetcode.com/problems/palindrome-pairs) | Trie, Palindromes, Hard |
| 1268. Search Suggestions System | [🔗 Link](https://leetcode.com/problems/search-suggestions-system) | Trie, Binary Search |
| 745. Prefix and Suffix Search | [🔗 Link](https://leetcode.com/problems/prefix-and-suffix-search) | Trie, HashMap, Design |

---

# 🧩 Practice Strategy

| Phase | What to Do | Problems |
| --- | --- | --- |
| 🔰 Learn Basic | Build Trie + insert/search/prefix | 208, 14 |
| 🔄 Apply Logic | Combine Trie with DFS/backtracking | 212, 720 |
| 🚀 Optimize | Focus on performance + hybrid logic | 421, 336, 745 |

---

# 🛠️ Tips for Interviews

- Be ready to **write your own Trie class** from scratch.
- Think about **memory vs speed trade-offs**.
- Consider **Trie size vs input word length**.

---