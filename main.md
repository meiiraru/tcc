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

Hoje em dia, os motores de jogos modernos, como **Unity** e **Unreal Engine**, oferecem uma ampla gama de funcionalidades,
incluindo renderização avançada, física realista, inteligência artificial, gerenciamento de recursos e suporte a múltiplas plataformas.

Essa modularização permite que desenvolvedores escolham apenas os subsistemas necessários para o seu projeto, facilitando também a manutenção e a escalabilidade da _engine_ em aplicações mais complexas.

# Capítulo 2: Padrões de Design e Arquitetura de Motores de Jogos

## 2.1 O Game Loop e o Ciclo de Vida do Jogo