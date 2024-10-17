// tictactoe.cpp
#include <iostream>

using namespace std;

// constants
const char SIGIL[3]={'.','X','O'};
const int NUMCOLUMNS = 3;
const int NUMROWS = 3;

int winner(int board[3][3]);
bool isGameOver(int board[3][3]);
void drawBoard(int board[3][3]);
bool isMoveLegal(int board[3][3], int, int);


int winner(int board[3][3]){
    if (board[0][0] == board[0][1] && board[0][0] == board[0][2] && board[0][0] != 0){
            return board[0][0];
        }
        if (board[1][0] == board[1][1] && board[1][0] == board[1][2] && board[1][0] != 0){
            return board[1][0];
        }
        if (board[2][0] == board[2][1] && board[2][0] == board[2][2] && board[2][0] != 0){
            return board[2][0];
        }
        if (board[0][0] == board[1][0] && board[0][0] == board[2][0] && board[0][0] != 0){
            return board[0][0];
        }
        if (board[0][1] == board[1][1] && board[0][1] == board[2][1] && board[0][1] != 0){
            return board[0][1];
        }
        if (board[0][2] == board[1][2] && board[0][2] == board[2][2] && board[0][2] != 0){
            return board[0][2];
        }
        if (board[0][0] == board[1][1] && board[0][0] == board[2][2] && board[0][0] != 0){
            return board[0][0];
        }
        if (board[2][0] == board[1][1] && board[2][0] == board[0][2] && board[2][0] != 0){
            return board[2][0];
        }
        return 0;
    }

void drawBoard(int board[3][3]){
	cout << " 0 1 2"<< endl;
	for (int row = 0; row < NUMCOLUMNS; ++row) 
	{
        cout << row << " ";
        for (int col = 0; col < NUMROWS; ++col) 
        {
            cout << SIGIL[board[row][col]] << " ";
        }
        cout << endl;
    }
}

bool isMoveLegal(int board[3][3], int row, int column){
    if (row < 0 || row >= NUMROWS) {
        return false;
    }
    if (column < 0 || column >= NUMCOLUMNS){
    	return false;
    }
    if (board[row][column] != 0) {
        return false;
    }
    return true;
}


bool isGameOver(int board[3][3]){
	if (winner(board) == 1 || winner(board) == 2) return true;
	for(int r=0; r<=2; r++)
		for (int c=0; c<=2; c++)
			if (board[r][c] == 0)
			return false;
	return true;
}

int main()
{
	int board[3][3]={{0}}; // 0 for empty square, 1 or 2 for taken squares
	int player = 1;
	int row, column, result;
	bool legalMove;

	// starting board
	drawBoard(board);
	while(!isGameOver(board)){
		cout << "Player " << player << "(" << SIGIL[player] << "), your move?";
		cin >> row >> column;
		legalMove = isMoveLegal(board, row, column);
		while(!legalMove){
			cout << "Player " << player << "(" << SIGIL[player] << "), your move?";
			cin >> row >> column;
			legalMove = isMoveLegal(board, row, column);
			}
		board[row][column] = player;
		drawBoard(board);
		player = 3 - player;
		}

	result = winner(board);
	if (result == 0){
		cout << "Tie Game" << endl;
	} else {
		cout << "Player " << result << "(" << SIGIL[result] << ") wins!" << endl;
	}
	return 0;
}
