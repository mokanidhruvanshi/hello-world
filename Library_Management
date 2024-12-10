import java.util.*;

// Book class to store book details
class Book {
    String title;
    String author;
    String genre;
    String ISBN;
    
    public Book(String title, String author, String genre, String ISBN) {
        this.title = title;
        this.author = author;
        this.genre = genre;
        this.ISBN = ISBN;
    }
    
    @Override
    public String toString() {
        return title + " by " + author + " (Genre: " + genre + ", ISBN: " + ISBN + ")";
    }
}

// Library Management System
public class LibraryManagementSystem {
    // Lists for storing books and members
    List<Book> books = new ArrayList<>();
    List<String> members = new ArrayList<>();
    List<String> borrowHistory = new ArrayList<>(); // Stack substitute for history tracking

    // Stacks and Queues
    Stack<String> borrowingHistory = new Stack<>();
    Queue<String> reservationQueue = new LinkedList<>();

    // HashMap as a Hash Table to map ISBNs to book details
    HashMap<String, Book> bookTable = new HashMap<>();

    // Tree structure for hierarchical catalog
    static class TreeNode {
        String category;
        List<TreeNode> subcategories = new ArrayList<>();
        List<Book> books = new ArrayList<>();

        TreeNode(String category) {
            this.category = category;
        }

        void addSubcategory(TreeNode subcategory) {
            subcategories.add(subcategory);
        }
        
        void addBook(Book book) {
            books.add(book);
        }
    }

    // Simple Graph representation for book relationships
    static class Graph {
        HashMap<Book, List<Book>> adjList = new HashMap<>();

        void addBook(Book book) {
            adjList.putIfAbsent(book, new ArrayList<>());
        }

        void addEdge(Book book1, Book book2) {
            adjList.get(book1).add(book2);
            adjList.get(book2).add(book1); // Assuming bidirectional relationship
        }

        List<Book> getRelatedBooks(Book book) {
            return adjList.get(book);
        }
    }

    Graph bookGraph = new Graph();

    // Add book to system
    public void addBook(Book book) {
        books.add(book);
        bookTable.put(book.ISBN, book);
        bookGraph.addBook(book);
    }

    // Borrow a book
    public void borrowBook(String isbn) {
        Book book = bookTable.get(isbn);
        if (book != null) {
            borrowingHistory.push(book.title);
            System.out.println("Book borrowed: " + book);
        } else {
            System.out.println("Book not found!");
        }
    }

    // Return a book
    public void returnBook() {
        if (!borrowingHistory.isEmpty()) {
            String lastBorrowed = borrowingHistory.pop();
            System.out.println("Book returned: " + lastBorrowed);
        } else {
            System.out.println("No borrowed books to return!");
        }
    }

    // Add a reservation request
    public void reserveBook(String bookTitle) {
        reservationQueue.offer(bookTitle);
        System.out.println("Reservation added for: " + bookTitle);
    }

    // Get book details by ISBN
    public void getBookByISBN(String isbn) {
        Book book = bookTable.get(isbn);
        if (book != null) {
            System.out.println("Book Details: " + book);
        } else {
            System.out.println("No book found with ISBN: " + isbn);
        }
    }

    // Main method for testing
    public static void main(String[] args) {
        LibraryManagementSystem library = new LibraryManagementSystem();

        // Adding books
        Book book1 = new Book("Book One", "Author A", "Fiction", "12345");
        Book book2 = new Book("Book Two", "Author B", "Science", "67890");
        library.addBook(book1);
        library.addBook(book2);

        // Borrowing and returning
        library.borrowBook("12345");
        library.returnBook();

        // Hash Table lookup
        library.getBookByISBN("12345");

        // Reservation
        library.reserveBook("Book One");

        // Tree structure
        TreeNode fictionNode = new TreeNode("Fiction");
        fictionNode.addBook(book1);
        System.out.println("Category: " + fictionNode.category + " Books: " + fictionNode.books);

        // Graph relationships
        library.bookGraph.addEdge(book1, book2);
        System.out.println("Related Books to " + book1.title + ": " + library.bookGraph.getRelatedBooks(book1));
    }
}
