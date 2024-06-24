#include<stdio.h>
#include<string.h>
#include<unistd.h>

#define MAX_SIZE 1000
/*0. Print out the list;
1. Find maximum marks and print to screen;
2. Find marks that are greater than or equal to average of all the marks;
3. Insert a mark into the array;
4. Delete a mark from the array;
5. Insert a marrk into the array at require signal
6. Sort the array (Ascending Order)
7. Input two float numbers a and b (a<b). Show marks that are greater than or equal to a and less than or equal to b */

// Nhap so luong phan tu trong mang
void inputInteger ( char *label, int *n);
// Nhap mang
void inputArray ( int *arr, int size);
// In ra mang moi
void printArray ( int *arr, int size);

// Tao cac ham tinh toan:
// 1. Tinh so lon nhat trong mang
void MAX ( int *arr, int size);

// 2. Tim cac phan tu lon hon hoac bang gia tri trung binh cua mang 
double caculateAverage ( int *arr , int size);
void printValueIsFiltered ( int *arr , int size, int Average );

// 3. Xoa so ra tu mang tai vi tri chi dinh
void removeNumberfromArray (int *arr, int *size, int index);

// 4. Them vao mot so tai vi tri chi dinh 
void insertNumberToRequireSignal ( int *arr, int *size, int index, int newElement);

// 5. Sap xep cac so trong mang
void sortArray ( int *arr, int size);

// 6. Tim cac phan tu nam trong khoang [ a ; b ]
void filterOfArray ( int *arr, int size, int Num1, int Num2);

// 7. Xoa nhieu phan tu cung luc 
void removeMoreValue(int *arr, int *size, int *signaltoDelete, int numToDelete);

// 8. Them nhieu phan tu cung luc
void insertMoreValue ( int *arr, int *size, int *signalToInsert, int *valueToInsert, int numToInsert);

// Hàm de sap xep mang theo thu tu giam dan
void sortHighToDown(int *arr, int size);



