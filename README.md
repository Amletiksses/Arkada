import pygame 

win_width = 900
win_height = 700
FPS = 60
move_right = False
move_left = False
view_right = True 

X, Y = 0, 0
global X, Y

win = pygame.display.set_mode((win_width, win_height))
pygame.display.set_caption("А Р К А Д А")
clock = pygame.time.Clock()

class GameSprite(pygame.sprite.Sprite):
    def __init__(self, img_pic, img_x, img_y, img_width, img_height, img_speed)
        self.image = pygame.image.load(img_pic)
        self.image = pygame.transform.scale(self.image, (img_width, img_height))
        self.rect = self.image.get_rect()
        self.rect.x = img_x
        self.rect.y = img_y

    def reset(self, x, y):
        win.blit(self.image, (x,y))

    def moving_right(self):
        global X
        X -= 5

    def moving_left(self):
        global X
        X += 5

class Player(GameSprite):
    def update(self):
        keys = pygame.key.get_pressed()
        if keys[pygame.K_RIGHT]:
            self.rect.x += 5
        if keys[pygame.K_LEFT]:
            self.rect.x -= 5

objects = list()
scense = GameSprite('wood.jpg', 0, 0, 4000, 700, 0)
objects.appened(scene)
hero = Player('hero.png', 250, 420, 70, 120, 5)

game = True
finish = False
while game:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game = False
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_RIGHT:
                if not view_right:
                    hero.image = pygame.transform.flip(hero.image, True, False)
                    view_right = False
                move_right = True
            if event.key == pygame.K_LEFT:
                if view_right:
                    hero.image = pygame.transform.flip(hero.image, True, False)
                    view_right = True
                move_right = True
            if event.type == pygame.KEYUP:
                if event.key == pygame.K_RIGHT:
                    move_right = False
                if event.key == pygame.K_LEFT:
                    move_left = False

        if move_right and X > -3100:
            for objects in objects:
                objects.moving_right()
        else:
            pass

        if move_rleft and X < 0:
            for objects in objects:
                objects.moving_left()
        else:
            pass

        for objects in objects:
            objects.recet(X,Y)

        hero.update()
        hero.reset(X + hero.rect.x, Y)

        pygame.display.update()
        clock.tick(FPS)


        hero.update()
        hero.reset(X + hero.rect.x)
