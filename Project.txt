#IMPORTING REQUIRED MODULES


from random import *

import pygame

from pygame import *

import time

mixer.init(frequency=22050, size=-16, channels=2, buffer=512)

#VARIABLES INITIALISATION

init()

out_y = 450

red = (200, 0, 0)

white = (255, 255, 255)

black = (0, 0, 0)

tile_fade = 30

tile_color = 500

font_start_x = 0

#IMAGE IMPORTING

bg_main = image.load( "bg_main.png" )

bg_over = image.load( "Game_over.png" )

bg_over2 = image.load( "Game_over2.png" )

#VARIABLES: FONTS

font_size = 40

text = font.SysFont(None, 35)

score = font.SysFont(None, font_size)

text_start = font.SysFont(None, 0)

color_fade = (235, 235, 235)

light_grey = (230, 230, 230)

clock = pygame.time.Clock()

screen = display.set_mode((280, 450))

display.set_caption( " Piano Tiles " )

#VARIABLES: CO-ORDINATES

line_1_start_pos = (70, 0)

line_1_end_pos = (70, 500)

line_2_start_pos = (140, 0)

line_2_end_pos = (140, 500)

line_3_start_pos = (210, 0)

line_3_end_pos = (210, 500)

line_4_start_pos = (280, 0)

line_4_end_pos = (280, 500)

line_width = 1

tile_width = 70

tile_height = 120

plus_one = 1

game_go = True

tile_x_new = round(randrange(0, 280) / 70.0) * 70.0

tile_y_new = -120

tile_false = Surface((tile_width, tile_height))

tile_falseX = 0

score_x = 140

score_y = 10

alp = 0

tile_falseY = 0

FPS = 300

#VARIABLES : SCORE TEXT

file_score = open( "C:\Users\V.I.S\Desktop\Gaurav\Piano Tiles\score.txt","w" )

score_txt = 0

score_str = "score : " + str(score_txt)




#FUNCTIONS

def game_run():

    global game_go

    game_go = True


def game_stop():

    global game_go

    game_go = False


def bg_music():

    music_bg = mixer.Sound( "Sound2.ogg" )

    channel = music_bg.play(-1, 0, 0)

    if channel.get_busy():

        pygame.time.wait(100)


def game_exit():
    
    pygame.quit()
    #file_score = open( "C:\Users\V.I.S\Desktop\Gaurav\Piano Tiles\score.txt","w" )
    #file_score.close()
    exit()

def restart():
    #bg_main = image.load ( "bg_main_2.png" )
    screen.blit(bg_main,(0,0))

def add_score_to_file():  

    global file_score , score_txt , score_str

    file_score = open( "C:\Users\V.I.S\Desktop\Gaurav\Piano Tiles\score.txt","w" )

    score_txt += 1

    score_str = "score : " + str(score_txt)

    file_score.write(score_str)

    file_score.close()
    

                
