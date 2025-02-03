# Grocery-Store-Billing-System-
This is a simple Grocery Store Billing System written in C. It allows users to enter customer details, purchase items, and calculate the total bill with sales tax and discounts. The program supports multiple payment methods, including cash and online payment, and generates an approval number for online transactions.
# Source-code-
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define NUM_ITEMS 6

int main() {
    int prices[NUM_ITEMS] = {350, 130, 1800, 350, 250, 150};
    char *item_names[NUM_ITEMS] = {"Rice", "Sugar", "Flour", "Pulses", "Oil", "Tea"};
    float quantities[NUM_ITEMS], total_price = 0, cash_payment, online_payment, remaining_balance;
    int payment_method;
    float sales_tax_rate = 0.05, sales_tax = 0, total_with_tax = 0;
    int discount = 0;
    char customer_name[50], customer_phone[20];
    
    srand(time(NULL));
    int approval_number = rand() % 900000000 + 100000000;
    
    // Customer details input
    printf("\nCustomer Name: ");
    scanf(" %[^"]", customer_name);
    printf("Phone Number: ");
    scanf("%s", customer_phone);
    
    printf("\nShahid Store Mardan\nAddress: Bank Road\nCell No: 034081903\n");
    printf("----------------------------------------------\n");
    printf("Description        Quantity (kg)\n");
    printf("----------------------------------------------\n");
    
    for (int i = 0; i < NUM_ITEMS; i++) {
        printf("%s: ", item_names[i]);
        scanf("%f", &quantities[i]);
    }
    
    // Calculate total price
    float total_item_price[NUM_ITEMS];
    for (int i = 0; i < NUM_ITEMS; i++) {
        total_item_price[i] = prices[i] * quantities[i];
        total_price += total_item_price[i];
    }
    
    // Apply discount if eligible
    if (total_price > 10000) {
        discount = 10;
    }
    float discount_amount = (discount > 0) ? total_price * 0.10 : 0;
    
    // Apply sales tax
    sales_tax = (total_price - discount_amount) * sales_tax_rate;
    total_with_tax = (total_price - discount_amount) + sales_tax;
    
    // Display bill summary
    printf("----------------------------------------------\n");
    printf("Item Name      Price (PKR)\n");
    printf("----------------------------------------------\n");
    
    for (int i = 0; i < NUM_ITEMS; i++) {
        printf("%s:         %.2f\n", item_names[i], total_item_price[i]);
    }
    
    printf("----------------------------------------------\n");
    printf("Total Price:          %.2f\n", total_price);
    printf("Sales Tax (5%%):       %.2f\n", sales_tax);
    
    if (discount > 0) {
        printf("Discount (10%%):       %.2f\n", discount_amount);
    }
    
    printf("Final Amount:         %.2f\n", total_with_tax);
    printf("----------------------------------------------\n");
    
    // Payment process
    printf("Select Payment Method (1 for Cash, 2 for Online): ");
    scanf("%d", &payment_method);
    
    if (payment_method == 1) {
        printf("Enter Cash Payment: ");
        scanf("%f", &cash_payment);
        remaining_balance = total_with_tax - cash_payment;
    } else if (payment_method == 2) {
        printf("Enter Online Payment: ");
        scanf("%f", &online_payment);
        remaining_balance = total_with_tax - online_payment;
    } else {
        printf("Invalid payment method selected.\n");
        return 1;
    }
    
    if (remaining_balance > 0) {
        printf("Remaining Balance: %.2f\n", remaining_balance);
    } else {
        printf("Payment Complete!\n");
    }
    
    if (payment_method == 2) {
        printf("Approval Number: %d\n", approval_number);
    }
    
    printf("----------------------------------------------\n");
    printf("Customer: %s\n", customer_name);
    printf("THANK YOU FOR SHOPPING WITH US!\n");
    
    return 0;
}
