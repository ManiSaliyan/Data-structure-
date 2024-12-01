# Data-structure-

### Program 6


```c
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#define MAX 5

int front=0,rear=-1,count=0,item_deleted,element;
char cqueue[MAX];

void insert();
void delete();
void display();

void main(){
    int choice;
    while(1){

        printf("\n\nProgram to illustrate operations on CIRCULAR QUEUE of characters\n");
        printf("\n\t1.Insert an element on to CIRCULAR QUEUE\n\t2.Deletean element from CIRCULARQUEUE\n\t3.Display the status of CIRCULAR QUEUE\n\t4.Exit\n");
        printf("\nEnter your choice: ");
        scanf("%d",&choice);

        switch(choice){
            case 1:insert();
                break;
            case 2:delete();
                break;
            case 3:display();
                break;
            case 4:
                return;
        }
    }
}

void insert(){

    if(count==MAX){
        printf("CIRCULAR QUEUE is full,elements can not be inserted\n");
        return;
    }

    rear=(rear+1)%MAX;
    printf("\n Enter the element to be inserted into the CIRCULAR QUEUE\n");
    scanf("%d",&element);
    cqueue[rear]=element;
    count++;
}

void delete(){
    if(count==0){
        printf("CIRCULAR QHEUE is empty,no element to delete\n");
        return;
    }

    item_deleted=cqueue[front];
    printf("the element deleted is %d\n",item_deleted);
    front=(front+1)%MAX;
    count-=1;
}
 
void display()
{
    int i,f;
    if(count==0){
        printf("CIRCULAR QUEUE is empty , no element to display\n");
        return;
    }

    printf("CIRCULAR QUEUE contants are\n");
    for(i=0,f=front;i<count;i++){
        printf("%d\t",cqueue[f]);
        f=(f+1)%MAX;
    }
}
```


# Program 7

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct{
    char usn[11]; char
    name[20]; 
    char branch[20]; 
    int semester; 
    char phone[20];
}STUDENT;

struct node{
    char usn[11];
    char name[20];
    char branch[20];
    int semester; 
    char phone[20];
    struct node *link;
};

typedef struct node*NODE;

NODE getnode(){
    NODE x;
    x=(NODE)malloc(sizeof(struct node));
    if(x==NULL){
        printf("out of memory\n");exit(0);
    }
    return x;
}

NODE insert_front(STUDENT item,NODE first){
    NODE temp; temp=getnode();

    strcpy(temp->usn,item.usn);
    strcpy(temp->name,item.name);
    strcpy(temp->branch,item.branch);
    temp->semester=item.semester;
    strcpy(temp->phone,item.phone);

    temp->link=NULL;
    if(first==NULL) return temp;
    temp->link=first;
    return temp;
}

NODE insert_rear(STUDENT item,NODE first){
    NODE temp,cur;
    temp=getnode();
    strcpy(temp->usn,item.usn);
    strcpy(temp->name,item.name);
    strcpy(temp->branch,item.branch);
    temp->semester=item.semester;
    strcpy(temp->phone,item.phone);

    temp->link=NULL;
    if(first==NULL) return temp;
    cur=first;
    while(cur->link!=NULL){
        cur=cur->link;
    }
    cur->link=temp; return
    first;
}

NODE delete_front(NODE first){
NODE temp;

if(first==NULL){
    printf("student list is empty\n");
    return NULL;
}

temp=first;
temp=temp->link;
printf("delete student record:USN=%s\n",first->usn);
free(first);
return temp;
}

NODE delete_rear(NODE first){
    NODE cur,prev;

    if(first==NULL){
        printf("student list is empty cannot delete\n");
        return first;
    }

    if(first->link==NULL){
        printf("delete student record:USN=%s\n",first->usn);
        free(first);
        return NULL;
    }

    prev=NULL;
    cur=first;
    while(cur->link!=NULL){
        prev=cur;
        cur=cur->link;
    }
    printf("delete student record:USN=%s\n",cur->usn);free(cur);
    prev->link=NULL;
    return first;
}

void display(NODE first){
    NODE cur; int
    count=0;
    if(first==NULL){
        printf("student list is empty\n");return;
    }
    cur=first;
    while(cur!=NULL){
        printf("%s\t%s\t%s\t%d\t%s\t\n",cur->usn,cur->name,cur->branch,cur->semester,cur->phone);
        cur=cur->link; count++;
    }
    printf("number of students=%d\n",count);
}

