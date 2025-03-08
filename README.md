## C Program: Count Non-Whitespace Characters

This program counts the number of non-white-space characters in a given input text file.

```c
/*
 * Author: Laxman Kharel
 * Date: September 12, 2024
 *
 * Description:
 * This program counts the number of non-white-space characters in a given input text file.
 * It takes command-line arguments to specify an input file and either displays the result 
 * on the screen (using -s flag) or writes it to an output file (using -f flag). 
 * The program handles incomplete argument errors and checks if the input/output files can be opened.
 *
 * Limitations:
 * This program does not handle special encodings beyond standard ASCII text files. 
 * It expects the input file to be in a readable format and will return an error if not found.
 *
 * Critical code and data declarations:
 * - countNonWhitespaceChars function: Reads through the file and counts non-white-space characters.
 * - Command-line arguments: These are used to determine the input file, output file, and display method.
 * - FILE pointers: Used for reading from input files and writing to output files if necessary.
 */

#include <stdio.h>
#include <ctype.h>  // For checking if a character is whitespace
#include <stdlib.h> // For exit function
#include <string.h> // For strcmp function

// Function to count non-whitespace characters in the given file
/*
 * Function: countNonWhitespaceChars
 * Parameters: FILE *file - pointer to the file to be read
 * Returns: int - number of non-whitespace characters in the file
 * Description: This function reads through the file character by character and increments
 *              a counter for each non-whitespace character it finds.
 */
int countNonWhitespaceChars(FILE *file) {
    int count = 0;
    char ch;
    while ((ch = fgetc(file)) != EOF) {
        // Check if the character is not a whitespace
        if (!isspace(ch)) {
            count++;
        }
    }
    return count;
}

int main(int argc, char *argv[]) {
    // Check for valid number of arguments
    if (argc < 3) {
        printf("Usage: %s -f inputfile outputfile OR %s -s inputfile\n", argv[0], argv[0]);
        return 1;
    }

    // Open the input file for reading
    FILE *inputFile = fopen(argv[2], "r");
    if (inputFile == NULL) {
        printf("Error: Cannot open input file.\n");
        return 1;
    }

    // Count non-whitespace characters
    int nonWhiteSpaceCount = countNonWhitespaceChars(inputFile);
    fclose(inputFile); // Close the input file after processing

    // Handle the output based on the flag (-f for file, -s for screen)
    if (strcmp(argv[1], "-f") == 0 && argc == 4) {
        // Open the output file for writing
        FILE *outputFile = fopen(argv[3], "w");
        if (outputFile == NULL) {
            printf("Error: Cannot open output file.\n");
            return 1;
        }
        // Write the result to the output file
        fprintf(outputFile, "Non-whitespace character count: %d\n", nonWhiteSpaceCount);
        fclose(outputFile); // Close the output file
    } else if (strcmp(argv[1], "-s") == 0) {
        // Display the result on the screen
        printf("Non-whitespace character count: %d\n", nonWhiteSpaceCount);
    } else {
        printf("Invalid arguments.\n");
        return 1;
    }

    return 0;
}
# my-new-repository
