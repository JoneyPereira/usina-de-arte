# RELATÓRIO TÉCNICO — PROJETO VR NO METAVERSO

Web 3.0 | Residência em TIC 29 — Atividade Avaliativa

---

## SEÇÃO 1 — IDENTIFICAÇÃO

Nome Completo: Joney Sousa Pereira

Turma / Residência: [Insira sua turma]

Limitação de Hardware Relatada:

---

## SEÇÃO 2 — CONCEITO DO PROJETO

2.1 Nome do Projeto: [Ex: EcoMeta: Galeria Sustentável]
2.2 Contexto e Objetivo no Metaverso:

[Explique o propósito. Ex: Criar um ambiente educacional imersivo para ensinar reciclagem para crianças, resolvendo a falta de engajamento em aulas teóricas.]

2.3 Descrição Geral do Ambiente Virtual:

[Descreva o espaço. Ex: Uma praça circular de 50m de diâmetro, cercada por árvores estilizadas, contendo 4 estações de coleta seletiva e um painel central de pontuação. A iluminação seria de fim de tarde (Golden Hour) para uma sensação acolhedora.]

---

## SEÇÃO 3 — CONFIGURAÇÃO TÉCNICA DO PROJETO

3.1 Versão do Unity e Porquê: [Ex: Unity 6000.3.9f1 LTS, por ser a versão estável com suporte de longo prazo recomendada para o Meta XR SDK.]

3.2 Instalação do Meta XR SDK (Passo a Passo): [Ex: 1. Acesso ao Project Settings; 2. Adição do escopo "Oculus"; 3. Download e Importação do 'Meta XR All-in-One SDK'.]

3.3 Configurações de Build para Android/Meta Quest: [Ex: Switch Platform para Android; Texture Compression: ASTC; Minimum API Level: Android 10 (Level 29) para compatibilidade com Quest 2/3.]

3.4 Configuração do XR Plugin Management: [Ex: Marcaria a opção 'Oculus' na aba Android para habilitar o suporte ao hardware.]

3.5 Movimentação no PC (Editor): [Ex: Utilizaria o 'XR Meta Simulator' do Meta SDK para emular os controles e headset usando mouse e teclado.]

---

## SEÇÃO 4 — ASSETS E ELEMENTOS DA CENA

### ASSET 1

* Nome: [Ex: Palmeira]
* Tipo: Material / Textura
* Origem: Asset Store (Gratuito)
* Função: Criar o fundo imersivo do ambiente.

### ASSET 2

* Nome: [Ex: Mesa de Madeira]
* Tipo: Objeto 3D
* Origem: Primitivo Unity (com modificações)
* Função: Suporte para os itens interativos.

### ASSET 3

* Nome: [Ex: Som de Clique]
* Tipo: Som
* Origem: Asset Store (Gratuito)
* Função: Feedback sonoro ao tocar em botões.

---

## SEÇÃO 5 — HIERARQUIA DE GAME OBJECTS

Scene: [Nome da Sua Cena]
(Descreva a sua cena e a hierarquia destrinchando como você faria a organização de cada game object, como nesse exemplo a seguir:)

* [--- MANAGEMENT --]
* EventSystem
* [--- PLAYER ---]
* [BuildingBlock] Camera Rig
* [--- ENVIRONMENT ---]
* Plane (Chão)
* Directional Light
* Casa
- Paredes
- Porta
- Maçaneta
* [--- INTERACTABLES ---]
* Botão_Principal
* Objeto_Coletável

---

## SEÇÃO 6 — PLANEJAMENTO DO REPOSITÓRIO GITHUB

* 6.1 Nome do Repositório: [Ex: Projeto-Metaverso-TIC29]
* 6.2 Estrutura de Pastas: /Assets: Scripts, Prefabs e Materiais.
* /ProjectSettings: Configurações de Build.
* .gitignore: Para ignorar /Library e /Temp.

---

## SEÇÃO 7 — PLANO DE EXECUÇÃO PASSO A PASSO

(Descreva o plano de execução do projeto seguindo o modelo abaixo:)
1. Etapa 1: Instalação do Unity e criação do projeto 3D (URP).
2. Etapa 2: Importação do Meta XR SDK via Package Manager.
3. Etapa 3: Configuração do XR Origin e mãos do Player.
4. Etapa 4: Modelagem básica do cenário usando ProBuilder ou Primitivos.
5. Etapa 5: Aplicação de materiais, texturas e configuração de iluminação (Baking).
6. Etapa 6: Programação dos Scripts de interação em C#.
7. Etapa 7: Configuração de componentes XR Simple Interactable nos objetos.
8. Etapa 8: Teste final via XR Simulator e Build para APK (.android).

---
## SEÇÃO 8 — REFLEXÃO FINAL

8.1 Aprendizado: [Ex: Entendi a importância da hierarquia e como o XR Interaction Toolkit facilita o mapeamento de controles.]
8.2 Dificuldades Previstas: [Ex: Ajustar o desempenho (Draw Calls) para rodar de forma fluida no hardware mobile do Quest.]
8.3 Melhorias Futuras: [Ex: Implementaria suporte a Multiplayer usando Photon (PUN2) para interação entre usuários.]