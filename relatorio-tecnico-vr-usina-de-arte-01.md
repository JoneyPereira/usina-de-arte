# RELATÓRIO TÉCNICO — PROJETO VR NO METAVERSO

Web 3.0 | Residência em TIC 29 — Atividade Avaliativa

---

## SEÇÃO 1 — IDENTIFICAÇÃO

**Nome Completo:** Joney Sousa Pereira

**Turma / Residência:** Residência em TIC 29

**Limitação de Hardware Relatada:** Desenvolvimento e testes realizados exclusivamente em PC (sem headset físico disponível), utilizando o XR Device Simulator do Meta SDK para emulação do ambiente VR durante a fase de construção.

---

## SEÇÃO 2 — CONCEITO DO PROJETO

**2.1 Nome do Projeto:** UsinaVR — Museu Digital Imersivo

**2.2 Contexto e Objetivo no Metaverso:**

A Usina de Arte é um parque artístico-botânico localizado no município de Água Preta, na Zona da Mata Sul de Pernambuco, a cerca de 150 km de Recife. Instalada nas dependências da antiga Usina Santa Terezinha — fundada em 1929 e que chegou a ser a maior produtora de álcool e açúcar do Brasil nos anos 1950 — o espaço foi reconvertido em 2015 pela família Pessôa de Queiroz em um projeto cultural, educativo e ambiental. Hoje reúne mais de 40 obras de artistas nacionais e internacionais espalhadas por 133 hectares, funcionando como museu a céu aberto de acesso gratuito ao público.

**O problema identificado:** apesar do enorme potencial cultural e artístico da Usina de Arte, sua localização geograficamente isolada — no interior de Pernambuco, sem transporte público direto — representa uma barreira real de acesso para a maior parte da população, especialmente para pessoas com mobilidade reduzida, estudantes de escolas públicas sem recursos para deslocamento, e visitantes internacionais. O acervo de obras de grande porte instaladas ao ar livre também é vulnerável às condições climáticas e ao desgaste do tempo, dificultando a preservação e a documentação digital de longo prazo.

**O objetivo** deste projeto é criar uma experiência em Realidade Virtual que replique, de forma navegável e imersiva, um recorte do acervo e do ambiente da Usina de Arte, permitindo que qualquer pessoa — independentemente de localização geográfica ou condição física — possa visitar, explorar e interagir com as obras do museu. A solução proposta resolve o problema de acesso físico ao museu e contribui para a preservação digital do patrimônio artístico-cultural do Nordeste brasileiro.

**2.3 Descrição Geral do Ambiente Virtual:**

O ambiente virtual recria um percurso central da Usina de Arte com cerca de 200m de extensão linear, partindo da entrada principal (com a locomotiva histórica exposta) em direção ao núcleo do parque artístico-botânico. O cenário inclui:

- Um terreno orgânico com vegetação tropical estilizada (árvores, arbustos e gramado), evocando o parque de reflorestamento com mais de 600 espécies da Usina real;
- Representações simplificadas de 5 obras emblemáticas do acervo, posicionadas ao longo do percurso (ver Seção 4);
- A fachada e estrutura industrial da antiga usina ao fundo, compondo o skybox com silhueta característica das chaminés e do hangar histórico;
- Iluminação de fim de tarde (Golden Hour), recriando a atmosfera acolhedora e quente típica do interior pernambucano;
- Painéis informativos flutuantes próximos a cada obra, com nome do artista, título e breve descrição.

O usuário navega pelo ambiente em primeira pessoa, caminhando pelo percurso central e se aproximando das obras para lê-las e contemplá-las.

---

## SEÇÃO 3 — CONFIGURAÇÃO TÉCNICA DO PROJETO

**3.1 Versão do Unity e Porquê:**

Unity 6000.0.x LTS (Unity 6), por ser a versão com suporte de longo prazo mais recente e totalmente compatível com o Meta XR SDK atual. A versão LTS garante estabilidade durante o desenvolvimento e recebe atualizações de correção sem quebras de API, sendo a escolha recomendada pela própria Meta para projetos direcionados ao Quest.

**3.2 Instalação do Meta XR SDK (Passo a Passo):**