int main(){
	int i, j;
	char c; // Ki tu xuong dong
	char choice;// Lua chon yes/no
	int numbers [ MAX_SIZE];
	
	int n, z, x; // so luong phan tu trong mang, z la so nhap vao de chon chuc nang, x la so nhap vao chuc nang cua tung case
	
	double Avg;// Avg la average trong Find marks that are greater than or equal to average of all the marks
	
	int newNum;// La newNumber trong Insert a mark into the array
	
	int place; // La index trong removeNumberfromArray
	
	int newN;// La newElement trong insertNumberToRequireSignal
	int signal; // La index trong insertNumberToRequireSignal
	
	int a; // Num1 trong filterOfArray
	int b; // Num2 trong filterOfArray
	
	int quantityToDelete; // so luong phan tu can xoa trong mang
	
	int quantityInsert; // so luong phan tu can them vao mang
	
	
	
	printf ("********************MANAGE POINT*********************\n");
	for ( i = 0; i <= 100; i+=25){
		printf ("Loading %d%%.......\n",i);
		sleep(1);
	}
	printf ("\nSUCCESSFUL !!!");
	sleep(1.5);
	system("cls"); 
	
	printf ("********************MANAGE POINT*********************\n");
	// Loc dau vao cho so luong phan tu mang
	do {
            printf( "\nInput the quantity of marks: " );
            scanf("%d", &n); // n la so phan tu trong mang
            scanf("%c", &c); // Doc phan nhap ky tu
            fflush(stdin);
            if ( n <= 0 || c != '\n') {
                printf("Choose again! ");
            }
        } while ( n <= 0 || c != '\n');
        
    // Loc dau vao cho viec nhap cac phan tu trong mang
	do{
	
            printf( "\nInput the marks: " );
            inputArray (numbers, n);
            scanf("%c", &c); // Doc phan nhap ky tu
            fflush(stdin);
            if ( c != '\n') {
                printf("Input again! ");
            }
    } while ( c != '\n');
	
	
	do{
	
		printf ("\n==========MENU==========");
		printf ("\n1.Max value in array");
		printf ("\n2.Value >= Average (array)");
		printf ("\n3.Delete number");
		printf ("\n4.Insert number (require)");
		printf ("\n5.Sort array");
		printf ("\n6.Filter value in [a;b]");
		printf ("\n7.Exit");
		
		 do {
            printf( "\nChoose number (1-7): " );
            scanf("%d", &z);
            scanf("%c", &c); // Doc phan nhap ky tu
            fflush(stdin);
            if (z < 1 || z > 7 || c != '\n') {
                printf( "Input again! " );
            }
        } while (z < 1 || z > 7 || c != '\n');
		
	switch (z){
		case 1:{
			if(n == 0){
					printf ("Not have value, input array again!");
				do{
				
					// Loc dau vao cho so luong phan tu mang
					do {
            			printf( "\nInput the quantity of array: " );
           				scanf("%d", &n);
            			scanf("%c", &c); // Doc phan nhap ky tu
            			fflush(stdin);
            			if ( n <= 0 || c != '\n') {
               				 printf("Input again! ");
            				}
       				 } while ( n <= 0 || c != '\n');
        
   					// Loc dau vao cho viec nhap cac phan tu trong mang
					do {
            			printf( "\nInput the array: " );
            			inputArray (numbers, n);
            			scanf("%c", &c); // Doc phan nhap ky tu
            			fflush(stdin);
            			if ( c != '\n') {
               				 printf("Input again! ");
            			}
        			} while ( c != '\n');
				
				}while (n == 0);
		}
			system("cls");
			MAX ( numbers, n);
		
			break;
		}
		
		case 2:{
			double Avg = caculateAverage ( numbers, n);
			system("cls");
			printValueIsFiltered ( numbers, n, Avg);
			break;
		}
		
		
		case 3:{
			do{
				printf ("\n1.Choose 1 index to delete\n");
				printf ("\n2.Choose more index to delete (>= 2)\n");
				printf ("\n3.Back to menu\n");
		
		
		 	do {
            	printf( "\nChoose number (1-3): " );
            	scanf("%d", &x);
            	scanf("%c", &c); // Doc phan nhap ky tu
            	fflush(stdin);
            	if (x < 1 || x > 3 || c != '\n') {
                	printf( "Input again! " );
            	}
        	} while (x < 1 || x > 3 || c != '\n');
        	
			switch (x){
        		case 1:{
				// Choose 1 value to delete
					do {
						if ( n == 0){
						printf ("Array not have value!");
						break;
						}
				
						do {
           					printf("\nInput the index to delete: ");
            				scanf("%d", &place);
           					scanf("%c", &c); // Doc phan nhap ky tu
            				fflush(stdin);
            				if ( place >= n|| place < 0 || c != '\n') {
                				printf( "Input again! " );
            				}
            
        				} while (place >= n || place < 0 || c != '\n');
        				
        				system("cls");
						removeNumberfromArray ( numbers, &n, place);
						printf ("\nThe array after use function: ");
						printArray (numbers, n);
			
				// Hoi nguoi dung co muon nhap them vi tri can xoa khong ?
	       				 do {
		            		printf("\nChoose ""y"" to CONTINUE and ""n"" to back FUNCTION: ");
	            			scanf("%c", &choice);
            				scanf("%c", &c); // Doc phan nhap ky tu
            				fflush(stdin);
            				if ( (choice != 'y' && choice != 'n') || c != '\n') {
                				printf("Choose again! ");
           		 			}
        				} while ((choice != 'y' && choice != 'n') || c != '\n');
        	
        				} while (choice =='y');
					break;
				}
			
				case 2:{
							do {
								if (n == 0) {
                    				printf("Array not have value!");
                    				break;
                				}
                				if (n == 1) {
                    				printf("Array have 1 value!");
                    				break;
                					}

                				
                				do {
                					
		            				printf("\nInput the quantity to delete: ");
	            					scanf("%d", &quantityToDelete);
            						scanf("%c", &c); // Doc phan nhap ky tu
            						fflush(stdin);
            						if (quantityToDelete < 2 || quantityToDelete > n || c != '\n') {
                						printf("Choose again! ");
           		 					}
        						} while ( quantityToDelete < 2 || quantityToDelete > n || c != '\n');
                				
                				

                				int indexToDelete[quantityToDelete];
                				
                				for (i = 0; i < quantityToDelete; i++) {
                					do {
		            					printf("\nInput the index to delete %d: ", i + 1);
	            						scanf("%d", &indexToDelete[i]);
            							scanf("%c", &c); // Doc phan nhap ky tu
            							fflush(stdin);
            							if (indexToDelete[i] < 0 || indexToDelete[i] >= n || c != '\n') {
                							printf("Choose again! ");
           		 						}
        							} while ( indexToDelete[i] < 0 || indexToDelete[i] >= n || c != '\n');
                				
                				}
                				
								system("cls");
                				removeMoreValue(numbers, &n, indexToDelete, quantityToDelete);
                				
                				printf("\nThe array after use function: ");
								printArray(numbers, n);

								// Hoi nguoi dung co muon nhap them vi tri can xoa khong?
								do {
		            				printf("\nChoose ""y"" to CONTINUE and ""n"" to back FUNCTION: ");
	            					scanf("%c", &choice);
            						scanf("%c", &c); // Doc phan nhap ky tu
            						fflush(stdin);
            						
            						if ((choice != 'y' && choice != 'n') || c != '\n') {
                						printf("Choose again! ");
           		 					}
           		 					
        						} while ((choice != 'y' && choice != 'n') || c != '\n');
        					} while (choice == 'y');
        					break;
						}
			
				case 3:{
					break;
					}	
				}
			}while (x!=3);
			
			break;
		}
		
		case 4:{
			do{
				printf ("\n1.Choose one index and number to insert\n");
				printf ("\n2.Choose more index to insert (>= 2)\n");
				printf ("\n3.Back to menu\n");
				
				do{
					printf( "\nChoose number (1-3): " );
					scanf ("%d", &x);
					scanf ("%c", &c); // Doc phan nhap ky tu
					fflush (stdin);
					if (x < 1 || x > 3  || c != '\n' ){
						printf ("Choose again!");
					}
				}while ( x < 1 || x > 3  || c != '\n');
				
				switch(x){
					
					// Chon mot vi tri de them so vao
					case 1:{
						do {
							
							do {
           						printf ("\nInput index to insert: ");
								scanf ("%d", &signal);
	           					scanf("%c", &c); // Doc phan nhap ky tu
            					fflush(stdin);
            					if ( signal > n || signal < 0 || c != '\n') {
                					printf( "Input again! " );
        	    					}
        					} while (signal > n || signal < 0 || c != '\n');
        					
        					do {
           						
								printf ("\nInput new number to insert: ");
								scanf ("%d", &newN);
	           					scanf("%c", &c); // Doc phan nhap ky tu
            					fflush(stdin);
            					if (  c != '\n') {
                					printf( "Input again! " );
        	    					}
        					} while ( c != '\n');
        				
        				system("cls");
						insertNumberToRequireSignal ( numbers, &n, signal, newN );
						printf ("\nThe array after use function: ");
						printArray (numbers, n);
			
			 				do {
            					printf("\nChoose ""y"" to CONTINUE and ""n"" to back FUNCTION: ");
            					scanf("%c", &choice);
            					scanf("%c", &c); // Doc phan nhap ky tu
            					fflush(stdin);
            					if ( (choice != 'y' && choice != 'n') || c != '\n') {
                					printf("Choose again! ");
           		 				}
        					} while ((choice != 'y' && choice != 'n') || c != '\n');
        	
        				} while (choice =='y');
						break;
					}
					
					// Chon nhieu vi tri de them so vao
					case 2:{
						do{		
								do {
		            				printf ("\nInput quantity insert: ");
	            					scanf("%d", &quantityInsert);
            						scanf("%c", &c); // Doc phan nhap ky tu
            						fflush(stdin);
            						if ( quantityInsert <= 0 ||c != '\n') {
                						printf("Choose again! ");
           		 					}
        						} while ( quantityInsert <= 0 || c != '\n');
								
								int indexInsert[quantityInsert];
								int valueInsert[quantityInsert];
								
								for ( i = 0; i < quantityInsert; i++){   
								     
                					do {
		            					printf("\nInput the index to insert %d: ", i + 1);
	            						scanf ("%d", &indexInsert[i]);
            							scanf("%c", &c); // Doc phan nhap ky tu
            							fflush(stdin);
            							if (indexInsert[i] < 0 || indexInsert[i] > n || c != '\n') {
                							printf("Choose again! ");
           		 						}
           		 						
        							} while ( indexInsert[i] < 0 || indexInsert[i] > n || c != '\n');               
									
									do {		            			
	            						printf("\nInput new number to insert %d: ", i + 1);
	            						scanf ("%d", &valueInsert[i]);
            							scanf("%c", &c); // Doc phan nhap ky tu
            							fflush(stdin);
            							if (c != '\n') {
                							printf("Choose again! ");
           		 						}
           		 						
        							} while (c != '\n');
																						
								}
								
								system("cls");
								insertMoreValue ( numbers, &n, indexInsert, valueInsert, quantityInsert);
								
								printf("\nThe array after use function: ");
								printArray(numbers, n);
								
								
								// Hoi nguoi dung co muon nhap them vi tri can xoa khong?
								do {
		            				printf("\nChoose \"y\" to CONTINUE and \"n\" to back FUNCTION: ");
	            					scanf("%c", &choice);
            						scanf("%c", &c); // Doc phan nhap ky tu
            						fflush(stdin);
            						if ((choice != 'y' && choice != 'n') || c != '\n') {
                						printf("Choose again! ");
           		 					}
        						} while ((choice != 'y' && choice != 'n') || c != '\n');
        						
						}while (choice == 'y');
						break;
					}
					
					case 3:{
						break;
					}
				} 
			
        	}while(x != 3);
        	
			break;
		}
		
		case 5:{
			do{
				if ( n == 0){
				printf ("Array not have value!");
				break;
				}
			}while (n==0);
			system("cls");
			sortArray ( numbers, n);
			break;
		}
		
		case 6:{
			do{
				if ( n == 0){
				printf ("Array not have value!");
				break;
				}
				
				do {
           			printf ("\nInput a and b: ");
					scanf ("%d %d", &a, &b); // a: Num1, b: Num2
           			scanf("%c", &c); // Doc phan nhap ky tu
            		fflush(stdin);
            		if ( a > b || c != '\n') {
                		printf( "Input again! " );
            		}
        		} while (a > b || c != '\n');
        		
				system("cls");
				filterOfArray ( numbers, n, a, b);
				printf ("\nThe array after use function: ");
				printArray (numbers, n);
			
			do{
				printf ("\n\nChoose ""y"" to CONTINUE and ""n"" to back MENU: ");
				scanf ("%c", &choice);
				scanf ("%c", &c); //Doc phan tu nhap ky tu
				fflush(stdin);
				if (choice != 'y' && choice != 'n' || c != '\n'){
					printf ("Choose again!");
				}
			}while (choice != 'y' && choice != 'n' || c != '\n');
		} while ( choice == 'y');
		
			break;
		}
		
		case 7:{
			do{
				printf ("Are you sure ? ");
				
				// Hoi nguoi dung co muon nhap them vi tri can xoa khong?
				do {
		            printf("\nChoose \"y\" to EXIT and \"n\" to CANCEL: ");
	            	scanf("%c", &choice);
            		scanf("%c", &c); // Doc phan nhap ky tu
            		fflush(stdin);
            		if ((choice != 'y' && choice != 'n') || c != '\n') {
                			printf("Choose again! ");
           		 		}
        		} while ((choice != 'y' && choice != 'n') || c != '\n');
        		
			
				if (choice == 'y'){
					system ("cls");
					printf ("************__________________THANK YOU__________________************");
					return 0;
					}
					
				if (choice == 'n'){
					break;
					}
        		
			}while (1);
			
			break;
		}
	}
	
	printf ("\nThe array after use function: ");
	printArray (numbers, n);
	} while (1);
}


