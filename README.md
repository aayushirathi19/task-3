import java.util.Scanner;

// BankAccount class without public keyword
class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }

    public boolean deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            return true;
        }
        return false;
    }

    public double getBalance() {
        return balance;
    }
}

// ATM class without public keyword
class ATM {
    private BankAccount account;
    private Scanner scanner;

    public ATM(BankAccount account) {
        this.account = account;
        this.scanner = new Scanner(System.in);
    }

    public void start() {
        int choice;
        System.out.println("🏧 Welcome to the ATM Interface!");

        do {
            showMenu();
            System.out.print("👉 Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1 -> checkBalance();
                case 2 -> deposit();
                case 3 -> withdraw();
                case 4 -> System.out.println("👋 Thank you for using ATM!");
                default -> System.out.println("❌ Invalid choice. Please try again.");
            }
        } while (choice != 4);
    }

    private void showMenu() {
        System.out.println("\n========= ATM Menu =========");
        System.out.println("1. 🧾 Check Balance");
        System.out.println("2. 💰 Deposit Money");
        System.out.println("3. 💸 Withdraw Money");
        System.out.println("4. 🚪 Exit");
        System.out.println("============================");
    }

    private void checkBalance() {
        System.out.printf("✅ Current balance: ₹%.2f\n", account.getBalance());
    }

    private void deposit() {
        System.out.print("📥 Enter amount to deposit: ₹");
        double amount = scanner.nextDouble();
        if (account.deposit(amount)) {
            System.out.printf("✅ ₹%.2f deposited successfully.\n", amount);
        } else {
            System.out.println("❌ Invalid deposit amount.");
        }
    }

    private void withdraw() {
        System.out.print("📤 Enter amount to withdraw: ₹");
        double amount = scanner.nextDouble();
        if (account.withdraw(amount)) {
            System.out.printf("✅ ₹%.2f withdrawn successfully.\n", amount);
        } else {
            System.out.println("❌ Insufficient balance or invalid amount.");
        }
    }
}

// ✅ Main public class must match file name (Main.java)
public class Main {
    public static void main(String[] args) {
        BankAccount userAccount = new BankAccount(10000.0);
        ATM atm = new ATM(userAccount);
        atm.start();
    }
}
