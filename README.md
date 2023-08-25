# Game1
import pygame
import sys

# Initialize Pygame
pygame.init()

# Game Constants
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
PLAYER_SIZE = 40
OBSTACLE_SIZE = 30
GOAL_SIZE = 50
FPS = 60

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)
GREEN = (0, 255, 0)

# Create the screen
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Simple 2D Game")

clock = pygame.time.Clock()

# Player
player_x = 50
player_y = SCREEN_HEIGHT // 2 - PLAYER_SIZE // 2
player_speed = 5

# Obstacle
obstacle_x = SCREEN_WIDTH - 100
obstacle_y = SCREEN_HEIGHT // 2 - OBSTACLE_SIZE // 2

# Goal
goal_x = SCREEN_WIDTH - GOAL_SIZE - 10
goal_y = SCREEN_HEIGHT // 2 - GOAL_SIZE // 2

# Main Loop
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    if keys[pygame.K_UP] and player_y > 0:
        player_y -= player_speed
    if keys[pygame.K_DOWN] and player_y < SCREEN_HEIGHT - PLAYER_SIZE:
        player_y += player_speed

    # Check collision with obstacle
    if player_x + PLAYER_SIZE > obstacle_x and player_y + PLAYER_SIZE > obstacle_y and player_y < obstacle_y + OBSTACLE_SIZE:
        running = False

    # Check reaching the goal
    if player_x + PLAYER_SIZE > goal_x and player_y + PLAYER_SIZE > goal_y and player_y < goal_y + GOAL_SIZE:
        running = False

    # Rendering
    screen.fill(WHITE)
    pygame.draw.rect(screen, GREEN, (player_x, player_y, PLAYER_SIZE, PLAYER_SIZE))
    pygame.draw.rect(screen, RED, (obstacle_x, obstacle_y, OBSTACLE_SIZE, OBSTACLE_SIZE))
    pygame.draw.rect(screen, BLACK, (goal_x, goal_y, GOAL_SIZE, GOAL_SIZE))
    pygame.display.flip()

    clock.tick(FPS)

pygame.quit()
sys.exit()
