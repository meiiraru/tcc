# Capítulo 1: O Conceito de Motores de Jogos (_Game Engines_)

## 1.1 Propósito, Definição e Função

Um motor de jogo, ou _Game Engine_, é uma plataforma de software projetada especificamente para a criação e o desenvolvimento de jogos digitais.
O principal propósito de uma _engine_ é fornecer aos desenvolvedores um conjunto de ferramentas e funcionalidades que facilitam a criação de jogos,
permitindo que o foco seja voltado para a parte mais criativa do desenvolvimento, ao invés de se preocuparem com os aspectos técnicos complexos.

No primórdio dos jogos, na era do Atari e dos primeiros consoles, não se existia um conceito de _game engine_, pois os jogos eram desenvolvidos de forma muito mais direta,
com cada jogo sendo uma aplicação independente, escrita do zero para cada plataforma específica.

A mudança desse paradigma começou a ocorrer quando os desenvolvedores perceberam que muitos jogos compartilhavam elementos em comum, como renderização gráfica, física e processamento sonoro,
separado dos dados dos jogos, como texturas, modelos 3D, sons e lógica de _gameplay_. _Engines_ pioneiras, como a **id Tech**, desenvolvida pela **id Software** para jogos como **Doom** e **Quake**,
consolidaram a ideia de que uma _engine_ poderia ser licenciada e reutilizada em múltiplos projetos, permitindo criar experiências completamente diferentes com base na mesma tecnologia _core_.

## 1.2 Arquitetura Modular e Funcionalidades

Uma arquitetura de _Game Engine_ moderna é construída de forma modular, composta por diversos subsistemas que trabalham em conjunto para fornecer uma experiência de desenvolvimento eficiente e robusta.
Cada módulo é responsável por uma área específica do desenvolvimento de jogos, e a integração entre eles é crucial para o funcionamento harmonioso da _engine_.

Hoje em dia, os motores de jogos modernos, como **Cinnamon**, **Godot**, **Unity** e **Unreal Engine**, oferecem uma ampla gama de funcionalidades,
incluindo renderização avançada, sistema de física, gerenciamento de recursos e suporte a múltiplas plataformas.

Essa modularização permite que desenvolvedores escolham apenas os subsistemas necessários para o seu projeto, facilitando também a manutenção e a escalabilidade da _engine_ em aplicações mais complexas.

# Capítulo 2: Padrões de Design e Arquitetura de Motores de Jogos

## 2.1 O Game Loop e o Ciclo de Vida do Jogo

O _Game Loop_ é o núcleo de qualquer _game engine_, sendo responsável por gerenciar o fluxo contínuo de execução do jogo. Ele é literalmente, assim como é chamado na programação, um _loop_,
que se repete continuamente enquanto o jogo está em execução, garantindo que todas as partes do jogo sejam atualizadas e renderizadas, além de permitir também o processamento de entradas (_inputs_) do usuário.

Segundo a arquitetura de um _game engine_, existem diferentes abordagens para a implementação do _Game Loop_. A **Cinnamon Engine** adota um modelo de _Game Loop_ robusto conhecido como _Fixed Update Time Step_,
que garante que a lógica do jogo seja atualizada em intervalos fixos, independentemente da taxa de quadros (_frame rate_) do jogo, misturado com _Variable Rendering_,
que permite que a renderização seja feita de forma mais fluida, adaptando-se à capacidade do hardware do jogador.

A fase de lógica, chamada de _Tick_ ou também de _Update_, é responsável por atualizar o estado do jogo, processando a física e a lógica de _gameplay_.
Essas atualizações são feitas em intervalos fixos, que no caso da **Cinnamon**, são de 20 vezes por segundo. Isso garante um determinismo, ou seja, deixa de ser relativo à performance do _hardware_ do usuário,
a lógica da engine é executada de forma consistente e previsível.

A fase de renderização, chamada de _Render_, é responsável por desenhar os elementos do jogo na tela, utilizando os dados atualizados na fase de lógica.
O _render_ é feito de forma variável, ou seja, a cada quadro (_frame_) que o _hardware_ do jogador consegue processar, garantindo uma experiência visual mais fluida e responsiva.
Para evitar que o _render_ fique em par com a velocidade dos _Ticks_, a **Cinnamon** utiliza algoritmos de interpolação linear (conhecidos como _lerp_) para prever e suavizar o movimento dos objetos entre os _Ticks_ de lógica,
permitindo com que a experiência visual seja mais agradável e fluida.

