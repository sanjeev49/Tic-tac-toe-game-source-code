# Tic-tac-toe-game-source-code
This game is created by Sanjeev Kumar
#1. Print a 3*3 board
from IPython.display import clear_output
def display_board(board):
    clear_output() # This will only work in jupyter notebook
    
    print('   |   |')
    print(' '+ board[7]+ ' | ' + board[8]+ ' | ' + board[9])
    print('--------------')
    print('   |   |')
    print(' '+board[4]+' | '+board[5]+' | '+board[6])
    print('--------------')
    print(' '+board[1]+' | '+ board[2]+' | '+board[3])
    print('   |   |')
    


#step2 Function to take input from user up to x or o'''
def player_input():
    marker = ''
    while not(marker == 'X' or marker == 'O'):
        marker = input('Player1: Do you want to be X or O? ').upper()
    if marker == 'X':
            return ('X', 'O')
    else:
            return ('O','X')

#step3: run the palce_maker fuction using test parameters and display the modified board
def place_marker(board, marker, position):
    board[position]= marker
    


#Step4.Check if someone has won the game
def win_check(board,mark):
    return((board[7]== mark and board[8] == mark and board[9] == mark) or #Check for upper row
           (board[4]== mark and board[5]== mark and board[6]== mark) or #Check for middle row
           (board[1]== mark and board[2]== mark and board[3]== mark) or #Check for lower row
           (board[7]== mark and board[4]== mark and board[1]== mark) or #Check for 1st column
           (board[8]== mark and board[5]== mark and board[2]== mark) or #Chekc for middle column
           (board[9]== mark and board[6]== mark and board[3]== mark) or #Check for last column
           (board[7]== mark and board[5]== mark and board[3]== mark) or #chekc for diagonal column
           (board[1]== mark and board[5]== mark and board[9] == mark))

#step 5. A fucntion to choose randomly which player goes first
import random
def choose_first():
    if random.randint(0,1) == 0:
        return 'Player2'
    else:
        return 'Player1'
    
#step6: A function which Check if there is a blank space return boolean
def space_check(board, position):
    return board[position]== ' '

#Step 7. A fuction that checks if board is already full and return boolean True for full else False
def full_board_check(board):
    for i in range(1,10):
        if space_check(board,i):
            return False
    return True

#step 8. A fucntion that asks for player next position between (1-9) and then use the funtion form step6 to check if free posi.
#then return the function for later use'''
def player_choice(board):
    position = 0
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board,position):
        position = int(input("Choose your next positon:(1-9)"))
    return position



#step9 asks for replays
def re_plays():
    return input("Do you want to paly agian answer in yes /or no: ").lower().startswith('y')

#step10: Functions and loops to run the game
print("Welcome to TIC TAC TOE!!!")
while True:
    #Reset the board
    theboard = [' '] * 10
    player1_marker , player2_marker = player_input()
    turn = choose_first()
    print(turn + ' will go first. ')
    
    
    play_game = input("Are you ready to play? Enter Yes or No. ")
    
    if play_game.lower()[0] == 'y':
        game_on = True
    else:
        game_on = False
        
        
    while game_on:
        if turn == 'Player1':
            #Player1, turn
            
            
            display_board(theboard)
            position = player_choice(theboard)
            place_marker(theboard ,player1_marker, position)
            
            
            if win_check(theboard, player1_marker):
                display_board(theboard)
                print("Congratulations! Player1 has  won the game")
            
                game_on = False
            else:
                if full_board_check(theboard):
                    display_board(theboard)
                    print("The game is draw")
                
                    break
                else:
                    turn = "Player2"
                
           
               
        else:
            #Player2 turn
            
            
            display_board(theboard)
            position = player_choice(theboard)
            place_marker(theboard,player2_marker, position)
            
            
            if win_check(theboard,player2_marker):
                display_board(theboard)
                print("Congratulatiosn Player2 has won!!!")
                game_on = False
            else:
                if full_board_check(theboard):
                    display_board(theboard)
                    print('The game is a draw')
                    break
                else:
                    turn = 'Player1'
    if not re_plays():
        break