1. Abrir o Unity Hub e criar um novo projeto 3D (URP — Universal Render Pipeline);
2. Acessar `Edit > Project Settings > Package Manager`;
3. Em *Scoped Registries*, adicionar o escopo do NPM do package da Meta: `https://npm.pkg.github.com` (ou via OpenUPM);
4. Acessar `Window > Package Manager`, selecionar *My Registries*;
5. Localizar e instalar o pacote **Meta XR All-in-One SDK**;
6. Após a importação, aceitar as dependências automáticas (XR Core Utilities, XR Interaction Toolkit);
7. Executar o assistente de configuração automática que aparece via `Meta > Tools > Project Setup Tool`, aplicando todas as correções sugeridas (compressão de textura, color space, etc.).

**3.3 Configurações de Build para Android/Meta Quest:**

- `File > Build Settings > Switch Platform`: selecionar **Android**;
- *Texture Compression*: **ASTC** (formato nativo e mais eficiente para o hardware Snapdragon do Quest);
- *Minimum API Level*: **Android 10 (API Level 29)**, garantindo compatibilidade com Meta Quest 2 e Quest 3;
- *Target API Level*: **Android 13 (API Level 33)**;
- Em `Player Settings > Other Settings`: desabilitar *Multithreaded Rendering* (pode causar artefatos em alguns shaders URP no Quest);
- Habilitar *IL2CPP* como Scripting Backend para melhor performance no dispositivo;
- Configurar ícone e nome do aplicativo em `Player Settings > Product Name`: "UsinaVR".

**3.4 Configuração do XR Plugin Management:**

1. Acessar `Edit > Project Settings > XR Plugin Management`;
2. Na aba **Android**, marcar a opção **Oculus** (provedor de XR da Meta);
3. Na aba **PC**, marcar **Oculus** também (permite teste em editor com Link/AirLink);
4. Em `Project Settings > XR Plugin Management > Oculus`: habilitar *Hand Tracking Support* como *Controllers And Hands* e *Symmetric Projection* para melhor desempenho no Quest.

**3.5 Movimentação no PC (Editor):**

Para desenvolvimento e testes sem o headset físico, será utilizado o **XR Device Simulator** nativo do XR Interaction Toolkit, já incluso no Meta XR All-in-One SDK como "Meta XR Simulator". O simulador permite:

- Movimentar a câmera com o mouse (rotação da cabeça) e teclas WASD (locomoção);
- Emular os controles dos dois controladores com o teclado (gatilhos, grip, botões A/B/X/Y);
- Testar interações com objetos XR sem necessitar do headset;
- A cena deve ter o prefab `XR Device Simulator` adicionado à hierarquia, ativado apenas no Editor (desabilitado em build para dispositivo via `#if UNITY_EDITOR`).

---

## SEÇÃO 4 — ASSETS E ELEMENTOS DA CENA

### ASSET 1

- **Nome:** Locomotiva Histórica
- **Tipo:** Objeto 3D (Primitivos Unity combinados: cilindros, cubos e esferas)
- **Origem:** Modelagem com primitivos Unity + ProBuilder
- **Função:** Elemento de entrada e identidade do museu, referência direta à locomotiva real exposta na Usina de Arte; serve como marco visual de chegada ao ambiente.

### ASSET 2

- **Nome:** "Diva" (referência à obra de Juliana Notari)
- **Tipo:** Objeto 3D estilizado
- **Origem:** Primitivos Unity (cilindro alongado com modificação de mesh via ProBuilder) + Material URP vermelho-terracota
- **Função:** Representação abstrata da obra monumental de 33m da artista recifense; elemento central do percurso, posicionado em uma colina gerada por Terrain.

### ASSET 3

- **Nome:** Painel Informativo Flutuante
- **Tipo:** Prefab UI (Canvas em modo World Space)
- **Origem:** Criado no Unity com componentes TextMeshPro e Image
- **Função:** Exibir título da obra, nome do artista e breve descrição ao se aproximar de cada instalação; ativado por trigger de proximidade via script C#.

### ASSET 4

- **Nome:** Vegetação Tropical Estilizada
- **Tipo:** Objeto 3D / Sprite Billboard
- **Origem:** Unity Asset Store — pacote gratuito "Low Poly Vegetation Kit"
- **Função:** Compor o ambiente de parque botânico ao longo do percurso, referenciando o programa de reflorestamento da Usina com mais de 600 espécies de plantas.

