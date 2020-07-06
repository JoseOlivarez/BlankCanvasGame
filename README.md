# Four Pass Assembler in C
/*Jose Olivarez Phase 1
2/19/2017  CSCI 3333.06*/



#include <stdio.h>
#include <stdlib.h>

char LoadFileName(char* s) { // function loads the filename the user input using a pointer that we pass in our main.
    printf("I understand your absurd request!\n");
    printf("This function will load the file: ");
    char fname[25]; // starts at 5 because load
    int i=5;
    while (s[i] != '\0') {
      fname[i-5] = s[i];
      i= i+1;
    }
    fname[i-5] = '\0';
    printf("%s\n", fname);
}

void debug() { // later to be used no parameters
  printf("I understand your absurd request!\n");
}
void dumpstartend(char* s) { // supposed to display user input for the start ing and ending address.
  printf("I understand your absurd request!\n");
  char start[25];
  char end[25];
  int i=5;
  while (s[i] != ' ') {
    //printf("%c",s[i]);
    start[i-5] = s[i];
    i++;
  }
  start[i-5] = '\0';
  i = i+1;
  int startChar = i;
  printf("start: %s\n", start);// prints start address
  while (s[i] != '\0') {
    //printf("%c",s[i]);
    end[i-startChar] = s[i];
    i= i+1;
  }
  end[i-startChar] = '\0';
  printf("end: %s\n", end); // prints end
}
void execute() {
  printf("I understand your absurd request!\n"); // to be used later
}
void AssembleFileName(char* s)  { // assembles the user input and the prints it out
    printf("I understand your absurd request!\n");
    printf("This function will load the file: ");
    char fname[25];
    int i=9;
    while (s[i] != '\0') {
      fname[i-9] = s[i];
      i = i+1;
    }
    fname[i-9] = '\0';
    printf("%s\n", fname);
}

void doDirectory() {

  // Will perform the Directory function

  printf("\nThe following are the current directory contents:\n");

  system("ls");

}

void doHelp() { // gives the user a list of commands
  printf("\nLoad <filename>         --Loads the file called <filename>.\n");

  printf("Execute                 --Uses a computer simulation to execute a "

    "program previously loaded.\n");

  printf("Debug                   --Allows you to execute in debug mode.\n");

  printf("Dump start end      --Calls dump between <start> and <end>. "

    "(Note: start and end should be hexadecimal values.)\n");

  printf("Help                    --Prints  help prompt.\n");

  printf("Assemble <filename>     --Assembles a file called <filename>.\n");

  printf("Directory               --Lists the contents of the "

    "current directory.\n");

  printf("Exit                    --Terminates  the program.\n");

}
void parametersneeded() { //a function used whenever parameters are needed.
  printf("Parameters are needed");

}
void main() {
  printf("How are you doing man I am phase 1"); // welcome message
  printf("\n");
  int parameterssatisfied = 1;
  char s[30];
  int shouldContinue = 1;
  while (shouldContinue) {
    fgets(s, 30, stdin);
    if (s[0] == 'e' && s[1] == 'x' && s[2] == 'i' && s[3] == 't') // checks if the characters match the commands and then calls them as functions.
      shouldContinue = 0;
    else if (s[0] == 'h' && s[1] == 'e' && s[2] == 'l' && s[3] == 'p')
      doHelp();
    else if (s[0] == 'd' && s[1] == 'i' && s[2] == 'r' && s[3] == 'e' && s[4] == 'c' && s[5] == 't' && s[6] == 'o' && s[6] == 'r' && s[7] == 'y')
      doDirectory();
    else if (s[0] == 'l' && s[1] == 'o' && s[2] == 'a' && s[3] == 'd') {
      LoadFileName(s);
      //char lfnparameter1[64];
      //char lfnparameter2[64];
      //fgets(lfnparameters, 64, stdin);
      //if (lfnparameters == ' ') {
      //  parametersneeded();
      //  parameterssatisfied = 0;
      //} else if (lfnparameters != NULL) {
      //  parameterssatisfied = 1;
      //  printf(lfnparameters);
    } else if (s[0] == 'e' && s[1] == 'x' && s[2] == 'e' && s[3] == 'c' && s[4] == 'u' && s[5] == 't' && s[6] == 'e')
      execute();
    else if (s[0] == 'd' && s[1] == 'e' && s[2] == 'b' && s[3] == 'g')
      debug();
    else if (s[0] == 'a' && s[1] == 's' && s[2] == 's' && s[3] == 'e' && s[4] == 'm' && s[5] == 'b' && s[6] == 'l' && s[7] == 'e' && s[8] == ' ')
      AssembleFileName(s);
    else if (s[0] == 'd' && s[1] == 'u' && s[2] == 'm' && s[3] == 'p' && s[4] == ' ')
      dumpstartend(s);
    else {
      printf("type out another statement \n");
    }
  }
  //for(int i = 0; i< 2; i++)
  //{
  //gets(s);
  //fgets(s, sizeof(s), stdin);
  //}
  /*char *word = strtok(s, " .");
	char *secondword = strtok(NULL, " .");
  char *thirdword = strtok(NULL, " .");
  printf("%s\n", word);
	printf("%s\n", secondword);
	printf("%s\n", thirdword);
	*/
}
#include <stdio.h>
#include <string.h>
#include <errno.h>
#include "errorHandler.h"
#include <ctype.h>
//#include <conio.h>
#include <stdlib.h>

void checkLabel();
void checkOpcode();
void processLine();
void itoa(int n, char s[]);

struct optab {
	//char code[10];
	//char objcode[10];
	char* code;
	char* objcode;
} myoptab[25] = { { "ADD", "18" }, { "AND", "58" }, { "COMP", "28" }, { "DIV",
		"24" }, { "J", "3C" }, { "JEQ", "30" }, { "JGT", "34" },
		{ "JLT", "38" }, { "JSUB", "48" }, { "LDA", "00" }, { "LDCH", "50" }, {
				"LDL", "08" }, { "LDX", "04" }, { "MUL", "20" }, { "OR", "44" },
		{ "RD", "D8" }, { "RSUB", "4C" }, { "STA", "0C" }, { "STCH", "54" }, {
				"STL", "14" }, { "STX", "10" }, { "SUB", "1C" }, { "TD", "E0" },
		{ "TIX", "2C" }, { "WD", "DC" } };

struct symtab {
	char symbol[10];
	int addr;
} mysymtab[500];

const int numberOfOpcodes = 25;
unsigned int startaddr, locctr;
int symcount = 0, length, errorFlag = 0, numberOfErrors = 0, errors[500];
