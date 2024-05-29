# Individual-work
# Tic-Tac-Toe Game

Welcome to the Tic-Tac-Toe game! This is a simple implementation of the classic game in Java.

## How to Play

- Player 1 will be '♥' and Player 2 will be '♡'.
- Take turns to place your mark on the 3x3 grid.
- The first player to get three in a row, column, or diagonal wins!
- If the board is full and no player has won, the game is a draw.

## Game Code

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
      
        System.out.println("Welcome my firend! This is the best day you ever had, Im right? I cnow what can make this day even more better - Tic-Tac-Toe!");
        System.out.println("Player 1 will be '♥' and Player 2 will be '♡'.");
        System.out.println("Take turns to place your mark on the 3x3 grid.");
        System.out.println("The first player to get three in a row, column, or diagonal wins!");
        System.out.println("Let's start the game!");

        char[][] board = {
            {' ', ' ', ' '},
            {' ', ' ', ' '},
            {' ', ' ', ' '}
        };

        Scanner scanner = new Scanner(System.in);

        char currentPlayer = '♥';

        while (true) {
            printBoard(board);

        
            System.out.println("Player " + currentPlayer + "'s turn. Enter row and column (like 0,1) and press ENTER: ");
            String input = scanner.nextLine();
            String[] parts = input.split(",");
            int row = Integer.parseInt(parts[0]);
            int col = Integer.parseInt(parts[1]);

            if (row < 0 || row > 2 || col < 0 || col > 2 || board[row][col] != ' ') {
                System.out.println("Invalid move. The cell is either out of bounds or already occupied. Try again.");
                continue; 
            }

            board[row][col] = currentPlayer;

            if (checkWin(board, currentPlayer)) {
                printBoard(board); 
                System.out.println("Congratulations! Player " + currentPlayer + " wins! Good job! See you next time");
                break; 
            }

            if (isBoardFull(board)) {
                printBoard(board); 
                
                System.out.println("Nooo way! The game is a draw! lets play again!");
                break; 
            }

           
            
            currentPlayer = (currentPlayer == '♥') ? '♡' : '♥';
        }

        scanner.close(); 
    }

    private static void printBoard(char[][] board) {
        System.out.println("  0   1   2 ");
        System.out.println(" +---+---+---+");
        for (int i = 0; i < board.length; i++) {
            System.out.print(i + " |"); 
            for (int j = 0; j < board[i].length; j++) {
                System.out.print(" " + board[i][j] + " |"); 
            }
            System.out.println(); 
            System.out.println(" +---+---+---+");   
        }
    }

  
    private static boolean checkWin(char[][] board, char player) {
        for (int i = 0; i < 3; i++) {
            if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) || 
                (board[0][i] == player && board[1][i] == player && board[2][i] == player)) { 
                return true;
            }
        }


        if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) || 
            (board[0][2] == player && board[1][1] == player && board[2][0] == player)) { 
            return true;
        }

        return false; // No win
    }


    private static boolean isBoardFull(char[][] board) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[i].length; j++) {
                if (board[i][j] == ' ') { 
                    
                    return false; 
                }
            }
        }
        return true; // The board is full
    }
}