// Nhap so luong phan tu trong mang
void inputInteger ( char *label, int *n){
	printf ("%s", label);
	scanf ("%d", n);
}
// Nhap mang
void inputArray ( int *arr, int size){
	int i;
	for ( i = 0; i < size; i++ ){
		scanf("%d", &arr[i]);
	}
}
// In ra mang moi
void printArray ( int *arr, int size){
	int i;
	for ( i = 0; i < size; i++ ){
		printf("%d ", arr[i]);
	}
}


// 1. Tinh so lon nhat trong mang
void MAX ( int *arr, int size){
	int Max = arr[0];
	int i ;
	for ( i = 0; i < size; i++){
		if (Max < arr[i]){
			Max = arr[i];
		}
	}
	printf ("Max value = %d", Max);
}

// 2. Tim cac phan tu lon hon hoac bang gia tri trung binh cua mang 
double caculateAverage ( int *arr , int size){
	int i;
	int sum = 0;
	for ( i = 0; i < size; i++){
		sum += arr[i];
	}
	return (double) sum / size;
}
void printValueIsFiltered ( int *arr , int size, int Average ){
	int i;
	printf ("Some value >= average (array):  ");
	for ( i = 0; i < size; i++){
		if (arr[i] >= Average){
			printf ("%d ", arr[i]);
		}
	}
}

