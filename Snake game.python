# Draft
import pygame
import random

class base:
    def __init__(self, x, y, width, height, color):
        self.x = x
        self.y = y
        self.width = width
        self.height = height
        self.color = color

    def draw(self):
        left = self.x - self.width / 2
        top = self.y - self.height / 2
        self.rect = pygame.Rect(left, top, self.width, self.height)
        pygame.draw.rect(window, self.color, self.rect)

class player(base):
    def __init__(self, x, y, width, height, color, speed, is_head):
        super().__init__(x, y, width, height, color)
        self.length = 1
        self.speed = speed
        self.is_head = is_head
        self.parent = None
        self.child = None
        self.previous_x = 0
        self.previous_y = 0
        

    def move(self):
        global snake_moved
        self.previous_x = self.x
        self.previous_y = self.y
        if self.is_head:
            
            keys = pygame.key.get_pressed()
            if keys[pygame.K_LEFT]:
                self.x -= self.speed
                snake_moved = True
            elif keys[pygame.K_RIGHT]:
                self.x += self.speed
                snake_moved = True
            elif keys[pygame.K_UP]:
                self.y -= self.speed
                snake_moved = True
            elif keys[pygame.K_DOWN]:
                self.y += self.speed
                snake_moved = True
            else:
                snake_moved = False
        else:
            if snake_moved:
                self.x = self.parent.previous_x
                self.y = self.parent.previous_y

    def add_child(self):
        someone_we_currently_check = self
        while someone_we_currently_check.child is not None:
            someone_we_currently_check = someone_we_currently_check.child
        new_child = player(self.x - 100, self.y - 100, self.width, self.height, self.color, self.speed, False)
        new_child.parent = someone_we_currently_check
        someone_we_currently_check.child = new_child


class apple(base):
    def __init__(self, x, y, width, height, color):
        super().__init__(x, y, width, height, color)

    def consumed(self):
        if self.rect.colliderect(snake.rect):
            snake.add_child()
            self.make_new_apple()

    def make_new_apple(self):
        self.x = random.randint(0, screen_size)
        self.y = random.randint(0, screen_size)

class obstacle(base):
    def __init__(self, x, y, width, height, color):
        super().__init__(x, y, width, height, color)

    def check_collided_with_snake(self):
        if self.rect.colliderect(snake.rect):
            print("game over!")


# ---------- Pygame template start ------------------------
pygame.init()
global window, screen_size
screen_size = 600
window = pygame.display.set_mode((screen_size,screen_size))
pygame.display.set_caption("pygame template")
run = True
print("going into the loop")

snake = player(300, 300, 10, 10, "green", 10, True)
test_apple = apple(100, 100, 10, 10, "red")
test_wall = obstacle(500, 500, 10, 100, "grey")

while run:
    window.fill((0,0,0))
    snake.move()
    snake.draw()
    temporary_snake = snake
    while temporary_snake.child is not None:
        temporary_snake.child.draw()
        temporary_snake.child.move()
        temporary_snake = temporary_snake.child

    test_apple.draw()
    test_apple.consumed()
    test_wall.draw()
    test_wall.check_collided_with_snake()

    pygame.display.update()
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            print("closing the game")
            run = False
    pygame.time.delay(20)
pygame.quit()

