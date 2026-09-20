# tic-tac-toe
#include <iostream>
using namespace std;


void displayBoard(char board[3][3])
{
    cout << "\n";
    cout << "     |     |     \n";
    cout << "  " << board[0][0] << "  |  " << board[0][1] << "  |  " << board[0][2] << "\n";
    cout << "_____|_____|_____\n";
    cout << "     |     |     \n";
    cout << "  " << board[1][0] << "  |  " << board[1][1] << "  |  " << board[1][2] << "\n";
    cout << "_____|_____|_____\n";
    cout << "     |     |     \n";
    cout << "  " << board[2][0] << "  |  " << board[2][1] << "  |  " << board[2][2] << "\n";
    cout << "     |     |     \n";
}

// Check whether a player has won
bool checkWin(char board[3][3], char player)
{
    // Check rows
    for (int i = 0; i < 3; i++)
    {
        if (board[i][0] == player &&
            board[i][1] == player &&
            board[i][2] == player)
        {
            return true;
        }
    }

    // Check columns
    for (int i = 0; i < 3; i++)
    {
        if (board[0][i] == player &&
            board[1][i] == player &&
            board[2][i] == player)
        {
            return true;
        }
    }

    // Check diagonals
    if (board[0][0] == player &&
        board[1][1] == player &&
        board[2][2] == player)
    {
        return true;
    }

    if (board[0][2] == player &&
        board[1][1] == player &&
        board[2][0] == player)
    {
        return true;
    }

    return false;
}

// Check whether the board is full
bool checkDraw(char board[3][3])
{
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            if (board[i][j] != 'X' && board[i][j] != 'O')
            {
                return false;
            }
        }
    }

    return true;
}

int main()
{
    // Initial board
    char board[3][3] =
    {
        {'1', '2', '3'},
        {'4', '5', '6'},
        {'7', '8', '9'}
    };

    char currentPlayer = 'X';
    int choice;
    int row, col;

    cout << "=================================\n";
    cout << "       TIC-TAC-TOE GAME\n";
    cout << "=================================\n";

    cout << "\nPlayer 1: X";
    cout << "\nPlayer 2: O\n";

    while (true)
    {
        displayBoard(board);

        cout << "\nPlayer " << currentPlayer;
        cout << ", enter your choice (1-9): ";
        cin >> choice;

        // Convert choice into row and column
        row = (choice - 1) / 3;
        col = (choice - 1) % 3;

        // Check invalid input
        if (choice < 1 || choice > 9)
        {
            cout << "Invalid choice! Please choose between 1 and 9.\n";
            continue;
        }

        // Check whether position is already occupied
        if (board[row][col] == 'X' || board[row][col] == 'O')
        {
            cout << "This position is already occupied!\n";
            continue;
        }

        // Place player's symbol
        board[row][col] = currentPlayer;

        // Check winner
        if (checkWin(board, currentPlayer))
        {
            displayBoard(board);

            cout << "\n=================================\n";
            cout << "       Player " << currentPlayer << " WINS!\n";
            cout << "=================================\n";

            break;
        }

        // Check draw
        if (checkDraw(board))
        {
            displayBoard(board);

            cout << "\n=================================\n";
            cout << "          GAME DRAW!\n";
            cout << "=================================\n";

            break;
        }

        // Change player
        if (currentPlayer == 'X')
        {
            currentPlayer = 'O';
        }
        else
        {
            currentPlayer = 'X';
        }
    }

    cout << "\nThank you for playing Tic-Tac-Toe!\n";

    return 0;
}