### ASSET 5

- **Nome:** Skybox Entardecer Nordestino
- **Tipo:** Material Skybox (6-sided ou Procedural)
- **Origem:** Unity Asset Store — pacote gratuito "Atmospheric Scattering" ou Skybox Procedural nativo do Unity com configuração manual de cor (tons laranja/amarelo quente)
- **Função:** Criar a atmosfera visual de fim de tarde característica do interior de Pernambuco, com iluminação dourada (Golden Hour) sobre o ambiente.

### ASSET 6

- **Nome:** Fachada Industrial da Usina
- **Tipo:** Objeto 3D (Primitivos + ProBuilder)
- **Origem:** Modelagem com cubos, planos e cilindros (chaminés) no Unity
- **Função:** Elemento de fundo (background) que compõe o skybox e dá identidade industrial ao cenário, referenciando a arquitetura real da Usina Santa Terezinha.

---

## SEÇÃO 5 — INTERAÇÃO OBRIGATÓRIA (C#)

**5.1 Descrição da Interação:**

A interação principal implementada é o **Painel Informativo por Aproximação**: ao se aproximar de qualquer uma das 5 obras do percurso, um painel flutuante em World Space é exibido com o título da obra, nome do artista e uma breve descrição. Ao se afastar, o painel desaparece. Esta interação é coerente com o contexto de museu — replicando digitalmente o comportamento de uma plaquinha informativa que o visitante lê ao se aproximar de uma escultura.

**5.2 Script C# — `PainelInfo.cs`:**

```csharp
using UnityEngine;

/// <summary>
/// Exibe e oculta um painel informativo quando o jogador
/// entra ou sai da zona de proximidade de uma obra de arte.
/// Attach: colocar este script no GameObject que contém o Collider Trigger
/// da obra. Arrastar o painel (Canvas World Space) no campo 'painelUI'.
/// </summary>
public class PainelInfo : MonoBehaviour
{
    [Header("Referências")]
    [Tooltip("Canvas World Space com as informações da obra")]
    public GameObject painelUI;

    [Header("Tag do Jogador")]
    [Tooltip("Tag usada pelo XR Origin / Camera Rig")]
    public string tagJogador = "Player";

    // Garante que o painel começa oculto ao iniciar a cena
    private void Start()
    {
        if (painelUI != null)
            painelUI.SetActive(false);
    }

    /// <summary>
    /// Chamado automaticamente quando um Collider entra no trigger.
    /// Verifica se é o jogador e, se for, exibe o painel.
    /// </summary>
    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag(tagJogador))
        {
            if (painelUI != null)
                painelUI.SetActive(true);
        }
    }

    /// <summary>
    /// Chamado automaticamente quando um Collider sai do trigger.
    /// Verifica se é o jogador e, se for, oculta o painel.
    /// </summary>
    private void OnTriggerExit(Collider other)
    {
        if (other.CompareTag(tagJogador))
        {
            if (painelUI != null)
                painelUI.SetActive(false);
        }
    }
}
```

**5.3 Como configurar na cena:**

1. Selecionar o GameObject da obra (ex: `Obra_Diva`);
2. Adicionar um componente **Sphere Collider** com `Is Trigger = true` e raio de ~3 unidades (zona de proximidade);
3. Adicionar o script `PainelInfo.cs` ao mesmo GameObject;
4. No campo `Painel UI` do Inspector, arrastar o `Canvas` filho `Painel_Info_Diva`;
5. Garantir que o XR Origin (Camera Rig) possui a Tag **"Player"** configurada;
6. Repetir o processo para cada uma das 5 obras da cena.

**5.4 Interação Secundária — Mudança de Cor por Clique (XR Simple Interactable):**

Como segunda interação, as obras possuem um componente **XR Simple Interactable** que, ao ser ativado pelo raio do controlador, alterna o material da obra entre a cor original e um destaque luminoso (emissivo), indicando visualmente que o objeto foi selecionado pelo visitante.