## 2.2 Gerenciamento de Objetos

O gerenciamento de objetos é uma parte essencial da arquitetura de um _game engine_, pois envolve a criação, atualização e destruição de objetos que compõem o mundo do jogo.
Esses objetos podem ser entidades do jogo, como personagens, inimigos, itens, ou elementos do ambiente, como árvores, prédios e obstáculos.

Atualmente, a maioria das _game engines_ modernas utiliza um sistema de gerenciamento baseado em componentes, onde cada objeto é apenas uma representação numérica,
com uma lista de componentes que definem seu comportamento e aparência. Essa abordagem permite uma maior flexibilidade e reutilização de código, pois os desenvolvedores podem criar novos tipos de objetos combinando diferentes componentes.

A **Cinnamon Engine** adota um sistema de gerenciamento de objetos baseado em classes, fortemente utilizando o paradigma de programação orientada a objetos (_OOP_).
Nesse sistema clássico, utiliza-se bastante o conceito de herança e polimorfismo de classes, permitindo que os desenvolvedores criem hierarquias de objetos e definam comportamentos específicos para cada tipo de objeto.
Esse padrão é mais tradicional e pode ser mais intuitivo para desenvolvedores que já estão familiarizados com a programação orientada a objetos, permitindo uma prototipagem mais rápida,
porém é menos flexível do que o sistema baseado em componentes.

## 2.3 Comunicação e _Dispatch_ de Eventos

A comunicação entre os diferentes subsistemas de uma _game engine_ é fundamental para o funcionamento de um jogo. Na **Cinnamon**, a comunicação com os eventos globais da _engine_
são feitas através de um registro de eventos, onde cada subsistema pode se inscrever, utilizando interfaces funcionais, para receber chamadas em determinados pontos do ciclo de vida da _engine_.

Eventos dentro do mundo do jogo, como colisões, interações com o jogador ou mudanças de estado, são tratados através do polimorfismo de funções e depende de cada objeto, que pode implementar métodos específicos para lidar com esses eventos.

# Capítulo 3: Renderização Gráfica e Pipeline Visual

A renderização gráfica é um dos aspectos mais visíveis e impactantes de um jogo, é o subsistema responsável por transformar modelos 3D, texturas, luzes e outros efeitos em uma imagem final que é exibida na tela do jogador.
Esse processo ocorre dezenas ou centenas de vezes por segundo, dependendo da taxa de quadros (_frame rate_) do jogo, e envolve uma série de etapas complexas que compõem a _pipeline_ de renderização.
A **Cinnamon Engine** foi projetada sobre a API gráfica **OpenGL**, comunicando-se diretamente com o _hardware_ através de chamadas de baixo nível fornecidas pela API **LWJGL (Lightweight Java Game Library)**, que é uma biblioteca de código aberto que fornece acesso a recursos de baixo nível do _hardware_, como gráficos, áudio e entrada de dispositivos.

## 3.1 _Pipeline_ Gráfico Programável e _Shaders_

O _pipeline_ gráfico programável é uma evolução do _pipeline_ fixo, permitindo que os desenvolvedores tenham controle total sobre como os gráficos são processados e renderizados.
Essa _pipeline_ programável permite que a _engine_ utilize pequenos programas chamados _Shaders_, que são executados paralelamente na GPU (Placa de Vídeo) para realizar operações de renderização,
como transformação de vértices, iluminação, texturização e efeitos visuais avançados.

O fluxo básico da **Cinnamon Engine** envolve a passagem de dados da CPU (memória RAM) para a GPU (VRAM) através de _buffers_, onde os _Shaders_ processam esses dados e produzem a imagem final que é exibida na tela do jogador.
Os vértices são processados em um _Vertex Shader_, que aplica transformações geométricas de matrices e calcula a posição final dos vértices na tela,
formando as primitivas geométricas, como triângulos, que são então rasterizados e preenchidos com cores e texturas no _Fragment Shader_, que calcula a cor final de cada pixel na tela.

