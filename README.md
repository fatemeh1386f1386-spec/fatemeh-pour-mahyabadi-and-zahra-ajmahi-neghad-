# fatemeh-pour-mahyabadi-and-zahra-ahmadi-neghad-
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

/* run this program using the console pauser or add your own getch, system("pause") or input loop */

int exist = 0, j = 0, next_account_ID = 1000, num_account = 0;
double a[200];
double balance = 0.0;
char pin[5] = "1234";
char newpin[5], pin2[5], pin3[5];
char name[100], family[100];
int attempts = 0;
int check_pin() {
    while (attempts < 3) {
        printf("Enter PIN: ");
        scanf("%s", pin2);
        if (strcmp(pin, pin2) == 0) {
            return 1;
        } else {
            attempts++;
            printf("Incorrect PIN. Attempts left: %d\n", 3 - attempts);
        }
    }
    return 0;
}

int showmenu() {
    int choice = 0;
    printf("main menu\n");
    printf("1.create account\n");
    printf("2.deposit\n");
    printf("3.withdraw\n");
    printf("4.check balance\n");
    printf("5.exchange pin\n"); 
    printf("6.exit\n");
    printf("enter num of menu:");
    scanf("%d", &choice);
    return choice;
}

void createaccount() {
    int active = 0;
    if (exist == 0) {
        printf("name:");
        scanf("%s", name); 
        printf("family:");
        scanf("%s", family);
        printf("enter balance:");
        scanf("%lf", &balance);
        exist = 1;
    }
    if (balance < 0) {
        printf("Balance cannot be negative.\n");
        return;
    }
    if (active == 0) {
        active = 1;
        printf("Account is now active.\n");
    }
    
    num_account++;
    next_account_ID++;
    printf("Account ID: %d\n", next_account_ID);
    a[j] = balance;
    j = (j + 1) % 10;
}

void Deposit() {
    double deposit = 0;
    if (exist == 0) {
        printf("No account exists.\n");
        return;
    }
    printf("Deposit: ");
    scanf("%lf", &deposit);
    if (deposit > 0) {
        balance += deposit;
        printf("balance: %lf\n", balance);
        a[j] = deposit;
        j = (j + 1) % 10;
    } else {
        printf("Deposit amount must be positive.\n");
    }
}

void Withdraw() {
    double withdraw = 0;
    if (exist == 0) {
        printf("No account exists. Please create an account first.\n");
        return;
    }
    printf("Withdraw : ");
    scanf("%lf", &withdraw);
    if (withdraw > 0 && withdraw <= balance) {
        balance -= withdraw;
        printf("balance: %lf\n", balance);
        a[j] = -withdraw;
        j = (j + 1) % 10;
    } else {
        printf("Invalid withdrawal amount .\n");
    }
}

void checkbalance() {
    int newID, active = 1; 
    printf("enter ID:");
    scanf("%d", &newID);
    if (newID == next_account_ID && active == 1) {
        printf("name: %s\n", name); 
        printf("family: %s\n", family);
        printf("balance: %lf\n", balance);
    } else {
        printf("Account inactive.\n");
    }
}

void changepin() {
    printf("Enter PIN: ");
    scanf("%s", pin3);
    if (strcmp(pin, pin3) == 0) {
        printf("New PIN: ");
        scanf("%s", newpin);
        strcpy(pin, newpin);
        printf("PIN changed successfully.\n");
    } else {
        printf("Incorrect  PIN.\n");
    }
}

int main(int argc, char *argv[]) {
    int choice;
    if (check_pin() == 0) {
        printf("Too many incorrect attempts. Exiting.\n");
        return 1;
    }

    while (1) {
        choice = showmenu();
        switch (choice) {
            case 1:
                createaccount();
                break;
            case 2:
                Deposit();
                break;
            case 3:
                Withdraw();
                break;
            case 4:
                checkbalance();
                break;
            case 5:
                changepin();
                break;
            case 6:
                printf("finish");
                return 0;
            
        }
    }
    return 0;
}
