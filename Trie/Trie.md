* Amazing for **PREFIX SEARCH** and **AUTO COMPLETE** and **SPELL CHECKERS**
* **O(L)** at worst case for search
* Every node has a hashmap or an array of pointers
	* Each index represents a character and a flag to indicate if any string ends with that node
	* Flag can be a bool, if its already filled, just move to that node instead of setting it

| Operation | Time Complexity | Auxiliary Space |        |      |      |     |          |      |      |     |     |     |     |     |     |     |     |     |     |
| --------- | --------------- | --------------- | ------ | ---- | ---- | --- | -------- | ---- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Insertion | O(n)            | O(n*m)          | Search | O(n) | O(1) |     | Deletion | O(n) | O(1) |     |     |     |     |     |     |     |     |     |     |
## How-To
1. Create a root node with the help of TrieNode() constructor.
2. Store a collection of strings that we have to insert in the trie in a vector of strings say, arr.
3. Inserting all strings in Trie with the help of the insertkey() function,
4. Search strings from searchQueryStrings with the help of search_key() function.
5. Delete the strings present in the deleteQueryStrings with the help of delete_key.
```csharp
public class TrieNode
{
	public TrieNode[] children; // use hashmap if not just 26 characters
	public int wordCount;
	public TrieNode()
	{
		this.children = new TrieNode[26];
		// This will keep track of number of strings that
		// are stored in the Trie from root node to any Trie
		// node.
		this.wordCount = 0;
	}
}

```

# Insertion

```csharp
static void insert(TrieNode root, string key)
{
	TrieNode currentNode = root;

	for (int i = 0; i < key.Length; i++) {
		int index = key[i] - 'a';
		if (currentNode.childNode[index] == null) {
currentNode.childNode[index] = new TrieNode();
		}
		currentNode = currentNode.childNode[index];
	}
	currentNode.wordCount++;
}

```

# Search

```csharp
public bool isPrefixExist(TrieNode root, string key)
{
	TrieNode currentNode = root;
	foreach (char c in key)
	{
		if (currentNode.childNode == null)
		{
			return false;
		}
		currentNode = currentNode.childNode;
	}
	return true;
}
```