

#include <iostream>
#include <algorithm>
#include <cstdlib> // for using the system that clears the console screen
using namespace std;

int main() {

    cout<<"Welcome to the Memory Game!"<<endl;
    
    int n;
    // Input the size of the array between 6 and 20
    cout << "Enter the size of the array (between 6 and 20): ";
    cin >> n;

    // Validate the input size
    while (n < 6 || n > 20) {
        cout << "Invalid size. Please enter a size between 6 and 20: ";
        cin >> n;
    }

    // Create an array of numbers
    int arr[20]; 
    for (int i = 0; i < n; i++) {
        arr[i] = i / 2 + 1;  // Each number appears twice
    }
    
    // Shuffle the array 
    random_shuffle(arr, arr + n);
    
    // Game loop
    int moves = 0;
    bool found[20] = {false}; // Array to track found pairs

    while (count(found, found + n, true) < n) { 
    // Continue the loop until all elements are found (true)
        
        // Display the current state of the array
        cout<<"Here is the array:"<<" ";
        for (int i = 0; i < n; i++) {
            if (found[i]) {
                cout << arr[i] << " "; // If player finds the number, they are flips in the array
            } else {
                cout << "? ";
            }
        }
        cout <<endl;
        
        // Get user input for two indices
        int a,b;
        cout<<"Enter the index to show (0 to " << n - 1 << "): ";
        cin>>a;
        cout<<"The card at index"<<" "<<a<<" "<<"is:"<<" "<<arr[a]<<endl;
        
        cout<<"Enter the second index to show (0 to " << n - 1 << "):";
        cin>>b;
        cout<<"The card at index"<<" "<<b<<" "<< "is:"<<" "<<arr[b]<<endl;

        // Validate input indices
        while (a < 0 || a >= n || b < 0 || b >= n || found[a] || found[b]) {
            cout << "Invalid indices or cards already found. Enter two valid indices: ";
            cin >> a >> b;
        }

        // Increment moves
        moves++;
        
        // Check if the selected cards match
         if(arr[a]==arr[b]){
            cout<<"Great! The cards are matched. Continue..."<<endl;
            cout<<"Press Enter to continue..."<<endl;
            found[a]=found[b]= true;
        }
        else{
            cout<<"The cards do not match. Try again!"<<endl;
            cout<<"Press Enter to continue..."<<endl;
        }
        
        // Clear the screen after pressinf Enter
        getchar();
        getchar();
        
        system("clear");
        cout<<endl;
        
    }

    cout<<"Congratulations! You won the game!"<<endl;
    cout << "Game completed in " << moves << " moves.";
}
