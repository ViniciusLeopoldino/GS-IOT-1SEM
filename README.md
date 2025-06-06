# SMAE - Sistema de Monitoramento e Alerta de Enchentes

![Status](https://img.shields.io/badge/status-conclu%C3%ADdo-brightgreen)

## Tabela de Conteúdos
1. [Descrição do Projeto](#1-descrição-do-projeto)
2. [Funcionalidades](#2-funcionalidades)
3. [Arquitetura da Solução](#3-arquitetura-da-solução)
4. [Tecnologias e Componentes](#4-tecnologias-e-componentes)
5. [Justificativas Técnicas](#5-justificativas-técnicas)
6. [Demonstração (Evidências)](#6-demonstração-evidências)
7. [Como Executar o Projeto](#7-como-executar-o-projeto-guia-de-instalação)
8. [Autor](#8-autor)

---

## 1. Descrição do Projeto
O **SMAE** é um protótipo de um sistema de Internet das Coisas (IoT) projetado para monitorar em tempo real as condições ambientais que podem levar a enchentes em áreas urbanas. A solução utiliza sensores para coletar dados críticos como nível da água, temperatura e umidade, processa essas informações e aciona alertas visuais e sonoros, além de exibir tudo em um dashboard online para acompanhamento remoto.

Este projeto foi desenvolvido como uma solução para o desafio de criar um sistema IoT funcional, desde a simulação do hardware até a visualização dos dados em uma plataforma de monitoramento.

## 2. Funcionalidades
-   ✅ **Monitoramento em Tempo Real:** Coleta de dados de nível da água, temperatura e umidade a cada 5 segundos.
-   ✅ **Sistema de Alerta em Três Níveis:**
    -   **Normal (Verde):** Condições seguras.
    -   **Alerta (Amarelo):** Nível da água subindo, requer atenção.
    -   **Perigo (Vermelho):** Nível crítico, com acionamento de alarme sonoro para evacuação imediata.
-   ✅ **Comunicação via MQTT:** Utiliza um dos protocolos mais eficientes para IoT, garantindo comunicação leve e em tempo real entre o dispositivo e o gateway.
-   ✅ **Dashboard Interativo:** Painel de controle desenvolvido em Node-RED para visualização remota dos dados através de medidores, gráficos históricos e indicadores de status.

## 3. Arquitetura da Solução
O sistema opera com uma arquitetura distribuída, onde o dispositivo de campo (simulado no Wokwi) se comunica com o dashboard através de um broker MQTT na nuvem.

`Wokwi (ESP32)` → `Wi-Fi` → `Internet (Broker MQTT HiveMQ)` → `Internet` → `Node-RED (Gateway/Dashboard)`

---

## 4. Tecnologias e Componentes

### Hardware (Simulado)
* Microcontrolador: **ESP32 DevKit V1**
* Sensor de Nível d'Água: **Sensor Ultrassônico HC-SR04**
* Sensor Ambiental: **Sensor de Temperatura e Umidade DHT22**
* Atuadores Visuais: **LED Verde, LED Amarelo, LED Vermelho**
* Atuador Sonoro: **Buzzer**

### Software & Cloud
* Simulador de Hardware: **Wokwi**
* Gateway e Dashboard: **Node-RED**
* Protocolo de Comunicação: **MQTT**
* Broker MQTT: **HiveMQ Public Broker**
* Bibliotecas Arduino: `WiFi`, `PubSubClient`, `DHT`, `ArduinoJson`

## 5. Justificativas Técnicas
A escolha dos componentes foi baseada na eficácia, custo e relevância para o problema proposto:

> **Sensor Ultrassônico (HC-SR04):** Escolhido por sua precisão e baixo custo para medir a distância, permitindo calcular o nível da água de forma eficaz e sem contato direto.
>
> **Sensor de Temperatura e Umidade (DHT22):** Adicionado para fornecer contexto ambiental. Picos de umidade e quedas de temperatura podem ser indicadores de chuva iminente, agregando uma camada extra de dados para futuras análises de previsão.
>
> **LEDs (Verde, Amarelo, Vermelho):** Utilizados como um sistema de alerta visual imediato e intuitivo, seguindo um padrão semafórico universalmente compreendido (Normal, Alerta, Perigo).
>
> **Buzzer:** Selecionado como um atuador de alerta sonoro, essencial para chamar a atenção de forma urgente em situações críticas de perigo, mesmo que ninguém esteja olhando para o painel de LEDs.

---

## 6. Demonstração (Evidências)

### Vídeo de Funcionamento
![GIF do Projeto](https://youtu.be/ZxqEnVOUHW4 "Demonstração do SMAE em funcionamento")

### Dashboard em Diferentes Estados

| Estado Normal | Estado de Alerta | Estado de Perigo |
| :---: | :---: | :---: |
| | | |
| ![Dashboard Normal](https://placeholder.com/dashboard-normal "Dashboard em Estado Normal") | ![Dashboard Alerta](https://placeholder.com/dashboard-alerta "Dashboard em Estado de Alerta") | ![Dashboard Perigo](https://placeholder.com/dashboard-perigo "Dashboard em Estado de Perigo") |

### Arquitetura do Projeto

| Circuito no Wokwi | Fluxo no Node-RED |
| :---: | :---: |
| | |
| ![Circuito Wokwi](https://placeholder.com/circuito "Circuito montado no Wokwi") | ![Fluxo Node-RED](https://placeholder.com/fluxo "Fluxo de dados no Node-RED") |

---

## 7. Como Executar o Projeto (Guia de Instalação)
Para executar este projeto, siga os passos abaixo.

### Parte 1: Configuração do Hardware Virtual (Wokwi)
1.  **Acesse o Wokwi:** Crie ou acesse sua conta em [wokwi.com](https://wokwi.com/).
2.  **Crie um novo projeto** com o ESP32.
3.  **Configure o Diagrama:** Copie o conteúdo do arquivo `diagram.json` abaixo e cole na aba correspondente do seu projeto Wokwi.

    ```json
    ```

4.  **Adicione as Bibliotecas:** Clique no botão azul `+` no editor de código e adicione as seguintes bibliotecas:
    * `WiFi` (geralmente já inclusa)
    * `PubSubClient`
    * `DHT sensor library`
    * `ArduinoJson`

5.  **Adicione o Código:** Copie o código do `sketch.ino` abaixo e cole no editor principal do Wokwi.

    ```cpp
    ```

### Parte 2: Configuração do Gateway e Dashboard (Node-RED)
1.  **Pré-requisitos:** Certifique-se de ter o Node-RED instalado e rodando, com o pacote `node-red-dashboard` instalado.
2.  **Importe o Fluxo:** Copie todo o código JSON abaixo. No seu Node-RED, vá em `Menu (☰) > Import` e cole o código.

    ```json
    ```

3.  **Faça o Deploy:** Clique no botão "Deploy" para ativar o fluxo. O nó `mqtt in` deve mostrar o status "connected".

### Parte 3: Testando a Solução Completa
1.  Inicie a simulação no Wokwi clicando no botão de play (▶).
2.  Abra o Monitor Serial no Wokwi para acompanhar as mensagens de conexão e publicação MQTT.
3.  Acesse seu dashboard do Node-RED (geralmente em `http://127.0.0.1:1880/ui`).
4.  Observe o painel sendo atualizado automaticamente. Interaja com os sensores no Wokwi (principalmente o sensor ultrassônico) e veja as mudanças refletidas em tempo real no dashboard.

---

## 8. Autor
**[Seu Nome Completo]**
- [LinkedIn](https://www.linkedin.com/)
- [GitHub](https://github.com/)