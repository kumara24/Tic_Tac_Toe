import random

def place(num,x):
    for i in range(len(x)):
        if x[i] == num:
            pos = x.index(num)
            return x[(pos + 1)]
    return str(num)

def print_grid(move,player,x):

    pos_list.extend([move,player])
           
    grid = ["","-------------\n",
        "|",place(1,pos_list),"|",place(2,pos_list),"|",place(3,pos_list),"|\n",
        "|---+---+---|\n",
        "|",place(4,pos_list),"|",place(5,pos_list),"|",place(6,pos_list),"|\n",
        "|---+---+---|\n",
        "|",place(7,pos_list),"|",place(8,pos_list),"|",place(9,pos_list),"|\n",
        "-------------\n"]
    if x == 2:
        print '\n', ' '.join(grid)

def winner(x,player,xx):

    if ((1 in x and 4 in x and 7 in x)or(1 in x and 2 in x and 3 in x)or(2 in x and 5 in x and 8 in x)or(3 in x and 6 in x and 9 in x)or
    (4 in x and 5 in x and 6 in x)or(7 in x and 8 in x and 9 in x)or(1 in x and 5 in x and 9 in x)or(3 in x and 5 in x and 7 in x)):
        if xx <> 1:
            print '\n'*5,"\'%s\'" %player, "HAS WON!"
        return 1 == 1

def computer_AI_part(listx):
    global computer_move
    for x in range(1,10):
        if x not in pos_list:
            listx.append(x)
            if (winner(listx,'Computer',1)) == True:
                del listx[-1]
                computer_move = x
                return 1
            del listx[-1]

def computer_and_player():
    global computer_move,pos_list,player_list,computer_list
    replay,draw = 0,0

    while True:

        if replay == 1:
            restart = raw_input("Would you like to replay?: ")
            if restart == "yes":
                pass
            elif restart == "y":
                pass
            elif restart == "Y":
                pass
            else:
                return
        else:
            print "\nTic Tac Toe - Computer vs You", '\n'*2,"Computer goes first\n"

        replay,computer_move,players_move,loop_count,pos_list,player_list,computer_list = 0,0,0,0,[],[],[]

        for each in "XXXXX":
            loop_count += 1

            if computer_AI_part(computer_list) or computer_AI_part(player_list) == 1:
                pass     
            else:
                while True:
                    computer_move = random.randint(1,9)
                    if computer_move in pos_list:
                        continue
                    break
            computer_list.append(computer_move)
            print_grid(computer_move,'O',2)

            if loop_count == 5:
                if winner(player_list,'player',2) == True or winner(computer_list,'Computer',2) == True:
                    pass
                else:
                    print "Match Was a draw!"
                replay = 1
                break

            if winner(computer_list,'Computer',2) == True:
                replay = 1
                break

            while True:
                try:
                    players_move = int(raw_input("\n\'%s\' Enter a value from the grid to plot your move: " %each))
                    if players_move in pos_list or players_move < 1 or players_move > 9:
                        print "Enter an available number that's between 1-9"
                        continue
                    break
                except:
                    print "Enter a number"

            player_list.append(players_move)
            print_grid(players_move,each,1)

            if winner(player_list,'player',1) == True:
                print_grid(players_move,each,2)
                winner(player_list,'player',2)
                replay = 1
                break

if __name__ == "__main__":
    computer_and_player()
