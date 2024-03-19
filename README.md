# 3FramesTask
# Problem-1: Storing Versions and Files Efficiently
Approach:

Delta Storage Technique: Store the base version of the file along with subsequent deltas. Each delta represents the changes made from the previous version.
File Structure Design: Use a structured format to store the base version and deltas in a single file. This structure could include metadata for version information and pointers to the delta sections.
Version Generation Methods: Write methods to generate any version by applying the deltas to the base version.
Implementation Steps:

Define a file format specifying how the base version and deltas will be stored within a single file.
Implement methods to read and parse this file format, extracting the base version and delta information.
Develop algorithms to apply the deltas to reconstruct any version of the file.
# Problem-2: Word Count Application with Memory Constraints
Approach:

Data Parsing: Read the large text file in chunks, processing a portion at a time to keep RAM usage within limits.
Word Counting: Maintain a dictionary where words are keys and their counts are values. Increment counts as words are encountered in the text.
Sorting: Once all words are counted, sort the dictionary based on word counts.
Fuzzy Search: Implement a fuzzy search algorithm, such as Levenshtein distance, to handle spelling variations.
Implementation Steps:

Read the text file in manageable chunks, processing each chunk to extract words and update the word count dictionary.
Sort the dictionary by word counts to get the most frequent words.
Implement fuzzy search functionality to handle spelling variations.
# Problem-3: Product Configuration with Efficient Search
Approach:

Product Storage: Organize products into categories and create data structures to store product details efficiently.
Product Search: Implement search algorithms to quickly locate products based on various parameters like name, category, price, etc.
In-Memory Database: Develop an in-memory storage system to hold product data, providing fast access and retrieval.
Textual Search: Implement text indexing and search algorithms to enable efficient searching of product descriptions and attributes.
Implementation Steps:

Define data structures to represent products and categories, considering attributes like name, description, price, etc.
Implement algorithms for adding, updating, and querying products and categories.
Develop search methods to quickly locate products based on different criteria.
Implement text indexing and search algorithms to enable efficient textual search capabilities.



# Problem-2: Word Count Application with Memory Constraints

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;
import java.util.TreeMap;

public class WordCount {
    public static Map<String, Integer> countWords(String filename) {
        Map<String, Integer> wordCounts = new HashMap<>();
        try (BufferedReader br = new BufferedReader(new FileReader(filename))) {
            String line;
            while ((line = br.readLine()) != null) {
                String[] words = line.split("\\s+");
                for (String word : words) {
                    // Remove punctuation and convert to lowercase
                    word = word.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
                    wordCounts.put(word, wordCounts.getOrDefault(word, 0) + 1);
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        Map<String, Integer> sortedWordCounts = new TreeMap<>((a, b) -> wordCounts.get(b).compareTo(wordCounts.get(a)));
        sortedWordCounts.putAll(wordCounts);
        return sortedWordCounts;
    }

    public static void main(String[] args) {
        Map<String, Integer> wordCounts = countWords("large_text_file.txt");
        for (Map.Entry<String, Integer> entry : wordCounts.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}


# Problem-3: Product Configuration with Efficient Search

import java.util.ArrayList;
import java.util.List;

class Product {
    private String name;
    private String category;
    private String description;
    private double price;
}

class ProductDatabase {
    private List<Product> products;

    public ProductDatabase() {
        this.products = new ArrayList<>();
    }

    public void addProduct(Product product) {
        products.add(product);
    }

    public List<Product> searchByName(String keyword) {
        List<Product> result = new ArrayList<>();
        for (Product product : products) {
            if (product.getName().toLowerCase().contains(keyword.toLowerCase())) {
                result.add(product);
            }
        }
        return result;
    }

    public List<Product> searchByCategory(String category) {
        List<Product> result = new ArrayList<>();
        for (Product product : products) {
            if (product.getCategory().equalsIgnoreCase(category)) {
                result.add(product);
            }
        }
        return result;
    }
}