// 3. Xoa so ra tu mang tai vi tri chi dinh
void removeNumberfromArray (int *arr, int *size, int index){
	int i;
	for ( i = index; i < *size - 1; i++){
		arr[i] = arr[i+1];
	}
	(*size) --;
	
}

// 4. Them vao mot so tai vi tri chi dinh 
void insertNumberToRequireSignal ( int *arr, int *size, int index, int newElement){
	int i;
	for ( i = *size; i > index; i--){
		arr[i] = arr[i-1];
	}
	arr[index] = newElement;
	(*size) ++;
	
}

// 5. Sap xep cac so trong mang
void sortArray ( int *arr, int size){
	int i;
	int j;
	for ( i = 0; i < size; i++){
		for (j = i +1; j < size; j++){
			if (arr[i] > arr[j] ){
				int temp = arr[i];
				arr[i] = arr[j];
				arr[j] = temp;
			}
		}
	}
}

// 6. Tim cac phan tu nam trong khoang [ a ; b ]
void filterOfArray ( int *arr, int size, int Num1, int Num2){
	int i;
	printf ("\nSome values in [a;b]: ");
	for ( i = 0; i < size; i++){
		if (arr[i] >= Num1 && arr[i] <= Num2){
			printf ("%d ", arr[i]);
		}
	}
	
}

