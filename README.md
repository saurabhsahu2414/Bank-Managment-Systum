# Bank-Managment-Systum
This Project based on the simple Debited and Credidet cash on the bank account
Code
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

struct bank {
    char name[100];
    char add[100];
    long long int adhar_no;
    long long int mob_no;
    char account_type;
    int balance;
};

void open_account(struct bank *acc) {
    printf("Enter your full name: ");
    getchar(); // Consume newline character from previous input
    fgets(acc->name, sizeof(acc->name), stdin);
    acc->name[strlen(acc->name) - 1] = '\0'; // Remove the newline character
    
    printf("Enter your full address: ");
    fgets(acc->add, sizeof(acc->add), stdin);
    acc->add[strlen(acc->add) - 1] = '\0'; // Remove the newline character

    printf("Enter your 16-digit Adhar number: ");
    scanf("%lld", &acc->adhar_no);

    printf("Enter your mobile number: ");
    scanf("%lld", &acc->mob_no);

    printf("What type of account do you want to open (s for saving, c for current): ");
    getchar(); // Consume newline character from previous input
    acc->account_type = getchar();

    while (acc->account_type != 's' && acc->account_type != 'c') {
        printf("Please enter 's' for saving or 'c' for current: ");
        getchar(); // Consume newline character from previous input
        acc->account_type = getchar();
    }

    printf("Enter initial deposit amount: ");
    scanf("%d", &acc->balance);

    while (acc->balance < 0) {
        printf("Please enter a valid initial deposit amount: ");
        scanf("%d", &acc->balance);
    }

    printf("Your account has been created.\n");
}

void deposit_money(struct bank *acc) {
    int amount;
    printf("Enter the amount to deposit: ");
    scanf("%d", &amount);

    acc->balance += amount;

    printf("Total balance is: %d $\n", acc->balance);
}

void withdraw_money(struct bank *acc) {
    int amount;
    printf("Enter the amount to withdraw: ");
    scanf("%d", &amount);

    if (amount > acc->balance) {
        printf("Insufficient balance\n");
    } else {
        acc->balance -= amount;
        printf("Withdrawal successful. Your total balance after deduction: %d $\n", acc->balance);
    }
}

void display_account(const struct bank *acc) {
    printf("Your full name: %s\n", acc->name);
    printf("Your full address: %s\n", acc->add);
    printf("Your Adhar number: %lld\n", acc->adhar_no);
    printf("Your mobile number: %lld\n", acc->mob_no);

    if (acc->account_type == 's') {
        printf("Type of account: Saving\n");
    } else if (acc->account_type == 'c') {
        printf("Type of account: Current\n");
    }

    printf("Total balance: %d $\n", acc->balance);
}

int main() {
    int choice;
    char option;
    struct bank acc;
    int account_created = 0;

    do {
        printf("\n1) Open Account\n");
        printf("2) Deposit Money\n");
        printf("3) Withdraw Money\n");
        printf("4) Display Account Details\n");
        printf("5) Exit\n");
        printf("Select an option: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("1) Open Account\n");
                open_account(&acc);
                account_created = 1;
                break;
            case 2:
                printf("2) Deposit Money\n");
                if (account_created) {
                    deposit_money(&acc);
                } else {
                    printf("You haven't created an account yet.\n");
                }
                break;
            case 3:
                printf("3) Withdraw Money\n");
                if (account_created) {
                    withdraw_money(&acc);
                } else {
                    printf("You haven't created an account yet.\n");
                }
                break;
            case 4:
                printf("4) Display Account Details\n");
                if (account_created) {
                    display_account(&acc);
                } else {
                    printf("You haven't created an account yet.\n");
                }
                break;
            case 5:
                printf("Exiting...\n");
                exit(0);
            default:
                printf("Invalid option. Please try again.\n");
        }

        printf("\nDo you want to select the next option? (y/n): ");
        scanf(" %c", &option);

        if (option == 'n' || option == 'N') {
            exit(0);
        }
    } while (option == 'y' || option == 'Y');

    return 0;
}
