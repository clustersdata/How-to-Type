# How-to-Type

How to Type

Problem Description

Pirates have finished developing the typing software. He called Cathy to test his typing software. She is good at thinking. After testing for several days, she finds that if she types a string by some ways, she will type the key at least. But she has a bad habit that if the caps lock is on, she must turn off it, after she finishes typing. Now she wants to know the smallest times of typing the key to finish typing a string.

Input

The first line is an integer t (t<=100), which is the number of test case in the input file. For each test case, there is only one string which consists of lowercase letter and upper case letter. The length of the string is at most 100.

Output

For each test case, you must output the smallest times of typing the key to finish typing this string.

Sample Input

3 Pirates HDUacm HDUACM

Sample Output

8 8 8 

Hint

The string “Pirates”, can type this way, Shift, p, i, r, a, t, e, s, the answer is 8. The string “HDUacm”, can type this way, Caps lock, h, d, u, Caps lock, a, c, m, the answer is 8 The string "HDUACM", can type this way Caps lock h, d, u, a, c, m, Caps lock, the answer is 

8

代码：#include <stdio.h>

#include <string.h>

#define MAX 200

int arr[MAX][4];

char str[MAX];

int letter(char ch)

{

 if(ch>='A'&&ch<='Z') return 1;
 
 return 0;
 
}

void proc()

{

 int i;
 
 int tmp,min;
 
 int len=strlen(str);
 
 for(i=0;i<len;i++)
 
{
     if(i==0)
     
     {
     
         if(letter(str[i])) {  arr[i][1]=2;   arr[i][2]=2; }
         
          else         {  arr[i][0]=1;   arr[i][3]=3; }
          
      }
      
      else
      
      {
      
          if(letter(str[i])==letter(str[i-1]))
          
          {
          
              if(arr[i-1][0]){  arr[i][0]=arr[i-1][0]+1;arr[i][3]=arr[i-1][0]+3;}
              
              if(arr[i-1][1]) { arr[i][1]=arr[i-1][1]+2;  arr[i][2]=arr[i-1][1]+2;}
              
              if(arr[i-1][2])
              
              {
              
                  if(arr[i][0]>arr[i-1][2]+1||!arr[i][0]) arr[i][0]=arr[i-1][2]+1;
                  
                  if(arr[i][3]>arr[i-1][2]+3||!arr[i][3]) arr[i][3]=arr[i-1][2]+3;
                  
               }
               
               if(arr[i-1][3])
               
               {
               
                  if(arr[i][1]>arr[i-1][3]+2||!arr[i][1]) arr[i][1]=arr[i-1][3]+2;
                  
                  if(arr[i][2]>arr[i-1][3]+2||!arr[i][2]) arr[i][2]=arr[i-1][3]+2;
                  
                }
                
            }
            
            else
            
            {
            
                if(arr[i-1][0]){   arr[i][1]=arr[i-1][0]+2;   arr[i][2]=arr[i-1][0]+2;}
                
                if(arr[i-1][1]){   arr[i][0]=arr[i-1][1]+1;   arr[i][3]=arr[i-1][1]+3;}
                
                if(arr[i-1][2])
                
                {
                
                    if(arr[i][1]>arr[i-1][2]+2||!arr[i][1]) arr[i][1]=arr[i-1][2]+2;
                    
                    if(arr[i][2]>arr[i-1][2]+2||!arr[i][2]) arr[i][2]=arr[i-1][2]+2;
                    
                }
                
                if(arr[i-1][3])
                
                {
                
                    if(arr[i][0]>arr[i-1][3]+1||!arr[i][0]) arr[i][0]=arr[i-1][3]+1;
                    
                    if(arr[i][3]>arr[i-1][3]+3||!arr[i][3]) arr[i][3]=arr[i-1][3]+3;
                    
                }
                
            }
            
        }
        
    }
    
    min=3*MAX;
    
    if(letter(str[len-1]))
    
    {
    
        if(arr[len-1][0]){  tmp=arr[len-1][0]+1;  if(tmp<min) min=tmp;}
        
        if(arr[len-1][1]){  tmp=arr[len-1][1];     if(tmp<min) min=tmp;  }
        
        if(arr[len-1][2]){  tmp=arr[len-1][2]+1;   if(tmp<min) min=tmp;}
        
        if(arr[len-1][3]){  tmp=arr[len-1][3];     if(tmp<min) min=tmp;  }
        
    }
    
    else
    
    {
    
        if(arr[len-1][0]) {  tmp=arr[len-1][0];     if(tmp<min) min=tmp; }
        
        if(arr[len-1][1]) {  tmp=arr[len-1][1]+1;   if(tmp<min) min=tmp;}
        
        if(arr[len-1][2]) {  tmp=arr[len-1][2];     if(tmp<min) min=tmp; }
        
        if(arr[len-1][3]) {  tmp=arr[len-1][3]+1;   if(tmp<min) min=tmp;}
        
    }
    
    printf("%d\n",min);
   
    
}

//Caps Shift:0-00;1-01;2-10;3-11

int main()

{


    int num;
    
    scanf("%d",&num);
    
    while(num--)
    
    {
    
        scanf("%s",str);
        
        memset(arr,0,strlen(str)*4*sizeof(int));
        
        proc();
        
    }
    
    return 0;
    
}
