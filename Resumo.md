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

## Aula 4 - flip player

- Se clicarmos em AnimatedSprite2D na direita vemos em offset Flip H que é o 
efeito que queremos aplicar ao player.
- Abrimos o script e arrastamos o animated segurando ctrl e adicionamos ao 
código:

```python
extends CharacterBody2D

# Adicionado 
@onready var anim: AnimatedSprite2D = $AnimatedSprite2D 

const SPEED = 30.0
const JUMP_VELOCITY = -300.0
``` 
- Mudei o nome da variável para anim, é do tipo AnimatedSprite2D e o sifrão
indica uma busca na árvode de nós à esquerda com este elemento
- No final do código antes de move_and_slie() vamos fazer um if:

```python
if direction > 0:
		anim.flip_h = false
	elif direction < 0:
		anim.flip_h = true
		
	move_and_slide()
```

- Na janela de animações adicionamos duas novas (ctrl+N): jump(jump16x16) e 
walk(waddling16x16), no código ficará assim:
	
```python
if is_on_floor():
		if direction > 0:
			anim.flip_h = false
			anim.play("walk")
		elif direction < 0:
			anim.flip_h = true
			anim.play("walk")
		else:
			anim.play("idle")
	else:
		anim.play("jump")
```

## Aula 5 - Camera no player

- Primeiro vamos ocultar o colisor do player clicando no "olho" do 
CollisionShape2D do player.
- Nas configurações projeto em Janela podemos dobrar o tamanho da altura e
largura em 300x200
- Para criar as plataformas, seleciono o bloco e ajusto seu tamanho, clico em 
ctrl+D para duplicar. Se ajustar o tamanho novamente verá que os dois blocos
estão vinculados, pois o godot o trata como o mesmo arquivo. Se quiser 
desvincular basta clicar no bloco e na direita onde escolhemos o tipo de shape
clicar no dropdown e escolher "Tornar único".
- Feito as plataformas e rodando percebemos que o player está lento, deixe a 
velocidade no código em 80.
- Para a camera no player criaremos um nó novo no player, chamado de Camera2D
como filha de player. Ao testar em F5 percebemos que a camera não tem limites,
se o personagem pula ou vai pra esquerda ele mostra muitas partes que talvez 
a gente não queira que seja mostrado. O ideal é dar limites.
- Com a Camera2D selecionada na janela direita clicamos em limit, deixaremos
left e top zerados, bottom 200(o tamanho da altura da janela feita no início
dessa aula). O right depende do tamanho da fase, afinal de acordo com que 
andamos pra direita o personagem vai progredindo. Sabendo onde será o fim da 
fase basta posicionar o player nele e na janela direita em transform vemos a 
coordenada x (entre 430 e 470 mais ou menos) e podemos limitar a camera até essa
posição.
- Por fim para suavizar a camera podemos marca o Position smoothing, dará uma 
sensação de movimento de camera ao para o personagem.

## Aula 6 - Configurando teclas

- Clicamos em Projeto -> Configurações do projeto -> Mapa de Entrada
- Em Adicionar nova ação damos um nome ao comando, este nome será chamado no
código, escreva "left" e dê enter e ele mostra o nome seguido do símbolo de +.
- Ao clicar no + ele pede para clicar na tecla correspondente ao comando,
no caso escolho o "A" e a seta esquerda do teclado, no comando "right" escolho 
"D" e seta para direita e por fim "jump" com as teclas backspace, "W" e seta 
para cima. 
- No código mudamos os comandos com ui para os nomes dos comando que demos:
```python
# Handle jump.
if Input.is_action_just_pressed("jump") and is_on_floor():
	velocity.y = JUMP_VELOCITY

# Get the input direction and handle the movement/deceleration.
# As good practice, you should replace UI actions with custom gameplay actions.
var direction := Input.get_axis("left", "right")
```

## Aula 7 - Tile Map

- Vamos alterar a paisagem, no site https://grafxkid.itch.io/seasonal-tilesets
baixamos os tilesets, extraimos e colocamos na pasta sprites.
- Vamos apagar as plataformas, clica com o direito em StaticBody2D e excluir.
- O novo nó em Game será o TileMapLayer.
- Clicando em Tile Set na janela direita e clicando em TileSet no dropdown
abrirá uma janela de configuração abaixo.
- Napasta Seasonal Tilesets escolhemos a pasta Grassland e a imagem Terrain 
16x16 arrastando na aba TileSet, ele pergunta se quer que ele crie 
automaticamente os tiles, responda que sim.
- Na aba TileMap selecionamos a ferramenta de pintura(D) e com o seletor no Game
selecionado clicamos no desenho e ao clicar no game ele carimba a imagem 
selecionada abaixo. Arrastando ele cria vários, com o direito ele apaga.
- Podemos circular uma área e com a ferramenta balde(B) ele preenche a área.
- Preste atenção no acabamento, perceba que as extremidades dos tiles da imagem
são diferentes para dar um efeito mais bonito.
- Se rodar o jogo o personagem vai cair, pois não há collision.
- Para isso clicamos ena janela direita em Tile Set -> Phisics Layers -> 
Adicionar elemento.
- Na aba TileSet na janela de baixo clicamos na aba superios desta janela em
Selecionar, segurando o shift selecionamos a grama dos tiles superiores, pois
é o local que queremos que tenha colisão.
- Ele abre um menu Tiles, em Física e depois Phisics layer, lá no final dele
haverá um tile para marcar os pontos do poligono de colisão. Clicamos em F
e ele seleciona o tile "full", ao dar F5 já vemos o resultado da seleção.

## Aula 8

- Criamos uma área que queremos que o personagem passe na frente de blocos
e ao pular suba na plataforma.
- Apagamos todos os tiles no jogo.
- No player em AnimatedSpite2D em Ordering na direita o Zindex indica qual a 
ordem das camadas de layers. Todos começão no 0, deixaremos o player no 1 e 
background posteriormente em -1, -2, -10 e assim por diante.
- Observamos que o tileset está na forma de cruz, selecionamos todos os blocos 
menos os 6 superiores, os 6 serão a base das plataformas tranpassáveis.
- Os de baixo slecionamos em tileset todos e clicamos em F, colocando colisor
em todos.
- Os 6 de cima uso colando em cima do chão cheio de colisor, escolho só a grama
para colidir e em poligon 0 abaixo do physics layer deixamos o direção única
marcado para o personagem passar por baixo ao pular e ficar em cima.
