# Video Heatmap Analyzer

A Python desktop app that analyzes **screen recordings** and generates a heatmap of where the mouse cursor went, useful for reviewing usability test sessions and seeing which areas of an interface got the most attention.

[🇧🇷 Leia em português](#-português)

## How it works

1. You open a video in the PyQt5 interface.
2. The app reads it frame by frame with OpenCV and finds the cursor by comparing consecutive frames: it blurs both frames slightly, takes their difference, thresholds it and keeps only small, roughly circular, square-ish blobs that look like a cursor.
3. Each detected position is stored with its timestamp.
4. For the time range you choose, the positions are accumulated into a heatmap (with a decay factor), smoothed with a Gaussian blur and drawn over the video frame with the selected color map.

## Features

- Media panel with the current file and a video preview.
- Adjustable detection: **sensitivity** (difference threshold) and **min/max size** of the cursor blob.
- Adjustable output: heatmap **resolution**, **smoothing** (blur size) and color map.
- Heatmap for a chosen time interval, overlaid on the corresponding frame, with an option to save it.
- Tries to raise the process priority while processing (`psutil` on Windows, `os.nice` on Linux).

## Requirements

Python 3 with `opencv-python`, `numpy`, `matplotlib`, `PyQt5` and, optionally, `psutil` (listed in `requirement.txt`).

## Getting started

```bash
git clone https://github.com/UxUchoa/Video-Heatmap-Python.git
cd Video-Heatmap-Python
python -m venv venv
.\venv\Scripts\activate          # macOS/Linux: source venv/bin/activate
pip install -r requirement.txt
python main.py
```

If `psutil` gives you trouble, remove it from `requirement.txt`: it's only used for the priority boost.

## Project structure

```text
main.py            entry point
src/processor.py   VideoHeatmapProcessor: cursor detection, heatmap generation and overlay
src/ui.py          PyQt5 interface ("Video Heatmap Analyzer Professional")
heatmap/           default output folder
executavel/        packaged Windows build
```

`VideoHeatmapProcessor` defaults: `decay_factor=0.95` and `blur_size=15` (always rounded to an odd number).

---

## 🇧🇷 Português

# Video Heatmap Analyzer

Aplicativo desktop em Python que analisa **gravações de tela** e gera um mapa de calor de por onde o cursor do mouse passou. Serve para revisar sessões de teste de usabilidade e ver quais áreas da interface receberam mais atenção.

### Como funciona

1. Você abre um vídeo na interface em PyQt5.
2. O app lê o vídeo quadro a quadro com OpenCV e encontra o cursor comparando quadros consecutivos: aplica um leve desfoque nos dois, calcula a diferença, aplica um limiar e mantém só manchas pequenas, quase circulares e com proporção perto de 1:1, que parecem um cursor.
3. Cada posição detectada é guardada com o momento do vídeo.
4. No intervalo de tempo escolhido, as posições são acumuladas num mapa de calor (com fator de decaimento), suavizadas com desfoque gaussiano e desenhadas sobre o quadro do vídeo com o mapa de cores escolhido.

### Recursos

- Painel de mídia com o arquivo atual e a prévia do vídeo.
- Detecção ajustável: **sensibilidade** (limiar da diferença) e **tamanho mínimo e máximo** da mancha do cursor.
- Saída ajustável: **resolução** do mapa, **suavização** (tamanho do desfoque) e mapa de cores.
- Mapa de calor de um intervalo de tempo escolhido, sobreposto ao quadro correspondente, com opção de salvar.
- Tenta aumentar a prioridade do processo durante o processamento (`psutil` no Windows, `os.nice` no Linux).

### Requisitos

Python 3 com `opencv-python`, `numpy`, `matplotlib`, `PyQt5` e, opcionalmente, `psutil` (todos em `requirement.txt`).

### Como rodar

```bash
git clone https://github.com/UxUchoa/Video-Heatmap-Python.git
cd Video-Heatmap-Python
python -m venv venv
.\venv\Scripts\activate          # macOS/Linux: source venv/bin/activate
pip install -r requirement.txt
python main.py
```

Se o `psutil` der problema, tire ele do `requirement.txt`: ele só é usado para aumentar a prioridade.

### Estrutura

`main.py` é o ponto de entrada, `src/processor.py` tem o `VideoHeatmapProcessor` (detecção do cursor, geração e sobreposição do mapa), `src/ui.py` tem a interface em PyQt5, `heatmap/` é a pasta de saída padrão e `executavel/` guarda a versão empacotada para Windows. Os padrões do processador são `decay_factor=0.95` e `blur_size=15` (sempre arredondado para ímpar).
