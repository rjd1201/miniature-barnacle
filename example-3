#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define ALPHABET_SIZE 26

// Trie düğüm yapısı
struct TrieNode {
    struct TrieNode *children[ALPHABET_SIZE];
    int isEndOfWord;
};

// Yeni Trie düğümü oluşturur
struct TrieNode* getNode(void) {
    struct TrieNode *pNode = (struct TrieNode *)malloc(sizeof(struct TrieNode));
    pNode->isEndOfWord = 0;

    for (int i = 0; i < ALPHABET_SIZE; i++) {
        pNode->children[i] = NULL;
    }

    return pNode;
}

// Trie'ye kelime ekler
void insert(struct TrieNode *root, const char *key) {
    struct TrieNode *pCrawl = root;

    for (int level = 0; key[level] != '\0'; level++) {
        int index = key[level] - 'a';
        if (!pCrawl->children[index]) {
            pCrawl->children[index] = getNode();
        }
        pCrawl = pCrawl->children[index];
    }

    pCrawl->isEndOfWord = 1;
}

// Trie içinde kelime arar
int search(struct TrieNode *root, const char *key) {
    struct TrieNode *pCrawl = root;

    for (int level = 0; key[level] != '\0'; level++) {
        int index = key[level] - 'a';
        if (!pCrawl->children[index]) {
            return 0;
        }
        pCrawl = pCrawl->children[index];
    }

    return (pCrawl != NULL && pCrawl->isEndOfWord);
}

// Trie içindeki düğümleri serbest bırakır
void freeTrie(struct TrieNode *root) {
    for (int i = 0; i < ALPHABET_SIZE; i++) {
        if (root->children[i]) {
            freeTrie(root->children[i]);
        }
    }
    free(root);
}

// Örnek kullanımı
int main() {
    // Trie'ye eklenecek kelimeler
    char keys[][8] = {"the", "a", "there", "answer", "any", "by", "bye", "their"};
    int n = sizeof(keys) / sizeof(keys[0]);

    struct TrieNode *root = getNode();

    // Kelimeleri Trie'ye ekle
    for (int i = 0; i < n; i++) {
        insert(root, keys[i]);
    }

    // Arama işlemleri
    printf("%s --- %s\n", "the", search(root, "the") ? "Bulundu" : "Bulunamadı");
    printf("%s --- %s\n", "these", search(root, "these") ? "Bulundu" : "Bulunamadı");
    printf("%s --- %s\n", "their", search(root, "their") ? "Bulundu" : "Bulunamadı");
    printf("%s --- %s\n", "thaw", search(root, "thaw") ? "Bulundu" : "Bulunamadı");

    // Trie düğümlerini serbest bırak
    freeTrie(root);

    return 0;
}