Toda a _pipeline_ de renderização é altamente personalizável, permitindo que os desenvolvedores desabilitem ou criem efeitos visuais novos e únicos, permitindo uma alta estilização visual e identidade artística para cada jogo desenvolvido com a **Cinnamon Engine**.

## 3.2 _Draw Calls_ e _Batching_

Um dos maiores gargalos de desempenho em jogos é o excesso de comunicação entre a CPU e a GPU, que compõem o número de chamadas de desenho feitos à GPU, ou _draw calls_.
Para mitigar este problema, a **Cinnamon Engine** implementa um modo misto entre _Immediate Mode_ e _Batching_, onde dependendo do tipo de objeto,
ele pode ser desenhado imediatamente ou agrupado em lotes (_batches_) para reduzir o número de chamadas à GPU.

**Cinnamon** permite que vértices brutos sejam enviados diretamente para a GPU, sem a necessidade de criar objetos intermediários, o que é útil para objetos simples, interfaces gráficas e _debugging_.
Esses vértices são capturados por um sistema de *Vertex Consumer*, que organiza os dados em _buffers_ e envia para a GPU em um único _draw call_, reduzindo significativamente a sobrecarga do processador.

## 3.3 Materiais, Iluminação Baseada em Física (_PBR_) e _Deferred Rendering_

Para alcançar um nível de realismo visual mais elevado e customização, a **Cinnamon Engine** implementa um sistema de materiais compatível com o formato **MTL-PBR** (_Physically Based Rendering_).
A teoria do PBR se baseia na microgeometria, na conservação da energia da luz e a simulação de como a luz interage com diferentes superfícies.
Ao invés de estimar o brilho e a cor de uma superfície de forma arbitrária, o PBR utiliza propriedades físicas reais, como rugosidade e metalicidade para determinar como a luz é refletida e absorvida,
resultando em uma aparência mais realista e consistente sob diferentes condições de iluminação.

Esses materiais reagem de maneira fisicamente precisa ao sistema de iluminação da _engine_, que calculam diferentes tipos de luzes, como luzes pontuais, direcionais e _spotlights_, além de projetar sombras dinâmicas.
Além disso, para a renderização das cenas no mundo, a **Cinnamon** utiliza um sistema de _Deferred Rendering_, que permite que a iluminação e os efeitos visuais sejam aplicados de forma mais eficiente,
separando a geometria da cena da iluminação, permitindo que múltiplas luzes sejam processadas sem a necessidade de recalcular a geometria para cada luz, aumentando o desempenho e a qualidade visual do jogo.

## 3.4 Pós-processamento e Efeitos Visuais

O pós-processamento é uma etapa final na _pipeline_ de renderização, onde efeitos visuais adicionais são aplicados à imagem final antes de ser exibida na tela do jogador.

Nessa etapa a **Cinnamon Engine** aplica efeitos como **SSAO** (_Screen Space Ambient Occlusion_), que simula a colusão da luz em cantos e superfícies próximas, aumentando a percepção de profundidade e realismo da cena, _Bloom_, que simula o efeito de luz intensa e difusa, **SSR** (_Screen Space Reflections_) que simula reflexos em superfícies refletivas, **FXAA** (_Fast Approximate Anti-Aliasing_) que suaviza as bordas dos objetos para evitar o efeito de serrilhado.

**Cinnamon** também permite aplicar efeitos de pós-processamento personalizados após a renderização da cena, permitindo que os desenvolvedores criem efeitos visuais únicos e estilizados para seus jogos, como filtros de cor, distorções, desfoques e outros efeitos artísticos.

# Capítulo 4: Matemática, Física e Detecção de Colisões

## 4.1 Fundamentos Matemáticos e Álgebra Linear

A **Cinnamon Engine** estende a biblioteca **JOML** (_Java OpenGL Math Library_) para manipular eficientemente as estruturas de dados fundamentais da computação gráfica, como vetores, matrizes e quaternions.

Além da álgebra básica, a _engine_ também implementa em seu módulo matemático funções de suporte para a criação de ruídos procedurais (_Noise Functions_),
onde podem ser utilizados para gerar terrenos, texturas e efeitos visuais de forma procedural, aumentando a diversidade e a complexidade dos jogos sem a necessidade de criar manualmente cada elemento.

Também tem suporte para funções de criação de curvas paramétricas e funções de interpolação (_Easing Functions_), que são amplamente utilizadas para criar animações suaves e transições entre estados de objetos no jogo.

