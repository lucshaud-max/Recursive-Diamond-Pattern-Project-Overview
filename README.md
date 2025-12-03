/*
    --------------------------------------------------------------
    Recursive Diamond Pattern Project
    Author: Rashaud Luc

    Description:
        This program prints a symmetrical diamond made entirely of
        asterisks (*) using recursion to control the row structure.
        
        The recursion works by:
            1. Printing the TOP half of the diamond through a 
               recursive method that decreases the left-star count
               and expands the inner-star count.
            2. Printing the BOTTOM half of the diamond through
               another recursive method that increases the 
               left-star count and shrinks the inner-star count.

        Only simple loops are used for character printing.
        No for/while loops are used to control the overall row flow.

        Output EXACTLY matches the assignment example.
    --------------------------------------------------------------
*/

#include <iostream>
using namespace std;

// Helper function to print n copies of a character
void printChars(int n, char c) {
    for (int i = 0; i < n; i++)
        cout << c;
}

/*
    Recursively prints the TOP half of the diamond.
    leftStars = number of stars on the left side
    innerStars = number of stars inside the center gap

    Recursion shrinks leftStars and grows innerStars each level.
*/
void printTop(int leftStars, int innerStars) {
    // Base case: stop BEFORE the center row
    if (leftStars == 1)
        return;

    // Print current row
    printChars(leftStars, '*');
    cout << "  ";
    printChars(innerStars, '*');
    cout << "  ";
    printChars(leftStars, '*');
    cout << endl;

    // Recursive call: shrink outer stars, grow inner stars
    printTop(leftStars - 1, innerStars + 2);
}

/*
    Recursively prints the BOTTOM half of the diamond.
    Starts from the center and expands outward.
*/
void printBottom(int leftStars, int innerStars, int target) {
    // Base case: stop after restoring full width
    if (leftStars > target)
        return;

    printChars(leftStars, '*');
    cout << "  ";
    printChars(innerStars, '*');
    cout << "  ";
    printChars(leftStars, '*');
    cout << endl;

    // Recursive call: grow left stars, shrink inner
    printBottom(leftStars + 1, innerStars - 2, target);
}

int main() {
    // Top line (printed only once)
    printChars(25, '*');
    cout << endl;

    // Print upper half (excluding top & center)
    printTop(11, 1);  // Matches assignment's spacing exactly

    // Print center line
    printChars(1, '*');
    cout << "  ";
    printChars(21, '*');
    cout << "  ";
    printChars(1, '*');
    cout << endl;

    // Print lower half (mirrors upper)
    printBottom(2, 19, 11);

    // Bottom line (printed only once)
    printChars(25, '*');
    cout << endl;

    return 0;
}
