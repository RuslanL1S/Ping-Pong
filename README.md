# Ping-Pong
from pygame import *
from random import randint

clock = time.Clock()

speed_x=3
speed_y=3

img_back = 'grass.jpg'
img_rok = 'rocketka.png'
img_rok1 = 'rocketka1.png'
img_ball='tyagi.png'

score=0
goal=10
lost=0

#класс-родитель для спрайтов
class GameSprite(sprite.Sprite):
   #конструктор класса
   def __init__(self, player_image, player_x, player_y,size_x, size_y, player_speed):
       sprite.Sprite.__init__(self)
       # каждый спрайт должен хранить свойство image - изображение
       self.image = transform.scale(image.load(player_image), (size_x, size_y))
       self.speed = player_speed
       # каждый спрайт должен хранить свойство rect - прямоугольник, в который он вписан
       self.rect = self.image.get_rect()
       self.rect.x = player_x
       self.rect.y = player_y


   def reset(self):
       window.blit(self.image, (self.rect.x, self.rect.y))

    
#класс-наследник для спрайта-игрока (управляется стрелками)
class Player(GameSprite):
    def update(self):
        keys = key.get_pressed()
        if keys[K_DOWN]:
            self.rect.y += self.speed
        if keys[K_UP]:
            self.rect.y -= self.speed
    def up(self):
        keys = key.get_pressed()
        if keys[K_s]:
            self.rect.y += self.speed
        if keys[K_w]:
            self.rect.y -= self.speed


#Игровая сцена:
win_width = 700
win_height = 500
window = display.set_mode((win_width, win_height))
display.set_caption("ping")
background = transform.scale(image.load("grass.png"), (win_width, win_height))

rok1 = Player(img_rok, 1, 250, 45, 100, 6)
rok = Player(img_rok1, 655, 250, 45, 100, 6)
ball = Player(img_ball,350,250,45,100,6)


finish = False
game = True
while game:
    for e in event.get():
        if e.type == QUIT:
            game=False
    if finish != True:
        window.blit(background, (0, 0))
        rok1.reset()
        rok1.update()
        rok.reset()
        rok.up()
        ball.reset()
        ball.rect.x += speed_x
        ball.rect.y += speed_y
        if ball.rect.y > win_height-50 or ball.rect.y < 0:
            speed_y *= -1
        if sprite.collide_rect(rok,ball) or sprite.collide_rect(rok1,ball):
            speed_x *= -1
        if ball.rect.x < 0 :
            ball.rect.x = 350
        if ball.rect.x > 650:
            ball.rect.x = 350
    display.update()
    clock.tick(60)

____________________________________________________________________________________________________________________
в данной игре под назвынием "ping-pong" можно играть вдвоем за счет управления двумя рокетками сразу ,что бы управлять левой рокеткой надо нажимать стрелочки вверх и вниз,а что бы управлять правой рокеткой нужно нажимать на клавиши "w" and "s" данный скрипт прописан в "Class Player", В этой игре есть мяч "бархатные тяги". 
