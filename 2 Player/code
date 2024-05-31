import pygame as pg
from pygame.locals import *
pg.init()

#objects
sym = 'x'
winner = None
draw = None
height = 400
width = 400
x_img = pg.image.load('cross.png')
o_img = pg.image.load('circle.png')
board = [[None]*3,[None]*3,[None]*3]

#screen display
screen = pg.display.set_mode((width, height+100))
screen.fill('white')
#resizing image
x_img = pg.transform.scale(x_img, (50, 50))
o_img = pg.transform.scale(o_img, (50, 50))

#creating our grid
def game_init():
    line_colour = ('black')
    #draw vertical lines
    pg.draw.line(screen, line_colour, (width/3 , 0), (width/3, height),7)
    pg.draw.line(screen, line_colour, (width/3*2 , 0), (width/3*2, height),7)
    #draw horizontal lines
    pg.draw.line(screen, line_colour, (0, height/3), (width, height/3),7)
    pg.draw.line(screen, line_colour, (0, height/3*2 ), (width, height/3*2),7)
    status()
#get mouse click coordinate
def click():
    x , y = pg.mouse.get_pos()
    print(1)
    if (x < width/3) : 
        col = 1
    elif (width/3 < x < width/3*2):
        col = 2
    elif (width/3*2 < x < width):
        col = 3
    else:
        col = None
    if (y < height/3):
        row = 1
    elif (height/3 < y < height/3*2):
        row = 2
    elif (height/3*2 < y < height):
        row = 3
    else: 
        row = None
    if board[row-1][col-1] is None:
        XO(row, col)
        win()

#blit user image
def XO(row,col):
    global sym, board
    if col == 1:
        posx = 30
    if col == 2:
        posx = width/3 + 30
    if col == 3:
        posx = width/3*2 + 30
    if row == 1 :
        posy = 30
    if row == 2:    
        posy = height/3 + 30
    if row == 3: 
        posy = height/3*2 + 30
    #blitting 
    board[row-1][col-1] = sym
    if sym == 'x':
        screen.blit(x_img, (posx, posy))
        sym = 'o'
    else:
        screen.blit(o_img, (posx, posy))
        sym = 'x'
    pg.display.update()

#checking for winning condition
def win():
    global draw , winner, board
    #row win
    for row in range(0,3):
        if ((board[row][0] == board[row][1] == board[row][2]) and (board[row][0] is not None)) :
            winner = board[row][0]
            pg.draw.line(screen, (255, 255, 0), 
                         (0, (row + 1)*height / 3 - height / 6), (width, (row + 1)*height / 3 - height / 6),
                         4)
            break
    #column win
    for col in range(0,3):
        if ((board[0][col] == board[1][col] == board[2][col]) and (board[0][col] is not None)) :
            winner = board[0][col]
            pg.draw.line(screen, (255, 255, 0), 
                         ((col + 1) * width / 3 - width / 6, 0), ((col + 1) * width / 3 - width / 6, height), 
                         4)
            break
    #diagonal win
    #right to left
    if ((board[0][0] == board[1][1] == board[2][2]) and (board[0][0] is not None)):
        winner = board[0][0]
        pg.draw.line(screen, (255,255,0), 
                     (50, 50), (350, 350), 
                     4)
    #left to right
    if ((board[0][2] == board[1][1] == board[2][0]) and (board[0][2] is not None)):
        winner = board[0][2]
        pg.draw.line(screen, (255,255,0), 
                     (350, 50), (50, 350), 
                     4)

    if (winner is None and all([all(row) for row in board])):
        draw = True
    status()

#checking if have winner or draw or still ongoing. note that this has to happen every move
def status():
    global draw, sym, winner
    if winner == None:
        message = sym + "'s turn"
    else:
        message = winner + " won"
    if draw==True: #means that variable draw holds something
        message = "draw"
    #getting our message to display
    font = pg.font.Font(None, 32)
    text = font.render(message, 1, (255,255,255))
    screen.fill((0, 0, 0), (0, 400, 500, 100))
    text_rect = text.get_rect(center=(width/2, height+50))
    screen.blit(text, text_rect)
    pg.display.update()

while True:
    game_init()
    for event in pg.event.get():
        if event.type == pg.QUIT:
            pg.quit()
        elif event.type == pg.MOUSEBUTTONDOWN:
            click()
    pg.display.update()