void main(){
    NODE first;
    int choice;
    STUDENT item;
    first=NULL;

    for(;;){
        printf("1.insert_front\n2.insert_rear\n3.delete_front\n4.delete_rear\n5.display\n6.exit\n");
        printf("Enter the choice:");
        scanf("%d",&choice);

        switch(choice){
            case 1:printf("USN :");
                scanf("%s",item.usn);
                printf("name :");
                scanf("%s",item.name);
                printf("branch :");
                scanf("%s",item.branch);
                printf("semester:");
                scanf("%d",&item.semester);
                printf("phone :");
                scanf("%s",item.phone);
                first=insert_front(item,first);break;
            case 2:
                printf("USN :");
                scanf("%s",item.usn);
                printf("name :");
                scanf("%s",item.name);
                printf("branch :");
                scanf("%s",item.branch);
                printf("semester:");
                scanf("%d",&item.semester);
                printf("phone :");
                scanf("%s",item.phone);
                first=insert_rear(item,first);break;
            case 3:
                first=delete_front(first); break;
            case 4:
                first=delete_rear(first);
                break;
            case 5:
                display(first);
                break;
            default:
                exit(0);
        }
    }
}
```


# Program 8

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct{
    int ssn;
    char name[20];
    char department[20];
    char designation[20];
    float salary;
    char phone[20];
} EMPLOYEE;

struct node{
    int ssn;
    char name[20];
    char department[20];
    char designation[20];
    float salary;
    char phone[20];
    struct node *llink;
    struct node *rlink;
};

typedef struct node* NODE;

NODE getnode(){
    NODE x;
    x = ( NODE ) malloc(sizeof(struct node));
    if ( x== NULL ){
        printf("Out of memory\n");
        exit(0);
    }
    return x; /* allocation successful */
}

// Insert node at the front end
NODE insert_front(EMPLOYEE emp, NODE first){
    NODE temp;
    temp = getnode();

    temp->ssn = emp.ssn;
    strcpy(temp->name, emp.name);
    strcpy(temp->department, emp.department);
    strcpy(temp->designation, emp.designation);
    temp->salary = emp.salary;
    strcpy(temp->phone, emp.phone);
    temp->llink = temp->rlink = NULL;

    if (first == NULL) return temp;

    temp->rlink = first;
    first->llink = temp;
    return temp;
}

// Inset node at the rear end
NODE insert_rear(EMPLOYEE emp, NODE first){
    NODE temp, cur;
    temp = getnode();
    temp->ssn = emp.ssn;
    strcpy(temp->name, emp.name);
    strcpy(temp->department, emp.department);
    strcpy(temp->designation, emp.designation);
    temp->salary = emp.salary;
    strcpy(temp->phone, emp.phone);
    temp->llink = temp->rlink = NULL;
    if (first == NULL) return temp;

    cur = first;
    while (cur->rlink != NULL) cur = cur->rlink;

    cur->rlink = temp;
    temp->llink = cur;
    
    return first;
}

NODE delete_front(NODE first){
    NODE second;
    if ( first == NULL ) {
        printf("employee list is empty \n");
        return NULL;
    }

    if (first ->rlink == NULL){
        printf("Employee details deleted: ssn=%d\n", first->ssn);free(first);
        return NULL;
    }

    second = first->rlink;
    second->llink= NULL;
    printf("Employee details deleted: ssn=%d\n", first->ssn);
    free(first);
    return second;
}

NODE delete_rear(NODE first){
    NODE cur, prev;
    if (first == NULL){
        printf("List is empty cannot delete\n");
        return first;
    }
    if (first->rlink == NULL ){
        printf("Employee details deleted: ssn= %d\n",first->ssn);
        free(first);
        return NULL;
    }

    prev = NULL;
    cur = first;
    while(cur->rlink != NULL ){
        prev = cur;
        cur = cur->rlink;
    }
    printf("Employee details deleted: ssn=%d\n",cur->ssn);
    prev->rlink = NULL;

    return first;
}


void display(NODE first){
    NODE temp,cur;int
    count = 0;
    if (first == NULL){
        printf("employee list is empty\n");
        return;
    }

    cur = first;
    while (cur != NULL){
        printf("%d %.2f %s %s %s %s\n", cur->ssn, cur->salary, cur->name,cur->department, cur->designation, cur->phone);
        cur =cur->rlink;
        count++;
    }
    printf("Number of employees = %d\n", count);
}

void main(){
    for (;;){
        NODE first;
        int choice;
        EMPLOYEE item;first =
        NULL;
        printf("1:Insert_Front 2: Insert_Rear\n");
        printf("3:Delete_Front 4: Delete_Rear\n");
        printf("5:Display 6: Exit\n");
        printf("Enter the choice\n");
        scanf("%d", &choice);
        
        switch(choice) {
            case 1: printf("ssn :");
                scanf("%d",&item.ssn);
                printf("name :");
                scanf("%s",item.name);
                printf("department :");
                scanf("%s",item.department);
                printf("designation :");
                scanf("%s",item.designation);
                printf("salary :");
                scanf("%f",&item.salary);
                printf("phone :");
                scanf("%s",item.phone);
                first = insert_front(item,first);
                break;
            case 2: printf("ssn :");
                scanf("%d",&item.ssn);
                printf("name :");
                scanf("%s",item.name);
                printf("department :");
                scanf("%s",item.department);
                printf("designation :");
                scanf("%s",item.designation);
                printf("salary :");
                scanf("%f",&item.salary);
                printf("phone :");
                scanf("%s",item.phone);
                first = insert_rear (item, first);
                break;
            case 3: first=delete_front(first);
                break;
            case 4: first=delete_rear(first);
                break;
            case 5: display(first);
                break;
            default: exit(0);
        }
    }
}
```


