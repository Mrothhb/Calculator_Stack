/****************************************************************************

Matthew Roth, A15685519
CSE 12, Winter 2019
January 22, 2015
cs12xcm
Assignment Three

File Name:      driver.c
Description:    The driver file to run the stack program. The driver will use 
switch case to request input from the user, and implement the input from the 
user on the generated stack. See file: stack.c for more details on program
design and implementation .
 ****************************************************************************/

/*		ANSWERS:
 * 1. $2 = (void *) 0x604010
 * 2. $5 = (Stack *) 0x604028
 * 3. Stack
 * 4 $7 = (Stack **) 0x7fffffffd8f8 a pointer to a pointer on Stack
 * 5. $9 = (Stack *) 0x604028, a pointer on the Stack
 * 6. the pointer described above minus three for shifting the index
 * 7. yes including the STACK_OFFSET
 **/

#include <stdio.h>
#include <stdlib.h>
#include "mylib.h"
#include "stack.h"

/* define the keyword "NULL" as 0 */
#ifdef NULL
#undef NULL
#endif
#define NULL 0

/*--------------------------------------------------------------------------
Function Name:         main 
Purpose:               run the stack.c program 
Description:           take input from the user and implement functions 
in the stack.c file 
Input:                 argc: argv: main variables   
Result:                The program will execute normally
Return:				   void.
--------------------------------------------------------------------------*/
int main (int argc, char * const * argv) {

	Stack * main_Stack = 0;         /* the test stack */
	unsigned long amount;           /* numbers of items possible go on stack */
	long command;                   /* stack command entered by user */
	long item = 0;                  /* item to go on stack */
	char option;                    /* the command line option */
	long status;                    /* return status of stack functions */

	/* initialize debug states */
	debug_off ();

	/* check command line options for debug display */
	while ((option = getopt (argc, argv, "x")) != EOF) {

		switch (option) {
			case 'x': debug_on (); break;
		}
	}

	while (1) {
		command = 0;            /* initialize command, need for loops */
		writeline ("\nPlease enter a command:", stdout);
		writeline ("\n\t(a)llocate, (d)eallocate, ", stdout);
		writeline ("p(u)sh, (p)op, (t)op, (i)sempty, (e)mpty, ",stdout);
		writeline ("\n\tis(f)ull, (n)um_elements, (w)rite to stdout, "
				, stdout);
		writeline ("(W)rite to stderr.\n", stdout);
		writeline ("Please enter choice:  ", stdout);
		command = getchar ();
		if (command == EOF)     /* are we done? */
			break;
		clrbuf (command);       /* get rid of extra characters */

		switch (command) {      /* process commands */
				
			case 'd':

				/*deallocate the memory in the stack*/			
				if(main_Stack != NULL){

					/*delete the stack*/
					delete_Stack(&main_Stack);
					if(main_Stack == NULL){
						writeline("Stack has been deleted.", stdout);
						break;
					}
				}
				else
					writeline("Stack was not deleted.", stdout);
				break;	


			case 'a':

				/*allocate*/
				writeline("Please enter the number of objects to be " 
						"able to store: ", stdout); 
				amount = decin();
				/*if the stack already exists then delete the old stack*/
				if(main_Stack != NULL){
					delete_Stack(&main_Stack);
				}
				/*create the new stack*/
				main_Stack = new_Stack(amount);
				break;

			case 'e': 

				/*empty stack*/
				empty_Stack(main_Stack);

				if (isempty_Stack(main_Stack))

					writeline("Stack is empty.\n", stdout);
				else
					writeline("Stack is not empty.\n", stdout);

				break;


			case 'f':    

			    /* isfull */
				if (isfull_Stack (main_Stack))
					writeline ("Stack is full.\n",stdout);
				else
					writeline ("Stack is not full.\n", stdout);
				break;

			case 'i': 

				/* isempty */
				if (isempty_Stack (main_Stack))
					writeline ("Stack is empty.\n", stdout);
				else
					writeline ("Stack is not empty.\n", stdout);
				break;

			case 'n':  

				/* get_occupancy */
				writeline ("Number of elements on the stack is:  ",
						stdout);
				decout (get_occupancy (main_Stack));
				newline (stdout);
				break;

			case 'p':    

				/* pop */
				status = pop (main_Stack, &item);
				if (! status)
					fprintf (stderr,"\nWARNING:  pop FAILED\n");
				else {
					writeline (
							"Number popped from the stack is:  ",
							stdout);
					decout (item);
					newline (stdout);
				}
				break;

			case 't':   

				/* top */
				status = top (main_Stack, &item);
				if (! status)
					fprintf (stderr,"\nWARNING:  top FAILED\n");
				else {
					writeline (
							"Number at top of the stack is:  ",
							stdout);
					decout (item);
					newline (stdout);
				}
				break;

			case 'u':  

				/* push */
				writeline (
						"\nPlease enter a number to push to stack:  ",
						stdout);
				item = decin ();
				clrbuf (0);     /* get rid of extra characters */
				status = push (main_Stack, item);
				if (! status)
					fprintf(stderr,"\nWARNING:  push FAILED\n");
				break;

			case 'w':      

				/* write */
				writeline ("\nThe Stack contains:\n", stdout);
				write_Stack (main_Stack, stdout);
				break;

			case 'W':  

				/* write */
				writeline ("\nThe Stack contains:\n", stdout);
				write_Stack (main_Stack, stderr);
				break;
		}

		if (item == EOF) /* check if done */
			break;
	}

	if (main_Stack)
		delete_Stack (&main_Stack);     /* deallocate stack */
	newline (stdout);
	return 0;
}

