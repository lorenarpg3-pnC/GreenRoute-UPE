# GreenRoute — Sistema Inteligente de Logística para Veículos Elétricos e Híbridos

<p align="center">
  <img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java">
  <img src="https://img.shields.io/badge/Architecture-MVC-blue?style=for-the-badge" alt="MVC">
  <img src="https://img.shields.io/badge/UPE-Surubim-red?style=for-the-badge" alt="UPE">
</p>

O **GreenRoute** é um sistema de gerenciamento de rotas intermunicipais projetado para mitigar os desafios de planejamento logístico impostos pela eletrificação veicular. O sistema gerencia frotas de veículos (elétricos e híbridos), malhas rodoviárias de cidades e a infraestrutura de eletropostos disponíveis, utilizando arquitetura modular e integração com Inteligência Artificial.

Este repositório central funciona como o **Hub Oficial da Disciplina**, centralizando as implementações e soluções desenvolvidas pelas equipes de estudantes.

---

## 📌 Contexto e Justificativa

A transição para a mobilidade sustentável exige um planejamento rigoroso de autonomia. Fatores dinâmicos como a distância entre municípios, a velocidade máxima das vias, a compatibilidade de conectores de eletropostos e a taxa de consumo energético determinam a viabilidade de uma viagem. 

O projeto simula um ecossistema logístico estruturado estritamente sob o padrão arquitetural **MVC (Model-View-Controller)**, dividindo-se em duas grandes etapas de maturidade de software:
1. **Módulo 1:** Persistência estática em memória, manipulação robusta de estruturas de dados nativas (Arrays) e interface via console.
2. **Módulo 2:** Interface Gráfica (GUI), coleções dinâmicas (ArrayList) e tomada de decisão inteligente integrada a Large Language Models (LLM) via API.

---

## 🏗️ Especificação Técnica das Entidades (Model)

O núcleo do sistema é composto pelo mapeamento rigoroso das seguintes entidades e atributos:

### 🧩 Diagrama de Entidades

*   **`Veiculo`** *(Classe Abstrata)*
    *   `int id` (Identificador numérico único sequencial)
    *   `String modelo`
    *   `double autonomiaMaxima` (em km com carga completa)
    *   `double cargaBateriaAtual` (porcentagem de 0.0 a 100.0)
    *   `double consumoKwhPorKm` (taxa média de consumo)
    *   `int tempoRecargaCompleta` (tempo em minutos de 0% a 100%)
    *   **`VeiculoEletrico`** *(Subclasse)*
        *   `String tipoConector` (Ex: Tipo 2, CCS2, CHAdeMO)
        *   `int tempoRecargaRapida` (em minutos em alta potência)
    *   **`VeiculoHibrido`** *(Subclasse)*
        *   `double capacidadeTanqueCombustivel` (em litros)
        *   `double consumoCombustivel` (em km/l no motor a combustão)
        *   `String tipoCombustivel` (Ex: Gasolina, Etanol)

*   **`Eletroposto`**
    *   `int id` (Identificador numérico único)
    *   `String nome`
    *   `String localizacao` (Endereço/Rodovia)
    *   `int cidadeId` (Vínculo numérico com a Cidade)
    *   `String tiposConectoresDisponiveis` (Ex: "CCS2, Tipo 2" - múltiplos)
    *   `double potenciaCargaKw` (Ex: 50.0 Kw, 150.0 Kw)
    *   `double precoPorKwh` (Valor cobrado pelo kWh)
    *   `int vagasDisponiveis`

*   **`Cidade`**
    *   `int id` (Código IBGE ou identificador único)
    *   `String nome`
    *   `String estado` (UF)
    *   `double distanciaDaCapital` (em km)

---

## 🎯 Cronograma de Módulos e Requisitos

### 🔹 Módulo 1: Estrutura Base e CRUD com Arrays (50% da Nota)
*   **Arquitetura:** Divisão estrita em pacotes `model`, `repository` e `controller`.
*   **Estruturas de Dados:** Uso obrigatório e exclusivo de **Arrays Tradicionais (`[]`)** para armazenamento em memória, tratando o crescimento da alocação de forma robusta.
*   **Interface:** Console interativo estruturado com laços `while` e condicionais `switch/case`.
*   **Regra de Negócio Inicial:** Simulação de rota calculando se a autonomia atual do veículo (`autonomiaMaxima * (cargaBateriaAtual / 100)`) cobre a distância até o destino. Caso seja insuficiente, o controlador realiza uma busca linear nos repositórios para sugerir eletropostos compatíveis com base no `cidadeId`.

### 🔹 Módulo 2: GUI, ArrayList e Roteirização Automatizada por LLM (50% da Nota)
*   **Refatoração:** Migração completa de arrays fixos para coleções dinâmicas **`java.util.ArrayList`**.
*   **Interface Gráfica (GUI):** Abandono completo do console. Telas completas de gerenciamento desenvolvidas em **Java Swing** ou **JavaFX** com tabelas visuais e modais.
*   **Tratamento de Exceções:** Lançamento de exceções personalizadas (Ex: `AutonomiaInsuficienteException`, `ConectorIncompativelException`) capturadas graficamente via alertas amigáveis (`JOptionPane`).
*   **Integração com IA (LLM):** 
    *   *Ação 1 (Cadastro Rápido):* Processamento de texto livre através de IA para extração de dados estruturados e preenchimento automatizado de formulários.
    *   *Ação 2 (Planejador Inteligente):* Motor de tomada de decisão enviando dados de autonomia e recarga combinados com dados simulados em tempo real (trânsito, clima) para geração de rotas descritivas pela LLM.
*   **Bônus:** Integração com a **API do Google Maps** para plotagem visual de rotas ou cálculo real de matriz de distância.

---

## 🚀 Como Contribuir / Enviar o Projeto (Instruções para Alunos)

Para evitar conflitos de código na *branch main*, as entregas serão isoladas por subpastas. Siga o protocolo abaixo:

1.  **Faça um Fork** deste repositório central para a sua conta do GitHub.
2.  No seu Fork, navegue até o diretório `/grupos/` e crie uma subpasta com o número do seu grupo (Ex: `/grupos/grupo_03/`).
3.  Desenvolva todo o projeto da sua equipe dentro dessa pasta específica.
4.  Certifique-se de que seus commits foram realizados dentro do prazo estipulado para cada módulo.
5.  Abra um **Pull Request (PR)** direcionado à *branch main* deste repositório usando o padrão de título: `[Módulo X] - Grupo XX - NomeEstudante1 e NomeEstudante2`.

---

## 🧑‍🏫 Orientação e Coordenação

*   **Professor Orientador:** Marcondes Ricarte da Silva Júnior
*   **Instituição:** Universidade de Pernambuco (UPE) — Campus Surubim
*   **Contexto:** Atividade Prática de Fixação - Programação Orientada a Objetos / Engenharia de Software

---

<p align="center">
  Desenvolvido para fins acadêmicos e científicos no ecossistema de soluções de IA & Mobilidade. ⭐ Deixe uma estrela no repositório para apoiar o projeto!
</p>