# Program 10

```c
#include<stdio.h>
#include <stdlib.h>
#define MAX 20

struct node{
int data;
struct node *lchild, *rchild;
};

typedef struct node* NODE;

NODE tree = NULL;

void CreateBST (int a[MAX], int n){
    NODE temp, p, q;
    int i;
    for(i=0;i<n;i++){
        temp =(struct node *)malloc(sizeof(struct node*));
        temp->data = a[i];
        temp->lchild = temp->rchild = NULL;
        if(tree == NULL) tree = temp;
        else{
            p = q = tree;

            while(q != NULL){
                p=q;
                if(a[i] < p->data) q = p->lchild;
                else if(a[i] > p->data) q = p->rchild;
                else{
                    free(temp);
                    break;
                }
            }

            if( q == NULL)
            {
                if(a[i] < p->data) p->lchild = temp;
                else p->rchild = temp;
            }
        }
    }
    printf("Binary Seacrh Tree created\n\n");
}

void Inorder(NODE tree){
    if(tree != NULL){
        Inorder(tree->lchild);
        printf("%d ",tree->data);
        Inorder(tree->rchild);
    }
}

void Preorder(NODE tree){
    if(tree != NULL){
        printf("%d ",tree->data);
        Preorder(tree->lchild);
        Preorder(tree->rchild);
    }
}

void Postorder(NODE tree){
    if(tree != NULL){
        Postorder(tree->lchild);
        Postorder(tree->rchild);
        printf("%d ",tree->data);
    }
}

int main(){
    int a[MAX], n, i, choice;
    while(1){
        printf("\n\n**********************MENU*****************"); 
        printf("\n1.Create a BST of n integers\n2. Traverse the BST in Inorder\n3. Traverse the BST inPreorder\n4. Traverse the BST in Postorder\n5. Exit\n");
        printf("Enter your choice : ");
        scanf("%d",&choice);
        switch(choice){
            case 1 : printf("Enter the number of integers : ");
                scanf("%d",&n);
                printf("Enter the elements\n");
                for(i=0; i<n; i++)
                scanf("%d",&a[i]);
                CreateBST(a, n);
                break;
            case 2 : printf("Inorder Traversal :\n");
                Inorder(tree);
                break;
            case 3 : printf("Preorder Traversal :\n");
                Preorder(tree);
                break;
            case 4 : printf("Postoder Traversal :\n");
                Postorder(tree);
                break;
            case 5 : exit(0);
                break;
        }
    }
}   
```