```csharp
using UnityEngine;
using UnityEngine.XR.Interaction.Toolkit;

/// <summary>
/// Alterna o material de uma obra entre o estado normal e o estado
/// destacado (emissivo) quando o usuário interage com ela via raio XR.
/// Attach: colocar no mesmo GameObject que tem o XR Simple Interactable.
/// </summary>
[RequireComponent(typeof(XRSimpleInteractable))]
public class ObraDestaque : MonoBehaviour
{
    [Header("Materiais")]
    [Tooltip("Material original da obra")]
    public Material materialNormal;

    [Tooltip("Material com emissão ativa (destaque ao ser selecionada)")]
    public Material materialDestacado;

    // Referência ao Renderer do mesh da obra
    private Renderer _renderer;

    // Controla o estado atual (normal ou destacado)
    private bool _destacado = false;

    private void Awake()
    {
        // Obtém o Renderer na inicialização para evitar GetComponent repetido
        _renderer = GetComponent<Renderer>();
    }

    private void OnEnable()
    {
        // Registra o callback no evento de ativação do XR Interactable
        GetComponent<XRSimpleInteractable>().activated.AddListener(AlternarDestaque);
    }

    private void OnDisable()
    {
        // Remove o callback ao desativar para evitar vazamento de memória
        GetComponent<XRSimpleInteractable>().activated.RemoveListener(AlternarDestaque);
    }

    /// <summary>
    /// Alterna entre material normal e material destacado a cada ativação.
    /// </summary>
    private void AlternarDestaque(ActivateEventArgs args)
    {
        _destacado = !_destacado;
        _renderer.material = _destacado ? materialDestacado : materialNormal;
    }
}
```

---

## SEÇÃO 6 — HIERARQUIA DE GAME OBJECTS

```
Scene: UsinaVR_Museu
│
├── [--- MANAGEMENT ---]
│   ├── EventSystem
│   ├── GameManager
│   └── XR_DeviceSimulator (ativo apenas no Editor)
│
├── [--- PLAYER ---]
│   └── [BuildingBlock] XR Origin (Camera Rig)
│       ├── Camera Offset
│       │   ├── Main Camera (Head)
│       │   ├── LeftHand Controller
│       │   └── RightHand Controller
│       └── Locomotion System
│           ├── Teleportation Provider
│           └── Snap Turn Provider
│
├── [--- ENVIRONMENT ---]
│   ├── Terrain (Chão + Colinas)
│   ├── Directional Light (Golden Hour)
│   ├── Skybox_Volume
│   ├── [Vegetacao]
│   │   ├── Arvore_01 ... Arvore_N
│   │   └── Arbustos_Group
│   └── [Estrutura_Industrial]
│       ├── Fachada_Usina
│       ├── Chamine_01
│       ├── Chamine_02
│       └── Hangar_Fundo
│
├── [--- PONTOS_DE_INTERESSE ---]
│   ├── Locomotiva_Historica
│   │   ├── Mesh_Locomotiva
│   │   └── Painel_Info_Locomotiva
│   ├── Obra_Diva
│   │   ├── Mesh_Diva
│   │   └── Painel_Info_Diva
│   ├── Obra_Paisagem
│   │   ├── Mesh_Paisagem
│   │   └── Painel_Info_Paisagem
│   ├── Obra_Brasil2017
│   │   ├── Mesh_Brasil2017
│   │   └── Painel_Info_Brasil2017
│   └── Obra_RadioCatimbo
│       ├── Mesh_RadioCatimbo
│       └── Painel_Info_RadioCatimbo
│
└── [--- INTERACTABLES ---]
    ├── TriggerZone_Entrada
    ├── TriggerZone_Diva
    ├── TriggerZone_Paisagem
    ├── TriggerZone_Brasil2017
    └── TriggerZone_RadioCatimbo
```

---

## SEÇÃO 7 — PLANEJAMENTO DO REPOSITÓRIO GITHUB

- **6.1 Nome do Repositório:** `UsinaVR-Museu-Digital`

- **6.2 Estrutura de Pastas:**

