# AI-Schema: System Architecture

## Общая схема системы

```mermaid
graph LR
    subgraph FRONT["📱 FRONT"]
        EMU["⏱️ EMULATOR"]
        TA["👤 Terminal A"]
        TB["👤 Terminal B"]
    end

    subgraph BACK["⚙️ BACK"]
        GM["🗄️ GRAPH MODEL"]
        SR["📁 SCRIPT REPO"]
        PL["📚 PROJECT LIB"]
        ASR["🎙️ ASR"]
        AI["⚙️ AI Agent"]
        LP["🛡️ LLM PROXY"]
        MQ[" MQTT MOSQUITTO"]
    end

    subgraph CLOUD["☁️ CLOUD"]
        GC["➕ GigaChat"]
        QW["🆀 Qwen"]
        LM["🧠 LLM"]
    end

    BUS["══════ 🚌 MQTT BUS ══════"]

    %% Физические подключения
    EMU <--> BUS
    TA <--> BUS
    TB <--> BUS
    ASR <--> BUS
    AI <--> BUS
    LP <--> BUS
    MQ <--> BUS

    %% Логические связи
    AI <--> GM
    AI <--> SR
    AI <--> PL
    ASR <--> AI
    AI <--> LP

    %% Облако
    GC -->|HTTPS| LP
    QW -->|HTTPS| LP
    LM -->|HTTPS| LP

