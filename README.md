import pygame
import sys
from pygame.locals import *

alto = 600
ancho = 1100                                                                             #TAMAÑO DE LA VENTANA

def main():
    pygame.init()
    ventanita = pygame.display.set_mode((ancho,alto))                                    #VENTANA
    pygame.display.set_caption("Las grandes aventuras de Billy, el triangulo volador")
    
    rojo = (100,100,100)                                                                 #COLORES
    azul = (255,255,255)
    verde = (29,15,51)
    
    personaje = pygame.image.load("Bill_Cipher_PNG.webp")                                #PERSONAJE
    personaje = pygame.transform.scale(personaje,(150,200))
    mask_pj = pygame.mask.from_surface(personaje)     
    personaje_rect = personaje.get_rect()
    personaje_rect.center = (50,78)
    
    
    muro = pygame.image.load("libro.jpeg")                                               #MURO
    muro = pygame.transform.scale(muro,(95,105))
    mask_muro = pygame.mask.from_surface(muro)
    muro_rect = muro.get_rect()
    muro_rect= (1,1)
    
    
    fondo = pygame.image.load("fondo.png")                                               #FONDO
    fondo = pygame.transform.scale(fondo,(1100,600))
    fondo_rect = fondo.get_rect()
    fondo_rect= (1,1)
    
    message = ""
        
    while True:
        pygame.time.Clock().tick(120)
        
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()
        
        
        fuente = pygame.font.Font(None,70)                                              #TEXTO        
        text = fuente.render(message, True ,azul)
        rect_text = text.get_rect()
        rect_text = (1,1)
        
        
        
        tecla_precionada = pygame.key.get_pressed()                                     #MOVIMIENTO
        if tecla_precionada[pygame.K_s]:
            personaje_rect.y +=10
            
        if tecla_precionada[pygame.K_d]:
            personaje_rect.x +=10
            
        if tecla_precionada[pygame.K_a]:
            personaje_rect.x -=10
            
        if tecla_precionada[pygame.K_w]:
            personaje_rect.y -=10
        
        if  personaje_rect.bottom >alto:
            personaje_rect.bottom =alto
            
        if  personaje_rect.top <0:
            personaje_rect.top =0
            
        if  personaje_rect.left <0:
            personaje_rect.left =0
            
        if  personaje_rect.right > ancho:
            personaje_rect.right =ancho
            
            
            
        offset = ((personaje_rect.x - muro_rect.x , personaje_rect.y - muro_rect.y))        #COLISION
        if mask_pj.overlap(mask_muro,offset):
            message='Existe una colisioń'
        
        
        
        ventanita.blit(fondo,fondo_rect)                                                  #MOSTRAR COSAS
        ventanita.blit(muro,muro_rect)
        ventanita.blit(personaje,personaje_rect)
        
        
        
        
        
        
        pygame.display.update()                                                          #RECARGAR VENTANA
if __name__=="__main__":
    main()
