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
O _renedr_ é feito de forma variável, ou seja, a cada quadro (_frame_) que o _hardware_ do jogador consegue processar, garantindo uma experiência visual mais fluida e responsiva.
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

## 2.3 Comunicação e _dispatch_ de Eventos

A comunicação entre os diferentes subsistemas de uma _game engine_ é fundamental para o funcionamento de um jogo. Na **Cinnamon**, a comunicação com os eventos globais da _engine_
são feitas através de um registro de eventos, onde cada subsistema pode se inscrever, utilizando interfaces funcionais, para receber chamadas em determinados pontos do ciclo de vida da _engine_.

Eventos dentro do mundo do jogo, como colisões, interações com o jogador ou mudanças de estado, são tratados através do polimorfismo de funções e depende de cada objeto, que pode implementar métodos específicos para lidar com esses eventos.