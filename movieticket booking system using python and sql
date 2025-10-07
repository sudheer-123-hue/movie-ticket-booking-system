# movie-ticket-booking-system
import mysql.connector
con = mysql.connector.connect(
    host="localhost",
    user="root",
    password="Sudheer@123", 
    database="movie_db"
)
cursor = con.cursor()


def add_movie():
    name = input("Enter movie name: ")
    genre = input("Enter movie genre: ")
    price = float(input("Enter ticket price: "))
    cursor.execute("INSERT INTO movies (name, genre, price) VALUES (%s, %s, %s)", (name, genre, price))
    con.commit()
    print("✅ Movie added successfully!")

def view_movies():
    cursor.execute("SELECT * FROM movies")
    movies = cursor.fetchall()
    print("\n--- Available Movies ---")
    for m in movies:
        print(f"ID: {m[0]} | Name: {m[1]} | Genre: {m[2]} | Price: ₹{m[3]}")

def book_ticket():
    view_movies()
    movie_id = int(input("\nEnter Movie ID to book: "))
    customer_name = input("Enter your name: ")
    seats = int(input("Enter number of seats: "))

    cursor.execute("SELECT price FROM movies WHERE movie_id=%s", (movie_id,))
    price = cursor.fetchone()

    if price:
        total = price[0] * seats
        cursor.execute("INSERT INTO bookings (movie_id, customer_name, seats, total) VALUES (%s, %s, %s, %s)",
                       (movie_id, customer_name, seats, total))
        con.commit()
        print(f" Booking successful! Total Amount: ₹{total}")
    else:
        print(" Invalid movie ID")

def view_bookings():
    cursor.execute("SELECT b.booking_id, m.name, b.customer_name, b.seats, b.total FROM bookings b JOIN movies m ON b.movie_id = m.movie_id")
    bookings = cursor.fetchall()
    print("\n--- All Bookings ---")
    for b in bookings:
        print(f"Booking ID: {b[0]} | Movie: {b[1]} | Customer: {b[2]} | Seats: {b[3]} | Total: ₹{b[4]}")

while True:
    print("\n===== MOVIE TICKET BOOKING SYSTEM =====")
    print("1. Add Movie (Admin)")
    print("2. View Movies")
    print("3. Book Ticket")
    print("4. View All Bookings")
    print("5. Exit")

    choice = input("Enter your choice: ")

    if choice == '1':
        add_movie()
    elif choice == '2':
        view_movies()
    elif choice == '3':
        book_ticket()
    elif choice == '4':
        view_bookings()
    elif choice == '5':
        print("Exiting... Goodbye!")
        break
    else:
        print("Invalid choice. Try again!")
