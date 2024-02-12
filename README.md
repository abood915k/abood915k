- 👋 Hi, I’m @abood915k
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
abood915k/abood915k is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
import random

# تهيئة الشاشة
WIDTH, HEIGHT = 800, 600
WIN = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Battle Royale Game")

# تهيئة الألوان
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)

# تهيئة اللاعب والعدو
PLAYER_SIZE = 50
player_x = WIDTH // 2 - PLAYER_SIZE // 2
player_y = HEIGHT - PLAYER_SIZE - 10
enemy_size = 50
enemy_x = random.randint(0, WIDTH - enemy_size)
enemy_y = 10

# سرعة اللاعب والعدو
player_speed = 5
enemy_speed = 2

# Loop الرئيسي
run = True
while run:
    WIN.fill(WHITE)
    pygame.time.delay(50)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False

    # حركة اللاعب
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x - player_speed > 0:
        player_x -= player_speed
    if keys[pygame.K_RIGHT] and player_x + player_speed + PLAYER_SIZE < WIDTH:
        player_x += player_speed

    # حركة العدو
    enemy_y += enemy_speed
    if enemy_y > HEIGHT:
        enemy_y = 0
        enemy_x = random.randint(0, WIDTH - enemy_size)

    # اصطدام اللاعب بالعدو
    player_rect = pygame.Rect(player_x, player_y, PLAYER_SIZE, PLAYER_SIZE)
    enemy_rect = pygame.Rect(enemy_x, enemy_y, enemy_size, enemy_size)
    if player_rect.colliderect(enemy_rect):
        print("Game Over")
        run = False

    # رسم اللاعب والعدو
    pygame.draw.rect(WIN, RED, (player_x, player_y, PLAYER_SIZE, PLAYER_SIZE))
    pygame.draw.rect(WIN, GREEN, (enemy_x, enemy_y, enemy_size, enemy_size))

    pygame.display.update()

pygame.quit()
