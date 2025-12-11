# КАРКАС ПРИЛОЖЕНИЯ, FPS
```py
import pygame
pygame.init() # ввод pygame
pygame.display.set_mode((600, 400), pygame.RESIZABLE) # создание окна
pygame.display.set_caption('Змейка') # изменение имени окна
clock = pygame.time.clock()
FPS = 60
while True:
    for event in pygame.event.get(): # ссылка на событие
        if event.type == pygame.QUIT: # проверка является ли event выходом из программы
            exit()
    clock.tick(FPS)  # ввод фпс(кадров в секунду)
```
# РИСОВАНИЕ ГРАФИЧЕСКИХ ПРИМИТИВОВ
```py
import pygame
pygame.init()

W, H = 600, 400
WHITE = (255, 255, 255)
RED =(255, 0, 0)
BLUE = (0, 0, 255)
GREEN = (0, 255, 0)
sc = pygame.display.set_mode(W, H)
pygame.draw.rect(sc, WHITE, (10, 10, 50, 100)) # рисует прямоугольник (плоскость, цвет, (начальные координаты, конечные координаты))
pygame.draw.line(sc, BLUE, (200, 20), (350, 50)) # рисует линию
pygame.draw.lines(sc, GREEN, True, [(200, 80), (250, 80), (300, 200)])
pygame.display.flip() # переворачивает экран для показа другой стороны(буферизация)
```
# ОБРАБОТКА СОБЫТИЙ ОТ КЛАВИАТУРЫ
```py
import pygame
pygame.init()
W, H = 600, 400
WHITE = (255, 255, 255)
RED =(255, 0, 0)
BLUE = (0, 0, 255)
GREEN = (0, 255, 0)
sc = pygame.display.set_mode(W, H)
clock = pygame.time.clock()
FPS = 60
x = W // 2
y = H // 2
speed = 5
while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            exit()
        elif event.type == pygame.KEYDOWN:  # проверка нажатия клавиши на клавиатуре
            if event.key == pygame.K_LEFT: # проверка КАКАЯ клавиша была нажата
                x -= speed
            elif event.key == pygame.K_RIGHT:
                x += speed                  # правая клавиша - движение вправо, левая клавиша - движение влево
    sc.fill(WHITE)
    pygame.draw.rect(sc, BLUE, (x, y, 10, 20))
    pygame.display.update
```
```py
import pygame
pygame.init()
W, H = 600, 400
WHITE = (255, 255, 255)
RED =(255, 0, 0)
BLUE = (0, 0, 255)
GREEN = (0, 255, 0)
sc = pygame.display.set_mode(W, H)
clock = pygame.time.clock()
FPS = 60
x = W // 2
y = H // 2
speed = 5
while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            exit()
    keys = pygame.key.get_pressed()      # вариант проще
    if keys[pygame.K_LEFT]:
        x -= speed
    elif keys[pygame.K_RIGHT]:
        x += speed
    sc.fill(WHITE)
    pygame.draw.rect(sc, BLUE, (x, y, 10, 20))
    pygame.display.update
```
# СОЗДАНИЕ ПОВЕРХНОСТЕЙ/SURFACE
```py
import pygame
pygame.init()
W, H = 600, 400
WHITE = (255, 255, 255)
RED =(255, 0, 0)
BLUE = (0, 0, 255)
GREEN = (0, 255, 0)

clock = pygame.time.clock()
FPS = 60

surf = pygame.Surface((200, 200))  # создание плоскости
surf.fill(RED)
pygame.draw.circle(surf, GREEN, (100, 100), 80)

surf_alpha = pygame.Surface((W, 100))           #создание поверхности surf_alpha
pygame.draw.rect(surf_alpha, BLUE, (0, 0, W, 100))
surf_alpha.set_alpha(128)               # прозрачность поверхности surf_alpha
# если surf_alpha по ширине и высоте больше чем surf, то она будет обрезаться
sc.blit(surf, (50, 50))   # с помощью blit отображение плоскости
pygame.display.update()

while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            exit()
    clock.tick(FPS)
```
# МИНИ-АНИМАЦИЯ
```py
import pygame
pygame.init()
W, H = 600, 400
WHITE = (255, 255, 255)
RED =(255, 0, 0)
BLUE = (0, 0, 255)
GREEN = (0, 255, 0)

clock = pygame.time.clock()
FPS = 60

surf = pygame.Surface((W, 200))   # СОЗДАНИЕ ПОВЕРХНОСТЕЙ
bita = pygame.Surface(50, 10)

surf.fill(BLUE)
bita.fill(RED)

bx, by = 0, 150
x, y = 0, 0

while 1:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            exit()
    surf.fill(BLUE)             # закрашивает поверхность в синий(под bita)
    surf.blit(bita, (bx, by))
    if bx < W:
        bx += 5         # увеличивает координату bx пока она меньше ширины окна
    else:
        bx = 0          # как только выходит за пределы ширины, координата обнуляется
    if y < H:
        y += 1          # увеличивает координату y пока она меньше высоты окна
    else:
        y = 0         
    sc.fill(WHITE) 
    sc.blit(surf, (x, y))       # отображается в клиентской области в пределах поверхности surf
    pygame.display.update()

    clock.tick(FPS)
```
# МОДУЛИ IMAGE И TRANSFORM
```py
pygame.image.get_extended() #если выводит True то можно использовать PNG и JPEG, если False то можно использовать ТОЛЬКО bmp
#для искусственных изображений PNG, для фотореалистичных JPEG
```
```py
import pygame
pygame.init

W, H = 600, 400

sc = pygame.display.set_mode((600, 400))

clock = pygame.time.Clock()
FPS = 60

WHITE = (255, 255, 255)
RED = (255, 0, 0)
YELLOW = (239, 228, 176)

print(pygame.image.get_extended()) # если выводит 1 то True, если 0 то False
car_surf = pygame.image.load('images/car.bmp') #в подкаталоге с файлом с кодом, должна находится картинка|load - возвращает поверхность на которой нарисовано изображение
car_rect = car_surf.get_rect(center = (W//2, H//2)) # за счет get_rect и center выводит картинку посередине окна
car_surf.set_colorkey((255, 255, 255)) # делает белый цвет ПРОЗРАЧНЫМ

bg_surf = pygame.image.load('images/sand.jpg')
finish_surf = pygame.image.load('images/finish.png') # если изображение имеет прозрачный фон, то .set_colorkey не нужен
car_surf = pygame.image.load('images/car.bmp').convert() # .convert() преобразовывает пиксели в нужный формат
finish_surf = pygame.image.load('images/finish.png').convert_alpha() # .convert_alpha() используется т.к. присутствует прозрачный фон
# .convert() помогает загружать изображения быстрее
car_up = car_surf
car_down = pygame.transform.flip(car_surf, 0, 1)
car_left = pygame.transform.rotate(car_surf, 90)
car_right = pygame.transform.rotate(carsurf, -90)

car_rect = car_surf.get_rect(center=(W//2, H//2))
car_surf.set_colorkey((255, 255, 255))

bg_surf = pygame.transform.scale(bg_surf, (bg_surf.getwidth()//3, bg_surf.get_height()//3)) # размеры уменьшает в 3 раза



pygame.transform.scale(Surface, (width, height), DestSurface = None) # масштабирует изображение

car = car_up
speed = 5

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            exit()
    bt = pygame.key.get_pressed()
    if bt[pygame.K_LEFT]:
        car = car_left
        car_rect.x -= speed
        if car_rect.x < 0:
            car_rect.x = 0
        elif bt[pygame.K_RIGHT]:
        car = car_right
        car_rect.x += speed
        if car_rect.x > W-car_rect.height:
            car_rect.x = W-car_rect.height
    elif bt[pygame.K_UP]:
        car = car_up
        car_rect.y -= speed
        if car_rect.y < 0:
            car_rect.y = 0
    elif bt[pygame.K_DOWN]:
        car = car_down
        car_rect.y += speed
        if car_rect.y > H-car_rect.height:
            car_rect.y = H-car_rect.height
# W-car_rect.height нужна для того чтобы машинка не выходила за края
# чтобы изображение машинки было без белого фона, нужно часть кода с .set_colorkey() вставить перед частью с настройкой передвижения машинки(car_up = car_surf car_down = pygame.transform.flip(car_surf, 0, 1) car_left = pygame.transform.rotate(car_surf, 90) car_right = pygame.transform.rotate(carsurf, -90))
    clock.tick(FPS)
```