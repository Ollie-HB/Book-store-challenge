1. Design and create the Table

Table: books

Columns:
id | title | author_name

2. Create Test SQL seeds

TRUNCATE TABLE books RESTART IDENTITY;

INSERT INTO books (title, author_name) VALUES ('Neuromancer', 'William Gibson');
INSERT INTO students (title, author_name) VALUES ('1984', 'George Orwell');

psql -h 127.0.0.1 book_store_test < spec/book_seeds.sql

3. Define the class names

class Book
end

class BookRepository
end

4. Implement the Model class

class Book
  attr_accessor :id, :title, :author_name
end

5. Define the Repository Class interface

class BookRepository

  # Selecting all records
  # No arguments

  def all
    # Executes the SQL query:
    # SELECT id, title, author_name FROM books;

    # Returns an array of Book objects.
  end

6. Write Test Examples


# EXAMPLES

# 1 Get all students

repo = BookRepository.new

books = repo.all

books.length # =>  2
books.first.id # => '1'
books.first.title # => 'Neuromancer'
books.first.author_name # => 'William Gibson'

RSpec.describe BookRepository do
    it "returns the list of books"

        repo = BookRepository.new

        books = repo.all

        expect(books.length).to eq 2
        expect(books.first.id).to eq '1'
        expect(books.first.title).to eq 'Neuromancer'
        expect(books.first.author_name).to eq 'William Gibson'
    end
end

7. Reload the SQL seeds before each test run


def reset_books_table
  seed_sql = File.read('spec/book_seeds.sql')
  connection = PG.connect({ host: '127.0.0.1', dbname: 'book_store_test' })
  connection.exec(seed_sql)
end

describe BookRepository do
  before(:each) do 
    reset_books_table
  end

  # (your tests will go here).
end
8. Test-drive and implement the Repository class behaviour
After each test you write, follow the test-driving process of red, green, refactor to implement the behaviour.