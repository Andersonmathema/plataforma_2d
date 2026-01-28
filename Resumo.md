# Godot resumo

## Aula 1 e 2 

- Criando nó raiz, renomeando pra Game.
- Crio uma pasta de scene e salvo (ctrl + s) dentro dela.
- Crio nó filho em Game (ctrl + a) e procuro o nó CharacterBody2D .
- Ele vai reclamar pois não tem colisor, ctrl+a e adicionamos o CollisionShape2D
- Ele vai reclamar o tipo de shape, selecinando e na direita escolhemos a forma,
 no caso CapsuleShape2D.
- Em Depuração -> forma de colisão visível.
- Marcamos isso para deixar o colisor visivel no jogo.
- Clicando com o direito no char adionaremos um script, mudamos a pasta 
para scripts/player.gd.
- Em Game damos ctrl+a e adicionamos um staticBody2D para criar o chão.
- Ele vai necessitar do CollisionShape2D.
- O shape retangular, posicionamos abaixo, testamos com F5.

## Aula 3

- Não faz sentido o player estar na cena Game só, pois o player jogará várias
cenas, por isso deletamos o player e o faremos em outra cena própria.
- Depois de deletar o player, clicamos no + na janela central para nova cena
- Em vez de Node2D, escolhemos outro nó.
- Mesmo processo, adiciona o characterdesign2D e o collision.
- Ctrl+s para salvar e vamos guardar ele em entities/player.tscn, pasta onde
ficará todos os chars, sejam players, enemies e items.
- Para vincular o player na cena do Game, em Game clicamos na corrente acima
do nome da cena (Game) e selecionamos o player.
- Em scripts/player.gd não excluímos o código, arrastamos o player.gd para cima 
da cena do Player e ele vinculará o código.
- Baixamos sprites do site https://grafxkid.itch.io/sprite-pack-6 e criamos a 
pasta sprites/1 - Penguin para acessar as sprites
- No Player adcionamos novo nó chamado AnimatedSprite2D.
- Na direita em Sprite frames escolhemos SpriteFrame, clicamos nele e escolhemos
o resource. Abaixo abrirá uma janela que renomeamos nas animações para 
idle(parado). Clicamos no icone de grade ou ctrl+shift+o, escolhemos o idle16x16
e fatiamos corretamente Horizontal 5 e Vertical 1. Selecionamos tudo e 
adicionamos os 5 quadros.
- A imagem aparecerá borrada, vá para Projeto -> Configurações do Projeto.
- Na aba Renderização -> Texturas -> Filtro de textura padrão -> Nearest
- Clique no play da janela central abaixo (ou a tecla D) para ver a animação.
- Para rodar a animação no jogo (F5) deixamos marcado o auto-reproduzir ao 
carregar (depois da lixeira na janela de Animações abaixo).
- O Colisor ajustamos ao tamanho do player.
- Para ajustar os tamanhos vamos em Configurações do Projeto -> Mostrar-> Janela
e escolhemos em Tamanho 150x100, maximized e em Esticar o modo para canvas_items
- Colocamos o chão e o player dentro da camera e damos F5
- Personagem muito rápido, ajustamos o script:
	
```python
const SPEED = 30.0
const JUMP_VELOCITY = -300.0
```

## Aula 4