```
UsinaVR-Museu-Digital/
├── Assets/
│   ├── _Project/
│   │   ├── Scripts/          # Scripts C# do projeto
│   │   ├── Prefabs/          # Prefabs reutilizáveis
│   │   ├── Materials/        # Materiais e shaders
│   │   ├── Scenes/           # Cenas Unity (.unity)
│   │   └── UI/               # Elementos de interface
│   ├── ThirdParty/           # Assets importados da Asset Store
│   └── XR/                   # Configurações do Meta XR SDK
├── ProjectSettings/          # Configurações do projeto Unity
├── Packages/                 # manifest.json e packages
├── .gitignore                # Ignora /Library, /Temp, /Logs, /obj
└── README.md                 # Documentação obrigatória do projeto (ver Seção 6.3)
```

- **6.3 Conteúdo obrigatório do README.md:**

O arquivo `README.md` na raiz do repositório deve conter os seguintes tópicos:

```markdown
# UsinaVR — Museu Digital Imersivo

**Aluno:** Joney Sousa Pereira

## Apresentando o Projeto
UsinaVR é uma experiência em Realidade Virtual que recria um percurso
imersivo pelo acervo da Usina de Arte (Água Preta/PE), permitindo que
qualquer pessoa visite e interaja com as obras do museu a céu aberto
diretamente de um headset Meta Quest ou pelo editor Unity no PC.

## Contexto e Objetivos
O ambiente representa um espaço de entretenimento cultural e educação
no Metaverso. O problema resolvido é a barreira geográfica de acesso
à Usina de Arte, localizada a 150 km de Recife sem transporte público
direto. A experiência VR democratiza o acesso ao patrimônio artístico
do Nordeste, com foco especial em estudantes de escolas públicas e
pessoas com mobilidade reduzida.

## Processo de Criação e Dificuldades
[Descrever etapas seguidas, ferramentas usadas e principais desafios
encontrados durante o desenvolvimento — a preencher após execução]

## Como Abrir o Projeto
1. Instalar Unity 6 LTS via Unity Hub
2. Clonar este repositório
3. Abrir a pasta raiz no Unity Hub > Add project from disk
4. Aguardar importação dos packages
5. Abrir a cena em Assets/_Project/Scenes/UsinaVR_Museu.unity
6. Pressionar Play para testar com o XR Device Simulator
```

- **6.4 .gitignore:** Incluir exclusões de `/Library/`, `/Temp/`, `/Logs/`, `/obj/`, `*.csproj`, `*.sln` e arquivos de build local.

---

## SEÇÃO 8 — PLANO DE EXECUÇÃO PASSO A PASSO

1. **Etapa 1 — Setup do ambiente de desenvolvimento:** Instalação do Unity 6 LTS via Unity Hub; criação do projeto 3D com template URP (Universal Render Pipeline); configuração inicial do controle de versão com Git e `.gitignore` adequado para Unity.

2. **Etapa 2 — Importação e configuração do Meta XR SDK:** Instalação do Meta XR All-in-One SDK via Package Manager; execução do Project Setup Tool para aplicar todas as configurações automáticas recomendadas; adição do prefab `XR Origin` e do `XR Device Simulator` à cena.

3. **Etapa 3 — Configuração da Build para Android:** Switch Platform para Android no Build Settings; configuração de textura ASTC, API Level 29+ e IL2CPP; ativação do plugin Oculus no XR Plugin Management.

4. **Etapa 4 — Construção do terreno e ambiente base:** Criação do terreno com ferramenta Terrain do Unity (colina para a obra "Diva", percurso plano central, limites com vegetação); aplicação da textura de grama e terra; posicionamento do Directional Light com cor quente (RGB ~255, 180, 80) simulando o entardecer.

5. **Etapa 5 — Modelagem dos elementos com ProBuilder e Primitivos:** Criação da locomotiva histórica com cilindros e cubos; fachada da usina e chaminés ao fundo; estrutura abstrata das 5 obras de referência; aplicação de materiais URP com cores sólidas e bump maps simples.

6. **Etapa 6 — Importação de assets da Asset Store:** Download e importação do pacote de vegetação Low Poly; distribuição das árvores e arbustos ao longo do percurso; configuração do Skybox com tons de entardecer nordestino.

