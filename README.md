# Jogo da velha

Mini-projeto realizado com a intenção de praticar conhecimentos sobre Vue 3 (conceitos básicos de componentização e Composition API) e Typescript.
O jogo da velha é uma ideia já *clássica* de tutoriais de frameworks frontend que aplicam componentização. No entanto, me pareceu mais interessante que outras ideias.
Hospedado (em 16/11/2022) em https://jogo-da-velha-gilt.vercel.app/.

Coisas que pensei durante o desenvolvimento:

- No começo, o jogo e os quadradinhos eram componentes diferentes. Essa configuração permitiu que eu exercitasse mais a trocar de informação entre componentes, aplicando props e emits. Mas a comunicação entre os componentes se tornou meio confusa pra mim, e a solução parecia ser um store. Pra manter a simplicidade de um primeiro projeto, decidir unificar o componente.
- A Composition API parece mais simples, mas, naturalmente, ainda há pouca coisa escrita nela. Como os primeiros tutoriais que tive contato era na Options, estranhei um pouco.
- Typescript não fez muita diferença em relação a complexidade, mas já mostrou que deixa o processo bem menos confuso.

Possibilidades de melhorias e/ou expansões:

- Aplicação mais contundente de estilos.
- Oferecer opções de símbolos para os jogadores.
- Mudar o placar para "Jogador 1 | Jogador 2" e alternar quem começa cada rodada.
- Tornar mais visual a conclusão de cada rodada.


