# lol
import pygame

class sq():
    def __init__(self, life):
        self.life = life
    def get_life(self):
        return self.life
    def chenge(self, life):
        self.life = life

Size = 700
sc = pygame.display.set_mode([Size, Size])

pos = [[sq(0) for i in range(100)] for _ in range(100)]

for i in range(100):
    for j in range(100):
        if i % 3 != 0:
            pos[i][j].chenge(1)

clr = ['#ff0000', '#ffa500', '#ffff00', '#008000', '#42aaff', '#0000ff', '#8b00ff']

change = [[0, 1], [1, 0], [-1, 0], [0, -1], [1, 1], [1, -1], [-1, 1], [-1, -1]]

while 1:
    sc.fill(pygame.Color('black'))
    for i in range(100):
        for j in range(100):
            if pos[i][j].get_life() == 1:
                pygame.draw.rect(sc, pygame.Color(clr[abs(i - j) % 7]), (i * 7, j * 7, 7, 7))
            else:
                pygame.draw.rect(sc, pygame.Color('black'), (i * 7, j * 7, 7, 7))

    b = [[sq(0) for i in range(100)] for _ in range(100)]
    for i in range(100):
        for j in range(100):
            cnt = 0
            for ch in change:
                nwi = i + ch[0]
                nwj = j + ch[1]
                if (nwi < 0 or nwi >= 100 or nwj < 0 or nwj >= 100):
                    continue
                else:
                    if pos[nwi][nwj].get_life() == 1:
                        cnt += 1
            if pos[i][j].get_life() == 1:
                if cnt == 2 or cnt == 3:
                    b[i][j].chenge(1)
            elif (cnt == 3):
                b[i][j].chenge(1)
    b, pos = pos, b
    pygame.display.flip()
    pygame.time.wait(100)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            exit()