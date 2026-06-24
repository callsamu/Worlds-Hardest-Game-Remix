Cada objeto conterá um conjunto de arquivos .gml, formato que pode ser aberto com o bloco de notas ou com o VSCode.

GML é a linguagem própria do GameMaker, software de criação de jogos utilizado neste projeto.

Create:
se trata das variáveis criadas imediatamente após a criação do objeto no jogo.

Step: 
se trata de um código que é executado a cada frame, que manipula tanto as variáveis declaradas no Create quanto as que são declaradas a cada frame.
Apresenta funções que lidam com o que ocorre em tempo real durante a jogatina, como colisões.

Draw:
lida com o que será desenhado durante a jogatina. Apresenta funções que criam ou manipulam sprites ou desenha formas simples sem necessariamente ter interação real no jogo.

Other:
lida com o que ocorre imediatamente após uma sala ser mostrada.

## Design Pattern Adotados

### State

Usado no gerenciamento de estado do objeto **ObjSquare** que representa o jogador. A cada frame o objeto pode transicionar
para um estado diferente e assumir um comportamento atrelado a ele. No caso, foram definidos os estados `normal, dying, reviving`
trabalhando em conjunto para implementar a morte e respawn do jogador.

<img width="513" height="120" alt="image" src="https://github.com/user-attachments/assets/c0972a6f-73e1-47ae-b57a-cd53a501dd2f" />

<img width="405" height="312" alt="image" src="https://github.com/user-attachments/assets/ac2299f4-86e9-4f07-b8fd-9051a850d25e" />

### Flyweight

Ao posicionar um inimigo no editor de níveis, é possível determinar um caminho que será percorrido por ele ao longo do tempo,
por meio de um objeto do Gamemaker chamado **path**. Nesse contexto, o path consiste nos segmentos de reta
formados por diferentes pontos que são colocados pelo usuário. 

Uma quantidade numerosa de inimigos podem ter paths idênticos, o que seria um desperdício de memória. É aplicado então o
conceito do **flyweight**, onde objetos de path são armazenados em uma array global, e são referenciados em um atributo dos
inimigos chamado inventório. Dessa forma, um pode-se atrelar um ou mais paths ao inventório dos inimigos, os quais vão
referenciar o mesmo objeto sem duplicação necessária.

<img width="858" height="204" alt="image" src="https://github.com/user-attachments/assets/1306ef0b-0232-4ce9-8575-325371c7eee5" />

### Prototype

Entretanto, o compartilhamento de referências a um path gera um grande incoveniente: se o usuário realiza uma
alteração mínima no path de um único inimigo, essa mesma modificação afeta **todos** os inimigos que o compartilham.
Isso torna desejável uma duplicação intencional do path, o que é feito com uma implementação do **prototype** no 
objeto respectivo, onde foi adicionado um método `clone()` que copia atributos do path para uma nova
instância, abstraindo assim a manipulação de detalhes internos do objeto ao código que adiciona a opção de cópia
na UI e realiza a duplicação.

<img width="519" height="478" alt="image" src="https://github.com/user-attachments/assets/4db5b8d3-316a-4d80-ae8a-afc16f6ed848" />

dez usuários de teste: https://docs.google.com/document/d/1DpLuFfR8ylnAlixrB8dD2iN_36zlv8jkx2sjv-9xV70/edit?usp=sharing
