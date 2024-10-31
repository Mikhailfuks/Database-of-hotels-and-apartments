import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class HotelApartmentDatabase {

    private List<Hotel> hotels = new ArrayList<>();
    private List<Apartment> apartments = new ArrayList<>();

    public static void main(String[] args) {
        HotelApartmentDatabase database = new HotelApartmentDatabase();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nHotel and Apartment Database Menu:");
            System.out.println("1. Add Hotel");
            System.out.println("2. Add Apartment");
            System.out.println("3. Search for Accommodation");
            System.out.println("4. Display All Hotels");
            System.out.println("5. Display All Apartments");
            System.out.println("6. Exit");

            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline character

            switch (choice) {
                case 1:
                    database.addHotel(scanner);
                    break;
                case 2:
                    database.addApartment(scanner);
                    break;
                case 3:
                    database.searchAccommodation(scanner);
                    break;
                case 4:
                    database.displayHotels();
                    break;
                case 5:
                    database.displayApartments();
                    break;
                case 6:
                    System.out.println("Exiting program.");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }

    // Add a new hotel to the database
    public void addHotel(Scanner scanner) {
        System.out.print("Enter hotel name: ");
        String name = scanner.nextLine();
        System.out.print("Enter hotel address: ");
        String address = scanner.nextLine();
        System.out.print("Enter hotel star rating (1-5): ");
        int starRating = scanner.nextInt();
        scanner.nextLine(); // Consume newline character
        System.out.print("Enter hotel price per night: ");
        double pricePerNight = scanner.nextDouble();
        scanner.nextLine(); // Consume newline character

        hotels.add(new Hotel(name, address, starRating, pricePerNight));
        System.out.println("Hotel added successfully.");
    }

    // Add a new apartment to the database
    public void addApartment(Scanner scanner) {
        System.out.print("Enter apartment name: ");
        String name = scanner.nextLine();
        System.out.print("Enter apartment address: ");
        String address = scanner.nextLine();
        System.out.print("Enter apartment size (in square meters): ");
        int size = scanner.nextInt();
        scanner.nextLine(); // Consume newline character
        System.out.print("Enter apartment price per night: ");
        double pricePerNight = scanner.nextDouble();
        scanner.nextLine(); // Consume newline character

        apartments.add(new Apartment(name, address, size, pricePerNight));
        System.out.println("Apartment added successfully.");
    }

    // Search for accommodation based on criteria
    public void searchAccommodation(Scanner scanner) {
        System.out.println("\nSearch Criteria:");
        System.out.println("1. Search by name");
        System.out.println("2. Search by address");
        System.out.println("3. Search by price range");

        System.out.print("Enter your choice: ");
        int choice = scanner.nextInt();
        scanner.nextLine(); // Consume newline character

        switch (choice) {
            case 1:
                System.out.print("Enter accommodation name: ");
                String name = scanner.nextLine();
                searchByName(name);
                break;
            case 2:
                System.out.print("Enter accommodation address: ");
                String address = scanner.nextLine();
                searchByAddress(address);
                break;
            case 3:
                System.out.print("Enter minimum price per night: ");
                double minPrice = scanner.nextDouble();
                scanner.nextLine(); // Consume newline character
                System.out.print("Enter maximum price per night: ");
                double maxPrice = scanner.nextDouble();
                scanner.nextLine(); // Consume newline character
                searchByPriceRange(minPrice, maxPrice);
                break;
            default:
                System.out.println("Invalid choice. Please try again.");
        }
    }

    // Search for accommodation by name
    public void searchByName(String name) {
        boolean found = false;
        for (Hotel hotel : hotels) {
            if (hotel.getName().equalsIgnoreCase(name)) {
                System.out.println(hotel.toString());
                found = true;
            }
        }
        for (Apartment apartment : apartments) {
            if (apartment.getName().equalsIgnoreCase(name)) {
                System.out.println(apartment.toString());
                found = true;
            }
        }
        if (!found) {
            System.out.println("Accommodation not found.");
        }
    }

    // Search for accommodation by address
    public void searchByAddress(String address) {
        boolean found = false;
        for (Hotel hotel : hotels) {
            if (hotel.getAddress().equalsIgnoreCase(address)) {
                System.out.println(hotel.toString());
                found = true;
            }
        }
        for (Apartment apartment : apartments) {
            if (apartment.getAddress().equalsIgnoreCase(address)) {
                System.out.println(apartment.toString());
                found = true;
            }
        }
        if (!found) {
            System.out.println("Accommodation not found.");
        }
    }

    // Search for accommodation by price range
    public void searchByPriceRange(double minPrice, double maxPrice) {
        boolean found = false;
        for (Hotel hotel : hotels) {
            if (hotel.getPricePerNight() >= minPrice && hotel.getPricePerNight() <= maxPrice) {
                System.out.println(hotel.toString());
                found = true;
            }
        }
        for (Apartment apartment : apartments) {
            if (apartment.getPricePerNight() >= minPrice && apartment.getPricePerNight() <= maxPrice) {
                System.out.println(apartment.toString());
                found = true;
            }
        }
        if (!found) {
            System.out.println("No accommodation found within the specified price range.");
        }
    }

    // Display all hotels in the database
    public void displayHotels() {
        if (hotels.isEmpty()) {
            System.out.println("No hotels found.");
            return;
        }
        System.out.println("\nHotels:");
        for (Hotel hotel : hotels) {
            System.out.println(hotel.toString());
        }
    }

    // Display all apartments in the database
    public void displayApartments() {
        if (apartments.isEmpty()) {
            System.out.println("No apartments found.");
            return;
        }
        System.out.println("\nApartments:");
        for (Apartment apartment : apartments) {
            System.out.println(apartment.toString());
        }
    }
}

// Hotel class
class Hotel {
    private String name;
    private String address;
    private int starRating;
    private double pricePerNight;

    public Hotel(String name, String address, int starRating, double pricePerNight) {
        this.name = name;
        this.address = address;
        this.starRating = starRating;
        this.pricePerNight = pricePerNight;
    }

    public String getName() {
        return name;
    }

    public String getAddress() {
        return address;
    }

    public int getStarRating() {
        return starRating;
    }

    public double getPricePerNight() {
        return pricePerNight;
    }

    @Override
    public String toString() {
        return "Hotel: " + name + "\nAddress: " + address + "\nStar Rating: " + starRating + "\nPrice per night: " + pricePerNight;
    }
}

// Apartment class
class Apartment {
    private String name;
    private String address;
    private int size;
    private double pricePerNight;

    public Apartment(String name, String address, int size, double pricePerNight) {
        this.name = name;
        this.address = address;
        this.size = size;
        this.pricePerNight = pricePerNight;
    }

    public String getName() {
        return name;
    }

    public String getAddress() {
        return address;
    }

    public int getSize() {
        return size;
    }

    public double getPricePerNight() {
        return pricePerNight;
    }

    @Override
    public String toString() {
        return "Apartment: " + name + "\nAddress: " + address + "\nSize: " + size + " sq m\nPrice per night: " + pricePerNight;
    }
}