// 7. Xoa nhieu phan tu cung luc 
void removeMoreValue(int *arr, int *size, int *signaltoDelete, int numToDelete) {
	int i, j;
	int newSize = *size;

	// Sap xep cac phan tu can xoa theo thu tu giam dan
	sortHighToDown(signaltoDelete, numToDelete);

	// Xoa cac phan tu trong mang theo thu tu tu trai sang phai theo nhung vi tri nhap vao
	for (i = 0; i < numToDelete; i++) {
		int index = signaltoDelete[i];
		if (index < newSize && index >= 0) {
			for (j = index; j < newSize - 1; j++) {
				arr[j] = arr[j + 1];
			}
			newSize--;
		}
	}

	*size = newSize;
}


// 8. Them nhieu phan tu cung mot luc
void insertMoreValue ( int *arr, int *size, int *signalToInsert, int *valueToInsert, int numToInsert){
	int i,j;
	int newSize = *size;
	
	//Sap xep cac phan tu theo thu tu giam dan
	sortHighToDown (signalToInsert, numToInsert);
	
	//Them cac phan tu trong mang theo thu tu tu trai sang phai theo nhung vi tri nhap vao
	for ( i = 0; i < numToInsert; i++){
		int index = signalToInsert[i];
		int value = valueToInsert[i];
		if (index <= newSize && index >= 0){
			for (j = newSize; j > index; j -- ){
				arr[j] = arr[j-1];
			}
			arr[index] = value;
			newSize ++;
		}
	}
	*size = newSize;
}

///////////////////////////// HAM SAP XEP THEO THU TU GIAM DAN/////////////////////////////
void sortHighToDown(int *arr, int size) {
	int i, j, temp;
	for (i = 0; i < size - 1; i++) {
		for (j = i + 1; j < size; j++) {
			if (arr[i] < arr[j]) {
				temp = arr[i];
				arr[i] = arr[j];
				arr[j] = temp;
			}
		}
	}
}

