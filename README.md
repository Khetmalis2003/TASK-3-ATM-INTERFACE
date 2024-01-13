# TASK-3-ATM-INTERFACE

import java.util.Scanner;

class UserAcc {
    private double balance;

    public UserAcc(double initialBalance) {
        this.balance = initialBalance;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposit successful. New balance: " + balance);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawal successful. Remaining balance: " + balance);
        } else {
            System.out.println("Invalid withdrawal amount or insufficient funds.");
        }
    }
}

class ATM {
    private UserAcc user;

    public ATM(UserAcc user) {
        this.user = user;
    }

    public void displayOptions() {
        System.out.println("Options:");
        System.out.println("1. Withdraw");
        System.out.println("2. Deposit");
        System.out.println("3. Check Balance");
        System.out.println("0. Exit");
    }

    public void processTransaction(int option, Scanner sc) {
        if (option == 1) {
            System.out.print("Enter withdrawal amount: ");
            user.withdraw(sc.nextDouble());
        } else if (option == 2) {
            System.out.print("Enter deposit amount: ");
            user.deposit(sc.nextDouble());
        } else if (option == 3) {
            System.out.println("Current balance: " + user.getBalance());
        } else {
            System.out.println("Exiting ATM. Thank you!");
            System.exit(0);
        }
    }
}

class Main {
    public static void main(String[] args) {
        UserAcc user = new UserAcc(1000.0);
        ATM atm = new ATM(user);

        Scanner sc = new Scanner(System.in);

        while (true) {
            System.out.println("\nATM Options:");
            atm.displayOptions();
            System.out.print("Choose an option (1-3, or 0 to exit): ");
            int option = sc.nextInt();

            atm.processTransaction(option, sc);
        }
    }
}
