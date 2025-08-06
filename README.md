import java.util.*;

class Product {
    String name;
    int quantity;
    double price;

    Product(String name, int quantity, double price) {
        this.name = name;
        this.quantity = quantity;
        this.price = price;
    }

    double getTotal() {
        return quantity * price;
    }
}

class Bill {
    List<Product> products = new ArrayList<>();
    double taxRate = 0.18; // 18% GST

    void addProduct(Product p) {
        products.add(p);
    }

    void generateBill() {
        double subtotal = 0;

        System.out.println("\n----- Final Bill -----");
        System.out.printf("%-15s %-10s %-10s %-10s\n", "Product", "Qty", "Price", "Total");

        for (Product p : products) {
            double total = p.getTotal();
            subtotal += total;
            System.out.printf("%-15s %-10d %-10.2f %-10.2f\n", p.name, p.quantity, p.price, total);
        }

        double tax = subtotal * taxRate;
        double grandTotal = subtotal + tax;

        System.out.println("-------------------------------");
        System.out.printf("Subtotal: %.2f\n", subtotal);
        System.out.printf("Tax (18%%): %.2f\n", tax);
        System.out.printf("Total Amount: %.2f\n", grandTotal);
    }
}

public class BillingSystem {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Bill bill = new Bill();

        System.out.println("=== Simple Billing System ===");

        while (true) {
            System.out.print("Enter product name (or 'done'): ");
            String name = sc.nextLine();
            if (name.equalsIgnoreCase("done")) break;

            System.out.print("Enter quantity: ");
            int qty = sc.nextInt();

            System.out.print("Enter price: ");
            double price = sc.nextDouble();
            sc.nextLine(); // clear buffer

            Product p = new Product(name, qty, price);
            bill.addProduct(p);
        }

        bill.generateBill();
        sc.close();
        System.out.println("[Thanks for shopping from Indikraft]");
    }
}
