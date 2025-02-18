Podemos usar o **FFmpeg** e o **GStreamer** para criar um servidor RTSP que transmite múltiplos vídeos como canais separados. A biblioteca **rtsp-simple-server (mediamtx)** é uma excelente opção para esse tipo de tarefa.  

---

## 🔹 **Solução com `rtsp-simple-server` (MediaMTX) + FFmpeg**
Esse método permite criar múltiplos streams RTSP usando a **mesma porta (554)**, diferenciando os vídeos por canais (ex: `rtsp://localhost:554/canal1`, `rtsp://localhost:554/canal2`, etc.).  

### 📌 **Passo 1: Instalar Dependências**
```bash
sudo apt update
sudo apt install ffmpeg
```
Agora, baixe o **MediaMTX** (antigo `rtsp-simple-server`):  
```bash
wget https://github.com/bluenviron/mediamtx/releases/latest/download/mediamtx_linux_amd64.tar.gz
tar -xvzf mediamtx_linux_amd64.tar.gz
chmod +x mediamtx
```

---

### 📌 **Passo 2: Criar a Pasta com os Vídeos**
Crie uma pasta e coloque seus vídeos dentro:  
```bash
mkdir ~/videos
mv meus_videos/*.mp4 ~/videos/
```

---

### 📌 **Passo 3: Criar um Script Python para Servir os Vídeos**
Crie um arquivo `stream_videos.py` e adicione o seguinte código:  

```python
import os
import subprocess
import time

# Configurações
RTSP_SERVER = "rtsp://localhost:554"
VIDEO_FOLDER = "/home/seu_usuario/videos"  # Atualize para sua pasta real
CANAL_PREFIX = "canal"  # Nome base para os streams

# Lista todos os vídeos na pasta
videos = [f for f in os.listdir(VIDEO_FOLDER) if f.endswith((".mp4", ".avi", ".mkv"))]

processes = []

for idx, video in enumerate(videos, start=1):
    video_path = os.path.join(VIDEO_FOLDER, video)
    rtsp_url = f"{RTSP_SERVER}/{CANAL_PREFIX}{idx}"  # Exemplo: rtsp://localhost:554/canal1

    print(f"Iniciando stream: {video_path} → {rtsp_url}")

    # Comando para transmitir o vídeo como RTSP
    command = [
        "ffmpeg",
        "-re",
        "-stream_loop", "-1",  # Loop infinito
        "-i", video_path,      # Arquivo de entrada
        "-c:v", "libx264",     # Codec de vídeo
        "-preset", "ultrafast",
        "-tune", "zerolatency",
        "-c:a", "aac",         # Codec de áudio
        "-f", "rtsp",
        rtsp_url
    ]

    # Iniciar processo
    proc = subprocess.Popen(command)
    processes.append(proc)
    time.sleep(2)  # Pequeno delay para evitar sobrecarga

try:
    while True:
        time.sleep(1)
except KeyboardInterrupt:
    print("\nEncerrando streams...")
    for proc in processes:
        proc.terminate()
    print("Todos os streams foram encerrados.")
```

---

### 📌 **Passo 4: Iniciar o Servidor RTSP**
Abra um terminal e execute:  
```bash
./mediamtx
```

Depois, abra um **segundo terminal** e execute o script Python:
```bash
python3 stream_videos.py
```

Isso iniciará os streams dos vídeos na mesma porta `554`, diferenciando apenas pelos canais.  

**Exemplos de URLs RTSP:**  
- `rtsp://localhost:554/canal1`  
- `rtsp://localhost:554/canal2`  
- `rtsp://localhost:554/canal3`  

Você pode testar no **VLC** indo em **Mídia → Abrir fluxo de rede** e inserindo uma das URLs.  

---

## 🎯 **Vantagens dessa Solução**
✅ Usa **FFmpeg**, que é altamente otimizado.  
✅ **Mesmo servidor RTSP** para múltiplos canais.  
✅ Cada vídeo fica em **loop infinito** automaticamente.  
✅ **Suporte a múltiplos formatos** de vídeo.  
✅ Código modular e fácil de expandir.  

Essa solução é altamente eficiente para testes e desenvolvimento! 🚀🔥