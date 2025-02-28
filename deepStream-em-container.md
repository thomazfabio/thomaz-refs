A NVIDIA fornece o **DeepStream** em forma de **container Docker**, o que facilita a instalação e configuração.  

Se você quiser rodar o **DeepStream** sem instalar diretamente no sistema, pode usar o container oficial da NVIDIA, que já vem com as dependências prontas.  

### 🚀 **Passos para rodar DeepStream via Docker**  

1️⃣ **Instale o NVIDIA Container Toolkit** (se ainda não tiver)  
```bash
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt update
sudo apt install -y nvidia-docker2
sudo systemctl restart docker
```

2️⃣ **Baixe e rode o container do DeepStream**  
```bash
docker run --gpus all -it --rm nvcr.io/nvidia/deepstream:6.3-triton bash
```
📌 Isso vai abrir um **shell dentro do container**, pronto para usar o DeepStream.  

### 🔥 **Explicação dos parâmetros:**  
- `--gpus all` → Permite que o container acesse todas as GPUs.  
- `-it` → Mantém o terminal interativo.  
- `--rm` → Remove o container ao sair (se não quiser isso, remova essa flag).  
- `nvcr.io/nvidia/deepstream:6.3-triton` → Imagem oficial do DeepStream (versão 6.3 com Triton Inference Server).  

💡 **Dica:** Se quiser rodar aplicações gráficas dentro do container (ex: visualizar vídeo), adicione `--runtime=nvidia -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix`.  

Se precisar de uma versão diferente, veja todas as imagens disponíveis aqui:  
🔗 [https://catalog.ngc.nvidia.com/orgs/nvidia/containers/deepstream](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/deepstream)  

Quer testar primeiro e depois instalar direto no sistema ou pretende rodar sempre via Docker? 🚀