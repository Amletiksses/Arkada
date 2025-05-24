import pygame

win_width = 900
win_height = 700
FPS = 60
move_right = False
move_left = False
move_up = False
view_right = True
x_fon = 0

win = pygame.display.set_mode((win_width,win_height))
pygame.display.set_caption('АРКАДА')
clock = pygame.time.Clock()

class GameSprite(pygame.sprite.Sprite):
    def __init__(self, img_pic, img_x, img_y, img_width, img_height, img_speed):
        self.image = pygame.transform.scale(pygame.image.load(img_pic), (img_width, img_height))
        self.rect = self.image.get_rect()
        self.rect.x = img_x
        self.rect.y = img_y
        self.speed = img_speed

    def reset(self):
        win.blit(self.image, (self.rect.x, self.rect.y))

    def right(self):
        #global x_fon
        self.rect.x -= 5  
        
    def left(self):
        #global x_fon
        self.rect.x += 5  
            
class Player(GameSprite):
    def right(self):
        self.rect.x += 5
    def left(self):
        self.rect.x -= 5

hero = Player('hero.png', 250, 420, 70, 120, 5)
objects = []        
scene = GameSprite('wood.jpg', 0, 0, 4000, 700, 0)
enemy_1 =  GameSprite('bad_boy.png', 800, 410, 80, 135, 0)
enemy_2 =  GameSprite('bad_boy.png', 1800, 180, 80, 135, 0)
enemy_3 =  GameSprite('bad_boy.png', 3100, 410, 80, 135, 0)
girl = GameSprite('girl.png', 3400, 410, 80, 130, 0)
platforma1 = GameSprite('wall.png', 600, 300, 400, 100, 0)
platforma2 = GameSprite('wall.png', 1600, 300, 400, 100, 0)
stair1 = GameSprite('stair.png', 540, 250, 80, 310, 0)
objects.append(scene)
objects.append(stair1)
objects.append(platforma1)
objects.append(platforma2)
objects.append(enemy_1)
objects.append(enemy_2)
objects.append(enemy_3)
objects.append(girl)

game = True
finish = False

while game:
    for e in pygame.event.get():
        if e.type == pygame.QUIT:
            game = False
        if e.type == pygame.KEYDOWN:
            if e.key == pygame.K_RIGHT:
                if not view_right:
                    hero.image = pygame.transform.flip(hero.image, True, False)
                    view_right = True
                move_right = True  
            if e.key == pygame.K_LEFT:
                if view_right:
                    hero.image = pygame.transform.flip(hero.image, True, False)
                    view_right = False      
                move_left = True
            if e.key == pygame.K_UP:
                move_up = True 

        if e.type == pygame.KEYUP:
            if e.key == pygame.K_RIGHT:
                move_right = False  
            if e.key == pygame.K_LEFT:
                move_left = False
            
    if move_right:
        if x_fon < 3680:
            x_fon += 5
            if x_fon >= 0 and x_fon <= 3100:
                for el in objects:
                    el.right()
            if x_fon < 0 or x_fon > 3100:
                hero.right()
    
    if move_left:
        if x_fon > -240:
            x_fon -= 5
            if x_fon >= 0 and x_fon <= 3100:
                for el in objects:
                    el.left()
            if x_fon < 0 or x_fon > 3100:
                hero.left()
    if move_up:
        if pygame.sprite.collide_rect(hero, stair1):
                if hero.rect.y -= 5
            else:
                if hero.rect.y < 420:
        if not pygame.sprite.collide_rect(hero, platforma1) or pygame.sprite.collide_rect(hero, platforma2):
            hero.rect.y += 5



    for el in objects:
        el.reset()
    hero.reset()

    pygame.display.update()
    clock.tick(FPS)
        pygame.display.update()
        clock.tick(FPS)