## 4.2 Detecção de Colisões por **SAT** e Resolução

A interação física entre os objetos no mundo requer um sistema de detecção e resolução de colisões. Na **Cinnamon Engine**, a detecção de colisões é dividida em duas fases, a fase ampla, chamada de _Broad Phase_ e a fase estreita, _Narrow Phase_.

Na _Broad Phase_, a _engine_ utiliza muito o conceito de **AABB** (_Axis-Aligned Bounding Box_), que são caixas delimitadoras alinhadas aos eixos, para rapidamente descartar pares de objetos que não estão próximos o suficiente para colidir.

Na _Narrow Phase_, quase se verifica se duas formas estão se sobrepondo, a **Cinnamon** utiliza o algoritmo **SAT** (_Separating Axis Theorem_).
A teoria do **SAT** afirma que, se dois polígonos convexos não estão colidindo, então existe pelo menos um eixo de projeção no qual as projeções dos dois polígonos não se sobrepõem.
A _engine_ aplica este teorema para testar intersecções entre diferentes formas de colisores, como **AABB**, **OBB** (_Oriented Bounding Box_), Esferas e Triângulos, permitindo uma detecção de colisões precisa e eficiente.

Detectar a colisão é apenas metade do problema, a _engine_ precisa dizer como os objetos devem reagir físicamente.
A **Cinnamon** implementa um sistema de resolução de colisões simples, dependendo do tipo de resolução desejada, permitindo respostas como _Slide_ (Deslizamento), _Bounce_ (Rebote) ou _Stop_ (Parada), dependendo do comportamento desejado para cada objeto.

# Capítulo 5: Estruturas de Dados Espaciais, Interface e Imersão

## 5.1 Particionamento Espacial e Terrenos

Renderizar e verificar colisões de um mundo inteiro a cada _frame_ seria computacionalmente inviável. Para resolver isso, a **Cinnamon Engine** estrutura o mundo do jogador utilizando o particionamento espacial baseado em **Octrees**.

A **Octree** é uma estrutura de dados hierárquica que subdivide o espaço tridimensional em oito regiões menores (nós). Essa abordagem permite que a _engine_ aplique técnicas como _Frustum Culling_,
descartando nós que estão fora do campo de visão da câmera, permitindo que apenas os objetos visíveis sejam processados e renderizados, aumentando significativamente o desempenho do jogo,
além também de otimizar a detecção de colisões, verificando apenas os objetos que estão dentro do mesmo nó ou em nós adjacentes.

## 5.2 Interface de Usuário

O Sistema de interface de usuário, **GUI** (_Graphical User Interface_) da _engine_ é projetado para ser flexível e eficiente, permitindo que os desenvolvedores criem interfaces intuitivas e responsivas para seus jogos.

A **Cinnamon Engine** implementa um sistema de **GUI** baseado em _Widgets_ e _Containers_, onde cada elemento da interface é um _Widget_ que pode ser posicionado, redimensionado e estilizado de acordo com as necessidades da janela atual.

Toda janela contém um _Container_ base, que então pode conter outros _Containers_ e _Widgets_, estruturados como uma árvore, permitindo a criação de hierarquias complexas de elementos de interface, como menus, botões, barras de progresso, caixas de diálogo e mais.

## 5.3 Texto

A **Cinnamon** implementa um sistema de objetos de texto, permitindo que textos possam ser adicionados dentro de outros textos, criando uma hierarquia similar a de uma árvore.
Os textos possuem uma propriedade de estilização, _Style_, que permite definir a fonte, cor e outros efeitos visuais, permitindo que os desenvolvedores criem interfaces de usuário mais ricas e personalizadas.

Por cada texto ser seu próprio nó, a _engine_ permite que textos filhos herdem propriedades de estilização do texto pai, permitindo uma maior consistência visual e facilidade de manutenção da interface.

## 5.4 Imersão e Integração com Realidade Virtual (VR)

A imersão é um aspecto crucial para a experiência do jogador, e a **Cinnamon Engine** oferece suporte a tecnologias de realidade virtual (_VR_).
A _engine_ integra-se com dispositivos de VR através da API **OpenXR**, fornecendo informações como posição e orientação da cabeça do jogador e dos controladores para o desenvolvedor final.