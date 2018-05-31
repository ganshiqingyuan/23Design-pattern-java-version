##迭代器模式
     

对一个集合进行迭代访问，以固定的方式，比如.next()，当修改疏忽存储类型时比如原先是用的数组，现在变为对象集合，你仍然可以使用

    while(it.next){
    ...
    }
这种方式进行访问，只需要修改构造迭代器的方式即可，大大复用了代码

java实现



###Aggregate  接口，，被遍历的集合接口

    public interface Aggregate {
    public abstract Iterator iterator();
    }

###Iterator   接口，，迭代器接口，提供迭代器方法

    public interface Iterator {
    public abstract boolean hasNext();
    public abstract Object next();
    }

####Book   类，，表示书

    public class Book {
    private String name;
    public Book(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
    }  
####BookShelf   类，，表示书架  实现 集合接口

    public class BookShelf implements Aggregate {
    private Book[] books;
    private int last = 0;
    public BookShelf(int maxsize) {
        this.books = new Book[maxsize];
    }
    public Book getBookAt(int index) {
        return books[index];
    }
    public void appendBook(Book book) {
        this.books[last] = book;
        last++;
    }
    public int getLength() {
        return last;
    }
    public Iterator iterator() {
        return new BookShelfIterator(this);
    }
    }
####BookShelfIterator   类，，实现迭代器接口

    public class BookShelfIterator implements Iterator {
    private BookShelf bookShelf;
    private int index;
    public BookShelfIterator(BookShelf bookShelf) {
        this.bookShelf = bookShelf;
        this.index = 0;
    }
    public boolean hasNext() {
        if (index < bookShelf.getLength()) {
            return true;
        } else {
            return false;
        }
    }
    public Object next() {
        Book book = bookShelf.getBookAt(index);
        index++;
        return book;
    }
    }





####入口代码

    import java.util.*;

    public class Main {
    public static void main(String[] args) {
        BookShelf bookShelf = new BookShelf(4);
        bookShelf.appendBook(new Book("Around the World in 80 Days"));
        bookShelf.appendBook(new Book("Bible"));
        bookShelf.appendBook(new Book("Cinderella"));
        bookShelf.appendBook(new Book("Daddy-Long-Legs"));
        Iterator it = bookShelf.iterator();
        while (it.hasNext()) {
            Book book = (Book)it.next();
            System.out.println(book.getName());
        }
    }
    }

    

