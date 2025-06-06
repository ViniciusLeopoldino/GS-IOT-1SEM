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
8. [Grupo](#8-grupo)

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
[Link Youtube](https://youtu.be/ZxqEnVOUHW4 "Demonstração do SMAE em funcionamento")

### Dashboard em Diferentes Estados

| Estado            | Imagem                                                                                               |
|-------------------|------------------------------------------------------------------------------------------------------|
| Estado Normal     | ![Estado Normal](https://github.com/user-attachments/assets/84b08bcb-6cc1-43fc-a4f0-cc7b7868ec10)    |
| Estado de Alerta  | ![Estado de Alerta](https://github.com/user-attachments/assets/217cdd2e-e21c-4426-ac2e-1d4b90343c8b) |
| Estado de Perigo  | ![Estado de Perigo](https://github.com/user-attachments/assets/75d6c41c-fe51-44e0-b775-4bedebbced66) |


### Arquitetura do Projeto

| Arquitetura       | Imagem                                                                                    |
|-------------------|-------------------------------------------------------------------------------------------|
| Circuito no Wokwi | ![image](https://github.com/user-attachments/assets/4c2a07fd-f7ad-4e9c-8ee5-57877b6ba263) |
| Fluxo no Node-RED | ![image](https://github.com/user-attachments/assets/8841ba9a-aefc-44a5-b3fb-0e67f6041c97) |

---

## 7. Como Executar o Projeto (Guia de Instalação)

Para executar este projeto, siga os passos abaixo.

### Parte 1: Configuração do Hardware Virtual (Wokwi)

1.  **Acesse o Projeto no Wokwi:** Clique no badge do Wokwi acima ou acesse o link: [https://wokwi.com/projects/432970311562255361](https://wokwi.com/projects/432970311562255361).
2.  **Visualize o Diagrama:** O circuito com o ESP32 e os sensores estará pronto para visualização.
3.  **Verifique o Código:** O código para o ESP32 (na aba `sketch.ino`) estará carregado. Você pode revisar as configurações de Wi-Fi e MQTT.
4.  **Execute a Simulação:** Clique no botão de play (▶) para iniciar a simulação. O Monitor Serial mostrará a tentativa de conexão Wi-Fi e MQTT.

### Parte 2: Configuração do Gateway e Dashboard (Node-RED)

1.  **Pré-requisitos:** Certifique-se de ter o Node-RED instalado e rodando, com o pacote `node-red-dashboard` instalado (`npm install node-red-dashboard` na pasta do seu Node-RED ou pela paleta de nós).

2.  **Importe o Fluxo:** Copie o código JSON do fluxo do Node-RED abaixo e cole no seu editor Node-RED (Menu → Import).

    ````json
    // [
    {
        "id": "01b6b0c72321aca5",
        "type": "json",
        "z": "357a76de90abc332",
        "name": "Converter para Objeto JSON",
        "property": "payload",
        "action": "obj",
        "pretty": true,
        "x": 480,
        "y": 200,
        "wires": [
            [
                "0f0ed4c7ba7efd71",
                "7709a5cd57c27844",
                "c782202a84c7a607",
                "404c74f7ac716470",
                "3f87461189687424"
            ]
        ]
    },
    {
        "id": "0f0ed4c7ba7efd71",
        "type": "change",
        "z": "357a76de90abc332",
        "name": "Nível da Água",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "payload.nivelAgua",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 750,
        "y": 120,
        "wires": [
            [
                "dd9694d97a6b3ca8",
                "75dacb46ece3b555"
            ]
        ]
    },
    {
        "id": "7709a5cd57c27844",
        "type": "change",
        "z": "357a76de90abc332",
        "name": "Temperatura",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "payload.temperatura",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 750,
        "y": 200,
        "wires": [
            [
                "fab750685abc4252"
            ]
        ]
    },
    {
        "id": "c782202a84c7a607",
        "type": "change",
        "z": "357a76de90abc332",
        "name": "Umidade",
        "rules": [
            {
                "t": "set",
                "p": "payload",
                "pt": "msg",
                "to": "payload.umidade",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 740,
        "y": 280,
        "wires": [
            [
                "6d2d05bf8a20b728"
            ]
        ]
    },
    {
        "id": "dd9694d97a6b3ca8",
        "type": "ui_gauge",
        "z": "357a76de90abc332",
        "name": "Nível da Água",
        "group": "2f4e3f3b.d0b1c",
        "order": 1,
        "width": "4",
        "height": "4",
        "gtype": "gage",
        "title": "Nível da Água",
        "label": "%",
        "format": "{{value}}",
        "min": 0,
        "max": "100",
        "colors": [
            "#5dd85d",
            "#f9d343",
            "#ff0000"
        ],
        "seg1": "60",
        "seg2": "85",
        "diff": false,
        "className": "",
        "x": 1020,
        "y": 100,
        "wires": []
    },
    {
        "id": "75dacb46ece3b555",
        "type": "ui_chart",
        "z": "357a76de90abc332",
        "name": "Histórico Nível da Água",
        "group": "2f4e3f3b.d0b1c",
        "order": 5,
        "width": "12",
        "height": "4",
        "label": "Histórico Nível da Água (%)",
        "chartType": "line",
        "legend": "false",
        "xformat": "HH:mm:ss",
        "interpolate": "linear",
        "nodata": "",
        "dot": false,
        "ymin": "0",
        "ymax": "100",
        "removeOlder": "1",
        "removeOlderPoints": "60",
        "removeOlderUnit": "3600",
        "cutout": 0,
        "useOneColor": false,
        "useUTC": false,
        "colors": [
            "#1f77b4",
            "#000000",
            "#000000",
            "#000000",
            "#000000",
            "#000000",
            "#000000",
            "#000000",
            "#000000"
        ],
        "outputs": 1,
        "useDifferentColor": false,
        "className": "",
        "x": 1050,
        "y": 160,
        "wires": [
            []
        ]
    },
    {
        "id": "fab750685abc4252",
        "type": "ui_gauge",
        "z": "357a76de90abc332",
        "name": "Temperatura",
        "group": "2f4e3f3b.d0b1c",
        "order": 2,
        "width": "4",
        "height": "4",
        "gtype": "gage",
        "title": "Temperatura",
        "label": "°C",
        "format": "{{value}}",
        "min": 0,
        "max": "50",
        "colors": [
            "#00bfff",
            "#ffae5c",
            "#ff6347"
        ],
        "seg1": "28",
        "seg2": "35",
        "diff": false,
        "className": "",
        "x": 1010,
        "y": 200,
        "wires": []
    },
    {
        "id": "6d2d05bf8a20b728",
        "type": "ui_gauge",
        "z": "357a76de90abc332",
        "name": "Umidade",
        "group": "2f4e3f3b.d0b1c",
        "order": 3,
        "width": "4",
        "height": "4",
        "gtype": "gage",
        "title": "Umidade",
        "label": "%",
        "format": "{{value}}",
        "min": 0,
        "max": "100",
        "colors": [
            "#4caf50",
            "#ffc107",
            "#2196f3"
        ],
        "seg1": "",
        "seg2": "",
        "diff": false,
        "className": "",
        "x": 1000,
        "y": 280,
        "wires": []
    },
    {
        "id": "404c74f7ac716470",
        "type": "function",
        "z": "357a76de90abc332",
        "name": "Define Status de Alerta",
        "func": "let nivel = msg.payload.nivelAgua;\nlet status = \"\";\nlet cor = \"\";\n\nif (nivel >= 85) {\n    status = \"PERIGO IMINENTE!\";\n    cor = \"red\";\n} else if (nivel >= 60) {\n    status = \"ALERTA - Nível Subindo\";\n    cor = \"orange\";\n} else {\n    status = \"NORMAL\";\n    cor = \"green\";\n}\n\n// Formata a mensagem para o nó de texto\nmsg.payload = `<font color='${cor}' size='5'><b>${status}</b></font>`;\n\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 770,
        "y": 360,
        "wires": [
            [
                "b4e21a09e413691d"
            ]
        ]
    },
    {
        "id": "b4e21a09e413691d",
        "type": "ui_text",
        "z": "357a76de90abc332",
        "group": "2f4e3f3b.d0b1c",
        "order": 4,
        "width": "12",
        "height": "2",
        "name": "Status do Alerta",
        "label": "STATUS ATUAL",
        "format": "{{msg.payload}}",
        "layout": "row-center",
        "className": "",
        "style": false,
        "font": "",
        "fontSize": "",
        "color": "#000000",
        "x": 1020,
        "y": 360,
        "wires": []
    },
    {
        "id": "3f87461189687424",
        "type": "debug",
        "z": "357a76de90abc332",
        "name": "debug 1",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "false",
        "statusVal": "",
        "statusType": "auto",
        "x": 520,
        "y": 80,
        "wires": []
    },
    {
        "id": "056ab3954d65464d",
        "type": "mqtt in",
        "z": "357a76de90abc332",
        "name": "",
        "topic": "smae/station/01/data",
        "qos": "2",
        "datatype": "auto-detect",
        "broker": "3f3855489843b886",
        "nl": false,
        "rap": true,
        "rh": 0,
        "inputs": 0,
        "x": 250,
        "y": 160,
        "wires": [
            [
                "01b6b0c72321aca5"
            ]
        ]
    },
    {
        "id": "2f4e3f3b.d0b1c",
        "type": "ui_group",
        "name": "Monitoramento em Tempo Real",
        "tab": "b3e3e4e.e4c1c18",
        "order": 1,
        "disp": true,
        "width": "12",
        "collapse": false
    },
    {
        "id": "3f3855489843b886",
        "type": "mqtt-broker",
        "name": "HiveMQ Público",
        "broker": "broker.hivemq.com",
        "port": 1883,
        "clientid": "",
        "autoConnect": true,
        "usetls": false,
        "protocolVersion": 4,
        "keepalive": 60,
        "cleansession": true,
        "autoUnsubscribe": true,
        "birthTopic": "",
        "birthQos": "0",
        "birthRetain": "false",
        "birthPayload": "",
        "birthMsg": {},
        "closeTopic": "",
        "closeQos": "0",
        "closeRetain": "false",
        "closePayload": "",
        "closeMsg": {},
        "willTopic": "",
        "willQos": "0",
        "willRetain": "false",
        "willPayload": "",
        "willMsg": {},
        "userProps": "",
        "sessionExpiry": ""
    },
    {
        "id": "b3e3e4e.e4c1c18",
        "type": "ui_tab",
        "name": "SMAE",
        "icon": "dashboard",
        "disabled": false,
        "hidden": false
    }
    ]
    ````

3.  **Faça o Deploy:** Após importar o fluxo, clique no botão vermelho "Deploy" para ativar as configurações. Verifique se o nó `mqtt in` (com o servidor `broker.hivemq.com` e tópico `smae/station/01/data`) se conecta com sucesso (indicado por um ponto verde abaixo do nó).

### Parte 3: Testando a Solução Completa

1.  Com a simulação do Wokwi rodando e o Node-RED com o fluxo implantado e conectado ao MQTT, acesse o seu dashboard do Node-RED (geralmente em `http://127.0.0.1:1880/ui`).
2.  Observe o painel sendo atualizado automaticamente com os dados dos sensores simulados no Wokwi.
3.  Interaja com os sensores no Wokwi (principalmente o sensor ultrassônico, arrastando o controle deslizante) e veja as mudanças refletidas em tempo real nos gráficos, medidores e no status de alerta do dashboard.

---

## 8. Grupo
| RM     | NOME                            |
|--------|---------------------------------|
| 556834 | Pablo Lopes Doria de Andrade    |
| 557047 | Vinicius Leopoldino de Oliveira |
| 558711 | Diego Santos Cardoso            | 