def game_start():
    
    global bg_main

    file_score = open( "C:\Users\V.I.S\Desktop\Gaurav\Piano Tiles\score.txt","w" )

    file_score.close()

    time1 = time.time()
    
    #bg_music()

    Exit = False

    start1 = False

    game_score = 0

    touch1 = 500

    touch2 = 500

    touch3 = 500

    touch4 = 500

    touch5 = 500

    tile1_X = 0

    tile1_Y = 0

    tile2_X = 210
    tile2_Y = -120

    tile3_X = 140
    tile3_Y = -280

    tile4_X = 70
    tile4_Y = -400

    tile5_X = 0
    tile5_Y = -520

    tile_end = 520

    while not Exit:

        global score_x, score_y, line_width, game_go, font_size, tile_fade, tile_falseX, tile_false, tile_falseY, game_go, FPS ,alp ,out_y,font_start_x

        condition = False

        mouse_cord = mouse.get_pos()
        
        if start1:

            font_start_x = -100

            tile1_Y += plus_one

            tile2_Y += plus_one

            tile3_Y += plus_one

            tile4_Y += plus_one

            tile5_Y += plus_one

            FPS += 0.01

            if 110 < mouse_cord[0] <= 170:

                if 400 < mouse_cord[1] <= 470:

                    if process.type == MOUSEBUTTONDOWN:

                        bg_main = image.load ( "bg_main.png" )

                        font_start_x = -100

                        start1 =  False

        if game_score >= 10:
            
            score_x = 125

        if game_score >= 100:
            
            score_x = 115
               
        def tile_x_random():
            
            global tile_x_new
            
            tile_x_new = round(randrange(0, 210) / 70.0) * 70.0

        def score_org1(score_org):
            
            main_score = score.render(score_org, True, red)
            
            screen.blit(main_score, [score_x, score_y])

        def start(start_game):
            
            main_start = score.render(start_game, True, white)
            
            screen.blit(main_start, [font_start_x, 40])
            
        """def sound():
            main_sound = mixer.Sound("Sound.ogg")
            main_sound.play()"""

        for process in event.get():
            
            if process.type == QUIT:
                
                game_exit()
        
            if process.type == MOUSEBUTTONDOWN:
                
                start1 = True

                if tile1_X <= mouse_cord[0] <= tile1_X + tile_width:
                    
                    if tile1_Y <= mouse_cord[1] <= tile1_Y + tile_height:
                        
                        if touch1 == tile_color:
                            
                            touch1 = tile_fade
                            
                            game_score += plus_one
                            
                            condition = True
                            
                            bg_main = image.load("bg_main_2.png")
                            
                            add_score_to_file()
                            

                if tile2_X <= mouse_cord[0] <= tile2_X + tile_width:
                    
                    if tile2_Y <= mouse_cord[1] <= tile2_Y + tile_height:
                        
                        if touch2 == tile_color:
                            
                            touch2 = tile_fade
                            
                            game_score += plus_one
                            
                            condition = True
                            
                            bg_main = image.load("bg_main_2.png")
                            
                            add_score_to_file()

                            

                if tile3_X <= mouse_cord[0] <= tile3_X + tile_width:
                    
                    if tile3_Y <= mouse_cord[1] <= tile3_Y + tile_height:
                        
                        if touch3 == tile_color:
                            
                            touch3 = tile_fade
                            
                            game_score += plus_one

                            condition = True
                            
                            bg_main = image.load("bg_main_2.png")
                            
                            add_score_to_file()
                            


                if tile4_X <= mouse_cord[0] <= tile4_X + tile_width:
                    
                    if tile4_Y <= mouse_cord[1] <= tile4_Y + tile_height:
                        
                        if touch4 == tile_color:
                            
                            touch4 = tile_fade
                            
                            game_score += plus_one
                            
                            condition = True
                            
                            bg_main = image.load("bg_main_2.png")
                            
                            add_score_to_file()


                if tile5_X <= mouse_cord[0] <= tile5_X + tile_width:
                    
                    if tile5_Y <= mouse_cord[1] <= tile5_Y + tile_height:
                        
                        if touch5 == tile_color:
                            
                            touch5 = tile_fade
                            
                            game_score += plus_one
                            
                            condition = True
                            
                            bg_main = image.load("bg_main_2.png")
                            
                            add_score_to_file()

                            
                if 420 < mouse_cord[1] < 450:
                    
                        condition = True

                    
                if not condition:
                    #alp = 120
                    
                    start1 = False
                    
                    bg_main = image.load( "bg_main_org.png" )
                    
                    if 0 < mouse_cord[0] < 70:
                        
                        tile_falseX = 0

                        
                    if 70 < mouse_cord[0] < 140:
                        
                        tile_falseX = 70

                        
                    if 140 < mouse_cord[0] < 210:
                        
                        tile_falseX = 140

                        
                    if 210 < mouse_cord[0] < 280:
                        
                        tile_falseX = 210

                        
                    if 280 < mouse_cord[0] < 350:
                        
                        tile_falseX = 290

                    if 0 < mouse_cord[1] < 120:
                        
                        tile_falseY = 0

                        
                    if 120 < mouse_cord[1] < 240:
                        
                        tile_falseY = 120

                        
                    if 240 < mouse_cord[1] < 360:
                        
                        tile_falseY = 240

                        
                    if 360 < mouse_cord[1] < 420:
                        
                        tile_falseY = 360

                    game_go = False
                               
