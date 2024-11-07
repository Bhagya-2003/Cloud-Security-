# Cloud-Security-
Program_2

#include <math.h>  
#include <stdio.h> 
long int power(long int a, long int b,long int P)  
{      
    if (b == 1)
    return a;
    else  
    return (((long  int)pow(a, b)) % P);  } 
    int main()  {
    int P, G, x, a, y, b, ka, kb;
    P = 23; // A prime number P is takeN
    printf("\n\n\t\t\tDIFFIEHELLMAN ALGORITHM");  
    printf("\n\n\t\t\tThe value of P : %ld", P);  
    G = 9; // A primitive root for P, G is taken      
    printf("\n\t\t\tThe value of G : %ld", G);          
    a = 4; 
    printf("\n\n\t\t\tThe private key a for Alice :%ld", a);
    x	= power(G, a, P); 
    b = 3;     
    printf("\n\t\t\tThe private key b for Bob :%ld", b);  
    y	= power(G, b, P);       
    ka = power(y, a, P);    
    kb = power(x, b, P);   
    printf("\n\n\t\t\tSecret key for the Alice is : %ld", ka);     
    printf("\n\t\t\tSecret Key for the Bob is : %ld", kb);     
    return 0;  
}

program_4

#include <stdio.h>  
#include <stdlib.h>  
#include <time.h>  
#include <math.h>  
#define MODULUS 111  
#define EXPONENT 5  
int mod_exp(int base, int exp, int mod)   
{
    int result = 1;
    base = base % mod;
    while (exp > 0)   
    {  
        if (exp % 2 == 1)   
       {  
            result = (result * base) % mod;  
        }  
        exp = exp >> 1;  
        base = (base * base) % mod;  
    }  
    return result;  
}   
int main()   
{  
    int random, commitment, challenge, response, verifier_check;     
    int secret = 7; // Prover's secret  
    int public_key = mod_exp(secret, EXPONENT, MODULUS);  
    printf("\n\n\t\t\tGUILLOU-QUISQUATER IDENTIFICATION PROTOCOL");     
    printf("\n\n\t\t\tProver's public key: %d", public_key);  
    srand(time(NULL));     
    random = rand() % MODULUS;      
    commitment = mod_exp(random, EXPONENT, MODULUS);  
    printf("\n\n\t\t\tCommitment: %d", commitment);  
    challenge = rand() % EXPONENT;
    printf("\n\n\t\t\tChallenge: %d", challenge);  
    response = (random * (int)pow(secret, challenge)) % MODULUS;     
    printf("\n\n\t\t\tResponse: %d", response);  
    verifier_check = (mod_exp(response,EXPONENT,MODULUS)* mod_exp(public_key, challenge, MODULUS)) % MODULUS;  
    if (verifier_check == commitment)  
    {  
  	printf("\n\n\t\t\tVerification successful!");  
    }      
    else  
   {  
  	printf("\n\n\t\t\tVerification failed!");  
    }  
    return 0;  
}

program_6

#include <stdio.h>  
#include <string.h>  
#define MAX_USERS 3  
  
typedef struct   
{  
    char username[50];     
    char role[20];  
} User;  
  
void performTask(const char *role)   
{  
    if (strcmp(role, "admin") == 0)   
    {  
        printf("\n\n\t\t\tAdmin task performed.");  
    }   
    else if (strcmp(role, "user") == 0)   
    {  
        printf("\n\n\t\t\tUser task performed.");  
    }      
    else      
    {  
        printf("\n\n\t\t\tNo privileges to perform this task.");  
    }  
} 
int main()   
{  
    User users[MAX_USERS] =   
    {  
  	{"alice", "admin"},  
  	{"bob", "user"},  
  	{"charlie", "guest"}  
    };  
    int found,i;      
    char username[50];  
    printf("\n\n\t\t\tPRINCIPLE OF LEAST PRIVILEGE");     
    printf("\n\n\t\t\tEnter Username : ");     
    scanf("%s", username);  
  
    found = 0;  
    for (i = 0; i < MAX_USERS; i++) {          
        if (strcmp(users[i].username, username) == 0)   
       {  
            found = 1;  
            printf("\n\t\t\tWelcome, %s!", users[i].username);
            performTask(users[i].role);             
            break;  
        }  
    }  
    if (!found)   
   {  
        printf("\n\n\t\t\tUser not found.");  
    }  
    return 0;  
}

program_8

#include <stdio.h>  
#include <string.h>  
#include <time.h>  
 
#define MAX_FILES 10  
#define MAX_FILENAME_LEN 100  
typedef struct  
{  
    char filename[MAX_FILENAME_LEN];      
    time_t last_modified;     
    int is_full_backup;  
} File;  
void perform_full_backup(File files[], int num_files)  
{
int i ;   
printf("\nPerforming full backup...");     
for ( i = 0; i < num_files; i++) 
{   
    files[i].is_full_backup = 1;   
    files[i].last_modified = time(NULL);    	
    printf("\n\t\tBacking up: %s", files[i].filename);  
    }  
}  
void perform_differential_backup(File files[], int num_files)  
{
int i ;   
    printf("\nPerforming differential backup...");      
    for (i = 0; i < num_files; i++)  
    {  
  	if (files[i].is_full_backup == 0)  
  	{  
  	    printf("\n\t\tBacking up: %s", files[i].filename);       
  	    files[i].last_modified = time(NULL);  
  	}  
  	else  
  	{  
  	    printf("\n\t\tSkipping (already fully backed up): %s", files[i].filename);  
  	}  
    }  
}  
void modify_file(File files[], int index)  
{  
    files[index].is_full_backup = 0; 
    printf("\n\nFile modified: %s", files[index].filename);     
    time(&files[index].last_modified);  
    printf("   Last Modified  %s at %s",files[index].filename, ctime(&files[index].last_modified));  
}  
int main()  
{  
    File files[MAX_FILES] =  
    {  
  	{"file1.txt", 0, 0},    	
  	{"file2.txt", 0, 0},    	
  	{"file3.txt", 0, 0},  
  	{"file4.txt", 0, 0},  
  	{"file5.txt", 0, 0}  
    };  
    int num_files = 5;      
    printf("\t\t\tDIFFERENTIAL BACKUP PROCES");    
    perform_full_backup(files, num_files);    
    modify_file(files, 2);    
    perform_differential_backup(files, num_files);     
    modify_file(files, 4);    
perform_differential_backup(files, num_files);       
return 0;  
}
