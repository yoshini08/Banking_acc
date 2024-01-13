import java.util.*;

class ATM {
    private String accountHolderName;
    private int balance, accountNumber;

    public ATM(String accountHolderName, int balance) {
        this.accountHolderName = accountHolderName;
        this.balance = balance;

        Set<Integer> accountNumbers = new HashSet<>();
        Random rand = new Random();
        int max = 999999, min = 200000;

        accountNumber = rand.nextInt(max - min + 1) + min;
        while (accountNumbers.contains(accountNumber)) {
            accountNumber = rand.nextInt(max - min + 1) + min;
        }
        accountNumbers.add(accountNumber);
        System.out.println("Your account number is: " + accountNumber);
    }

    public void displayInfo() {
        System.out.println("Account Holder Name: " + this.accountHolderName);
        System.out.println("Account Number: " + accountNumber);
    }

    public void deposit(int depositAmount) {
        balance += depositAmount;
    }

    public void withdraw(int withdrawAmount) {
        if (balance >= withdrawAmount) {
            balance -= withdrawAmount;
            System.out.println("Collect your money");
        } else {
            System.out.println("Insufficient balance");
        }
    }

    public void displayBalance() {
        System.out.println("Your balance amount is " + balance);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        ArrayList<ATM> accountList = new ArrayList<>();

        LOOP: while (true) {
            System.out.println("-------BANK-------" + "\n" + "Choose..." + "\n" + "1...SignIn" + "\n" + "2...LogIn"
                    + "\n" + "3...Exit");
            int choice = in.nextInt();
            switch (choice) {
                case 1:
                    System.out.println("-----SignIn-----");
                    System.out.println("Enter your name : ");
                    in.nextLine();
                    String name = in.nextLine();

                    System.out.println("Your Account ID is: " + (1 + accountList.size()));

                    ATM newAccount = new ATM(name, 0);
                    accountList.add(newAccount);

                    break;
                case 2:
                    System.out.println("-----LogIn-----");
                    System.out.println("Enter your Account ID : ");
                    int id = in.nextInt();

                    if (id > 0 && id <= accountList.size()) {
                        accountList.get(id - 1).displayInfo();

                        loop: while (true) {
                            System.out.println(
                                    "-------ATM-------" + "\n" + "Choose... " + "1...Deposit " + "2...Withdraw "
                                            + "3...Balance " + "4...Exit");
                            int userChoice = in.nextInt();
                            switch (userChoice) {
                                case 1:
                                    System.out.println("Enter amount : ");
                                    int depositAmount = in.nextInt();
                                    accountList.get(id - 1).deposit(depositAmount);
                                    break;
                                case 2:
                                    System.out.println("Enter amount : ");
                                    int withdrawAmount = in.nextInt();
                                    accountList.get(id - 1).withdraw(withdrawAmount);
                                    break;
                                case 3:
                                    accountList.get(id - 1).displayBalance();
                                    break;
                                case 4:
                                    break loop;
                                default:
                                    System.out.println("Invalid Input");
                            }
                        }
                    } else
                        System.out.println("Account ID doesn't exist");

                    break;
                case 3:
                    System.out.println("Exiting the program. Thank you!");
                    break LOOP;
                default:
                    System.out.println("Invalid Input");
            }
        }
    }
}