#GAME STRUTURE

        #LINES
                    
        draw.line(screen, light_grey, line_1_start_pos, line_1_end_pos, line_width)
        
        draw.line(screen, light_grey, line_2_start_pos, line_2_end_pos, line_width)
        
        draw.line(screen, light_grey, line_3_start_pos, line_3_end_pos, line_width)
        
        draw.line(screen, light_grey, line_4_start_pos, line_4_end_pos, line_width)
        
        #TILES
        
        tile_false = Surface((tile_width, tile_height))
        
        tile_false.set_alpha(alp)
        
        tile_false.fill(red)
        
        screen.blit(tile_false, (tile_falseX, tile_falseY))

        #TILE-1 SETTINGS
        
        tile1 = Surface((tile_width, tile_height))
        
        tile1.set_alpha(touch1)
        
        tile1.fill(black)
        
        screen.blit(tile1, (tile1_X, tile1_Y))

        
        #TILE-2 SETTINGS
        
        tile2 = Surface((tile_width, tile_height))
        
        tile2.set_alpha(touch2)
        
        tile2.fill(black)
        
        screen.blit(tile2, (tile2_X, tile2_Y))

        
        #TILE-3 SETTINGS
        
        tile3 = Surface((tile_width, tile_height))
        
        tile3.set_alpha(touch3)
        
        tile3.fill(black)
        
        screen.blit(tile3, (tile3_X, tile3_Y))

        
        #TILE-4 SETTINGS
        
        tile4 = Surface((tile_width, tile_height))
        
        tile4.set_alpha(touch4)

        tile4.fill(black)
        
        screen.blit(tile4, (tile4_X, tile4_Y))

        
        #TILE-5 SETTINGS
        
        tile5 = Surface((tile_width, tile_height))
        
        tile5.set_alpha(touch5)
        
        tile5.fill(black)
        
        screen.blit(tile5, (tile5_X, tile5_Y))
        

#TILE END

        if tile1_Y == tile_end:

            
            if touch1 == tile_fade:
                
                tile_x_random()
                
                tile1_Y = tile_y_new
                
                tile1_X = tile_x_new
                
                touch1 = tile_color

            else:
                
                game_go = False


        if tile2_Y == tile_end:
            
            if touch2 == tile_fade:
                
                tile_x_random()
                
                tile2_Y = tile_y_new
                
                touch2 = tile_color

            else:
                
                game_go = False


        if tile3_Y == tile_end:
            
            if touch3 == tile_fade:
                
                tile_x_random()
                
                tile3_Y = tile_y_new
                
                tile3_X = tile_x_new
                
                touch3 = tile_color


            else:
                
                game_go = False



        if tile4_Y == tile_end:
            
            if touch4 == tile_fade:
                
                tile_x_random()
                
                tile4_Y = tile_y_new
                
                tile4_X = tile_x_new
                
                touch4 = tile_color


            else:
                
                game_go = False



        if tile5_Y == tile_end:
            
            if touch5 == tile_fade:
                
                tile_x_random()
                
                tile5_Y = tile_y_new
                
                tile5_X = tile_x_new
                
                touch5 = tile_color


            else:
                
                game_go = False


#FONT SETTING & SCORE
                
        start("Start")
        
        score_org1("{}".format(game_score))
        
        display.update()
        
        clock.tick(FPS)
        
        screen.blit(bg_main, (0, 0))

        
#GAME ENDING & RESTART

        
        if not game_go:
            
            score_x = 130
            
            line_width = 0
            
            touch1 = 0
            
            touch2 = 0
            
            touch3 = 0
            
            touch4 = 0
            
            touch5 = 0
            tile1_Y = -120
            
            tile2_Y = -120
            
            tile3_Y = -120
            
            tile4_Y = -120
            
            tile5_Y = -120
            
            screen.blit(bg_over, (0, 0))
            
            mouse_cord2 = mouse.get_pos()


            #RESTARTING            
            if 99 < mouse_cord2[0] <= 176:
                
                if 290 < mouse_cord2[1] <= 346:
                    
                    if process.type == MOUSEBUTTONDOWN:
                        
                        screen.blit(bg_over2, (0, 0))
                        
                        file_score = open( "C:\Users\V.I.S\Desktop\Gaurav\Piano Tiles\score.txt","w" )
                        
                        file_score.flush()
                        
                        file_score.close()
                        
                        line_width = 1
                        
                        game_score = 0
                        
                        touch1 = 500
                        
                        touch2 = 500
                        
                        touch3 = 500

                        touch4 = 500

                        touch5 = 500

                        tile1_X = 0

                        tile1_Y = 0

                        tile2_X = 210

                        tile2_Y = -120

                        tile3_X = 140

                        tile3_Y = -280

                        tile4_X = 70

                        tile4_Y = -400

                        tile5_X = 0

                        tile5_Y = -520

                        tile_end = 520

                        font_start_x = 0

                        start1 = False  

                        game_go = True

                      
if game_go:
    
    game_start()

