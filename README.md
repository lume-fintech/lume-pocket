# 📱 Desafio Técnico: Lume Pocket

Este é o desafio técnico de preparação para a equipe de desenvolvimento do **Projeto LUME**.

**Objetivo:** Este não é um teste de aprovação ou reprovação. O objetivo é simular o fluxo de trabalho real que teremos no projeto principal, garantindo que todos estejam alinhados com os padrões de código, versionamento e entrega.

---

## 🎯 O Escopo do App

Você desenvolverá o **Lume Pocket**, um gerenciador de tarefas simplificado. O foco não é a complexidade visual, mas a estrutura e o funcionamento lógico.

### Funcionalidades
1.  **Tela Home (Lista):**
    * Exibir uma lista de atividades (Ex: "Estudar Widgets", "Daily Lume", "Configurar Ambiente").
    * **Técnica:** Obrigatório uso de `ListView.builder`.
    * **Interação:** Um botão flutuante (FAB) que adiciona um item novo à lista ao ser clicado (apenas atualização de estado local).
2.  **Tela de Detalhes:**
    * Ao clicar em um item da lista, navegar para uma segunda tela.
    * Exibir o título da atividade e uma descrição (texto fictício).
    * Botão de voltar para a Home.

---

## 🧐 Critérios de Avaliação (O que estamos olhando)

A qualidade da entrega será medida pelos seguintes pilares:

### 1. Organização e Conventional Commits (Peso Alto ⭐)
Não queremos apenas o código pronto. Queremos ver a **história** da construção do app através do Git.
* **Atomicidade:** Não faça um único commit com tudo pronto. Faça commits a cada funcionalidade ou componente criado.
* **Padrão Obrigatório:** Utilize o [Conventional Commits](https://www.conventionalcommits.org/pt-br).
    * `feat: adiciona estrutura da tela home`
    * `fix: corrige erro de overflow na lista`
    * `docs: atualiza readme com instruções`
    * `style: ajusta cores do card`

### 2. Estrutura de Projeto (Padrão MVVM)

A organização das pastas é o critério mais importante desta etapa. Você deve separar claramente quem desenha a tela de quem processa a lógica.

Estrutura sugerida:

```text
lib/
├── models/         # [MODEL] O "O Que": Classes de dados puras (ex: Task). Sem import de material.dart.
├── viewmodels/     # [VIEWMODEL] O "Como": Classes com a lógica e estado (ex: TaskViewModel).
├── views/          # [VIEW] O "Onde": As telas do App (HomeView, DetailsView). Só desenham e chamam a ViewModel.
├── components/     # Widgets visuais reutilizáveis (botões customizados, cards, itens de lista).
└── main.dart       # Ponto de entrada e configurações iniciais.
```

## 📚 Material de Estudo: Arquitetura

Para cumprir este desafio, você não pode apenas "fazer funcionar". Você precisa "organizar a casa". Antes de começar a codar, leia atentamente os conceitos abaixo.

### 1. Por que Arquitetura? (O Problema do Código Espaguete)
No desafio anterior, vocês provavelmente colocaram variáveis, funções e widgets tudo misturado dentro do arquivo da tela.
* **Problema:** Se o app crescer, vira uma bagunça impossível de manter.
* **Solução:** Separar responsabilidades. Quem desenha na tela não deve saber fazer conta. Quem faz conta não deve saber desenhar na tela.

### 2. O Padrão Escolhido pro LUME: MVVM (Model - View - ViewModel)
O Flutter funciona muito bem com este padrão porque ele é **Reativo**.

* **Model:** É o dado puro (Ex: A classe `Tarefa` com título e descrição). Não sabe que o app existe.
* **View:** É a tela (Widgets). Ela é "burra". Ela só mostra o que a ViewModel manda e avisa quando o usuário clicou em algo.
* **ViewModel:** É o cérebro. Ela guarda a lista de tarefas, tem a função de `adicionarTarefa()`, e avisa a View quando os dados mudaram.

### 🆚 Comparação: MVC vs MVVM
Muitos tutoriais antigos ensinam MVC. Veja a diferença para não confundir:

| Característica | MVC (Model-View-Controller) | MVVM (Model-View-ViewModel) 🏆 |
| :--- | :--- | :--- |
| **Quem manda?** | O **Controller** manda na View. Ele diz: *"Tela, mude o texto para 'Olá'!"* | A **View** observa a ViewModel. A ViewModel diz: *"O texto agora é 'Olá'"* e a View se atualiza sozinha. |
| **Dependência** | O Controller precisa conhecer a View. | A ViewModel **NÃO CONHECE** a View. Ela não sabe quem está assistindo ela. |
| **No Flutter** | Menos comum para gestão de estado moderna. | **Padrão da Indústria.** Usa-se `ChangeNotifier` ou `ValueNotifier` para essa comunicação. |

> **Resumo da Ópera:** No MVC, o Controller empurra a mudança para a tela. No MVVM, a Tela fica "escutando" as mudanças do ViewModel. **Neste desafio, queremos MVVM.**

### 🔗 Onde Estudar (Recomendações)

Não tentem implementar arquiteturas complexas como Clean Architecture agora. Foquem no **MVVM Simples com ChangeNotifier**.

1.  **Gerência de Estado Nativa (Essencial):**
    * Pesquise por: *"Flutter ChangeNotifier e AnimatedBuilder tutorial"*.
    * Este é o jeito nativo do Flutter fazer a View escutar a ViewModel sem precisar de bibliotecas externas.

2.  **Vídeos Recomendados:**
    * **Canal Flutterando:** Procure por vídeos sobre "Arquitetura MVVM" ou "Gerência de Estado".
    * **Conceito:** Procure vídeos que expliquem "Separação de View e Regra de Negócio".

3.  **Dica de Ouro:**
    Se no seu arquivo `home_view.dart` tiver um `setState` que altera uma regra de negócio (ex: adicionar item na lista), **está errado**. O `setState` na View deve servir apenas para coisas visuais (ex: mudar a cor de um botão ao clicar). A lista de dados deve ser alterada dentro da `ViewModel`.

---


## 3. Entrega Final (Build)

Você deve provar que seu ambiente é capaz de gerar o aplicativo final para Android.

* O repositório deve conter o código fonte.
* Você deve gerar e disponibilizar o arquivo `.apk`.

## 🤖 IA Report (Obrigatório)

Assim como em desafios anteriores, você deve entregar um relatório sobre como utilizou a Inteligência Artificial.

Crie um arquivo `IA_REPORT.md` na raiz do projeto contendo:

* **Prompts:** O que você perguntou?
* **Contribuição:** Onde a IA ajudou mais (código, lógica, correção de erros)?
* **O que aprendeu:** O que você entendeu graças à explicação da IA?
* **Autoria:** Confirmação de que você testou e entendeu o código gerado.

## 📚 Material de Apoio

* **Roadmap de Estudos:** [https://github.com/Flutterando/Roadmap](https://github.com/Flutterando/Roadmap)
* **Conventional Commits:** [Guia Prático](https://www.conventionalcommits.org/pt-br/)

## 🚀 Como Entregar

### 1. Repositório
1.  Crie um repositório no seu GitHub.
2.  Suba o projeto seguindo os padrões de commit (Conventional Commits).
3.  O `IA_REPORT.md` deve estar na raiz do projeto.

### 2. O Executável (APK)
Você deve gerar a versão de instalação para Android. Para otimizar o tamanho do aplicativo, utilizaremos a divisão por arquitetura.

**Passo a passo:**

1.  No terminal, rode o comando:
    ```bash
    flutter build apk --split-per-abi
    ```
    *(Isso vai demorar um pouco mais que o normal, pois ele está compilando 3 versões diferentes).*

2.  Após finalizar, vá até a pasta:
    `[seu-projeto]/build/app/outputs/flutter-apk/`

3.  Você verá três arquivos APK lá:
    * `app-armeabi-v7a-release.apk` (Celulares mais antigos/32bits)
    * `app-arm64-v8a-release.apk` (Celulares modernos/64bits) 🟢 **(É ESSE AQUI)**
    * `app-x86_64-release.apk` (Emuladores)

4.  **Envie APENAS o arquivo `app-arm64-v8a-release.apk`.**
    * *Nota: Se você não souber onde está a pasta, pode clicar com o botão direito na pasta `build` no seu editor e escolher "Open in Explorer" ou "Reveal in Finder".*

---

## 🎨 Referência Visual (Layout)

Não esperamos um design digno de prêmio, mas a estrutura deve seguir o padrão **Material Design**.

Abaixo estão os protótipos de referência ("Mockups") do que esperamos visualmente. Usem como guia para posicionar os elementos (Cards, Textos, Botões).

### Tela 1: Home (Lista de Tarefas)
*Observem o uso do botão flutuante (FAB) e o espaçamento entre os cards.*

![Layout da Home](layout_home.png)
*(Se a imagem não carregar: imagine uma lista vertical onde cada item tem ícone, título e subtítulo, com um botão "+" no canto inferior direito)*

### Tela 2: Detalhes da Tarefa
*Observem o botão de voltar no topo e a hierarquia dos textos (Título grande, descrição menor).*

![Layout de Detalhes](layout_details.png)

---


## 🚀 Boa sorte, estamos a disposição para tirar dúvidas!


