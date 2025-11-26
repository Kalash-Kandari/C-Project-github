#include <stdio.h>
#include <string.h>
char itemName[20][50];
int itemQuantity[20];
int count = 0;
void addItem(void){
    char ch;
    repeat:
    printf("\nEnter item name : ");
    fflush(stdin);
    gets(itemName[count]);
    printf("Enter item quantity : ");
    scanf("%d",&itemQuantity[count]);
    count++;
    printf("\nPress 'Y' to add more items otherwise press 'N' : ");
    fflush(stdin);
    ch = getchar();
    if (ch=='y'||ch=='Y')
    {
        goto repeat;
    }
}
void removeItem(void){
    char name[50];
    int check = 0;
    printf("Enter item name : ");
    fflush(stdin);
    gets(name);
    for (int i = 0; i < count; i++)
    {
        if (strcmp(name,itemName[i]) == 0)
        {
            for (int j = i; j < count; j++)
            {
                strcpy(itemName[j],itemName[j+1]);
                itemQuantity[j] = itemQuantity[j+1];
            }
            count--;
            printf("\nItem has been deleted\n");
            return;
            check = 1;
        }
    }
    if (check==0)
    {
        printf("\nItem name is not find\n");
    }
}
void editItem(void){
    char name[50];
    int quantity,check = 0;
    printf("Enter item name : ");
    fflush(stdin);
    gets(name);
    printf("Enter new quantity : ");
    scanf("%d",&quantity);
    for (int i = 0; i < count; i++)
    {
        if (strcmp(name,itemName[i]) == 0)
        {
            itemQuantity[i] = quantity;
            printf("\nItem quantity is updated\n");
            check = 1;
        }
    }
    if (check==0)
    {
        printf("\nItem name is not find\n");
    }
}
void showShoppingList(){
    if (count == 0)
    {
        printf("\nShopping list is empty\n");
        return;
    }
    printf("\n Item name\tItem Quantity\n\n");
    for (int i = 0; i < count; i++)
    {
        printf("%s\t\t%d\n",itemName[i],itemQuantity[i]);
    }
}
int main()
{
    int choice;
    printf("\n-: WELCOME TO THE SHOPPING LIST :-\n");
    do
    {
        printf("\nEnter 1 to add item in shopping list\n");
        printf("Enter 2 to remove item from shopping list\n");
        printf("Enter 3 to edit item of shopping list\n");
        printf("Enter 4 to show shopping list\n");
        printf("Enter 5 to exit\n");
    repeat:
        printf("Enter your choice: ");
        fflush(stdin);
        scanf("%d", &choice);
        switch (choice)
        {
        case 1:
            addItem();
            break;
        case 2:
            removeItem();
            break;
        case 3:
            editItem();
            break;
        case 4:
            showShoppingList();
            break;
        case 5:
            break;
        default:
            printf("\nInvalid choice try again\n");
            goto repeat;
        }
    } while (choice != 5);

    FILE *fptr;
    fptr = fopen("Shop.txt", "w");
    fprintf(fptr,"\n Item name\tItem Quantity\n\n");
    for (int i = 0; i < count; i++)
    {
        fprintf(fptr, "%s\t\t%d\n",itemName[i],itemQuantity[i]);
    }
    return 0;
}
