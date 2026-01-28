# Godot resumo

```
git remote add origin https://github.com/ProfAndersonAndrade/plataforma_2d.git
git branch -M main
git push -u origin main
```

## Aula 1 e 2 

- Criando nó raiz, renomeando pra Game
- Crio uma pasta de scene e salvo (ctrl + s) dentro dela
- Crio nó filho em Game (ctrl + a) e procuro o nó CharacterBody2D 
- Ele vai reclamar pois não tem colisor, ctrl+a e adicionamos o CollisionShape2D
- Ele vai reclamar o tipo de shape, selecinando e na direita escolhemos a forma,
 no caso CapsuleShape2D
- Em Depuração -> forma de colisão visível.
- Marcamos isso para deixar o colisor visivel no jogo
- Clicando com o direito no char adionaremos um script, mudamos a pasta 
para scripts/player.gd
- Em Game damos ctrl+a e adicionamos um staticBody2D para criar o chão
- Ele vai necessitar do CollisionShape2D
- O shape retangular, posicionamos abaixo, testamos com F5

## Aula 3

- Não faz sentido o player estar na cena Game só, pois o player jogará várias
cenas, por isso deletamos o player e o faremos em outra cena própria
- Depois de deletar o player, clicamos no + na janela central para nova cena
- Em vez de Node2D, escolhemos outro nó
- Mesmo processo, adiciona o characterdesign2D e o collision
- Ctrl+s para salvar e vamos guardar ele em entities/player.tscn, pasta onde
ficará todos os chars, sejam players, enemies e items.