7. **Etapa 7 — Implementação dos scripts de interação C#:** Criação do script `PainelInfo.cs` com lógica de `OnTriggerEnter`/`OnTriggerExit` para cada obra; criação do script `ObraDestaque.cs` integrado ao `XRSimpleInteractable` para alternância de material; configuração dos Sphere Colliders como triggers nas 5 obras; atribuição da tag "Player" ao XR Origin; comentários de código em todas as funções conforme exigido.

8. **Etapa 8 — Organização da hierarquia, nomenclatura e README.md:** Agrupamento de todos os objetos em pastas lógicas conforme hierarquia definida na Seção 6; revisão de nomenclatura de todos os GameObjects; remoção de assets não utilizados; criação do `README.md` com todos os tópicos obrigatórios (apresentação do projeto, contexto/objetivo no Metaverso, processo de criação e dificuldades).

9. **Etapa 9 — Teste via XR Device Simulator e ajustes finais:** Validação da navegação completa pelo percurso no Editor; teste de todos os triggers de painéis informativos; ajuste de escala dos objetos (o avatar padrão tem ~1,75m de altura como referência); verificação de performance (Draw Calls alvo: abaixo de 100 para garantir 72fps no Quest).

10. **Etapa 10 — Push para GitHub e entrega:** Commit final com mensagem descritiva; push do repositório para o GitHub com as pastas `Assets/`, `ProjectSettings/` e `Packages/`; verificar que o `README.md` está na raiz do repositório com todos os tópicos obrigatórios; geração do arquivo `link-repositorio.txt` com a URL pública do repositório para envio na plataforma Homero.

---

## SEÇÃO 9 — REFLEXÃO FINAL

**8.1 Aprendizado:**

Este projeto permitiu compreender na prática como a Realidade Virtual pode ser aplicada à preservação e democratização do acesso ao patrimônio cultural. A principal lição técnica foi entender a importância da hierarquia organizada de GameObjects para um projeto escalável — especialmente ao trabalhar com múltiplos pontos de interesse, cada um com sua própria lógica de trigger e UI. Também ficou clara a relevância do XR Interaction Toolkit como camada de abstração que padroniza interações entre diferentes plataformas XR, reduzindo o trabalho de configuração manual de inputs.

Do ponto de vista conceitual, o projeto evidencia como a tecnologia VR pode resolver problemas reais de inclusão cultural: a Usina de Arte é um acervo extraordinário que permanece inacessível para a maioria dos brasileiros devido à barreira geográfica. Uma experiência digital navegável pode ampliar imensamente o alcance educacional e cultural do espaço, especialmente para estudantes de escolas públicas do Nordeste.

**8.2 Dificuldades Previstas:**

A principal dificuldade técnica antecipada é a **otimização de performance para o hardware mobile do Meta Quest**, que possui capacidade de processamento significativamente inferior a um PC. Ambientes com vegetação densa e múltiplos objetos facilmente ultrapassam o limite de Draw Calls recomendado para 72fps. As estratégias de mitigação previstas incluem: uso de assets Low Poly, GPU Instancing para vegetação repetida, Occlusion Culling ativado, e Level of Detail (LOD) para objetos distantes. Outra dificuldade esperada é a calibração de escala dos elementos 3D para que façam sentido na perspectiva em primeira pessoa com altura de avatar realista.

**8.3 Melhorias Futuras:**

Como evolução natural do projeto após esta primeira fase, seriam implementadas:

- **Áudio ambiental imersivo:** sons de pássaros, vento e ambiente rural do interior pernambucano, utilizando o Audio Mixer do Unity com reverberação espacial 3D;
- **Galeria expandida:** inclusão digital de todas as mais de 40 obras do acervo real da Usina de Arte, com fotos em alta resolução aplicadas como texturas em painéis;
- **Modo visita guiada:** um guia virtual narrado (Text-to-Speech ou áudio pré-gravado) que acompanha o usuário pelo percurso, contando a história de cada obra e do espaço;
- **Suporte multiplayer:** integração com o Photon Unity Networking (PUN 2) para permitir que grupos de estudantes visitem o museu virtual simultaneamente, viabilizando visitas escolares remotas;
- **Build para Meta Quest APK:** com a infraestrutura montada nesta fase, a compilação para o dispositivo físico seria o próximo passo direto, tornando a experiência verdadeiramente imersiva com o headset.
