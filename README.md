#include <iostream>
using namespace std;
char board[3][3];         
char current = 'X';  
void showBoard() {
    cout << "\n";
    for (int r = 0; r < 3; ++r) {
        for (int c = 0; c < 3; ++c) {
            char cell = board[r][c];
            // Print square number (1-9) if empty
            cout << ' ' << (cell ? cell : ('1' + r * 3 + c)) << ' ';
            if (c < 2) cout << '|';
        }
        if (r < 2) cout << "\n-----------\n";
    }
    cout << "\n\n";
}
bool win(char p) {
    for (int i = 0; i < 3; ++i)
        if ((board[i][0]==p && board[i][1]==p && board[i][2]==p) ||   // rows
            (board[0][i]==p && board[1][i]==p && board[2][i]==p))     // cols
            return true;
    return (board[0][0]==p && board[1][1]==p && board[2][2]==p) ||
           (board[0][2]==p && board[1][1]==p && board[2][0]==p);
}
bool full() {
    for (auto &row : board)
        for (char c : row)
            if (!c) return false;
    return true;
}

int main() {
    
    while (true) {
        showBoard();
        
        int move;
        cout << current << "'s turn (1-9): ";
        while (!(cin >> move) || move < 1 || move > 9 ||
               board[(move-1)/3][(move-1)%3]) {
            cin.clear(); cin.ignore(1000, '\n');
            cout << "Invalid. Try again: ";
        }
        board[(move-1)/3][(move-1)%3] = current;
        if (win(current)) {
            showBoard();
            cout << current << " wins!\n";
            break;
        }
        if (full()) {
            showBoard();
            cout << "Draw.\n";
            break;
        current = (current == 'X') ? 'O' : 'X';
    }
    return 0;
}
