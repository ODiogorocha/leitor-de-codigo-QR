# MobileNet SSD e Leitura de QR Code

Este projeto utiliza a biblioteca OpenCV e a MobileNet SSD para detectar objetos e ler códigos QR em tempo real a partir da câmera. O código é capaz de identificar diferentes classes de objetos, como carros, pessoas e bicicletas, e também processar e exibir informações de códigos QR encontrados na imagem.

## Funcionalidades

- **Detecção de Objetos**: Utiliza o modelo pré-treinado MobileNet SSD para detectar objetos em tempo real. As classes de objetos detectadas incluem "pessoa", "carro", "bicicleta", entre outras.
- **Leitura de QR Code**: Lê e decodifica códigos QR presentes no vídeo, desenhando contornos ao redor dos mesmos e exibindo as informações contidas.

## Requisitos

Para executar este projeto, você precisará das seguintes bibliotecas:

- `opencv-python`
- `numpy`
- `pyzbar`

Você pode instalá-las usando o comando:

```bash
pip install opencv-python numpy pyzbar
```

Além disso, é necessário ter os seguintes arquivos de modelo para a rede neural:

- `deploy.prototxt`: Definição da arquitetura da rede.
- `mobilenet_iter_73000.caffemodel`: Pesos treinados para o modelo.

Esses arquivos podem ser encontrados no [link de referência](https://insper.github.io/robotica-computacional/modulos/06-visao-p3/atividades/1-mobilenet/).

## Como Executar

1. **Clone o repositório** e navegue até o diretório do projeto:

```bash
git clone <URL_DO_REPOSITORIO>
cd <NOME_DO_DIRETORIO>
```

2. **Coloque os arquivos de modelo** (`deploy.prototxt` e `mobilenet_iter_73000.caffemodel`) no diretório principal do projeto.

3. **Execute o script**:

```bash
python main.py
```

O script abrirá a câmera e começará a detectar objetos e códigos QR em tempo real. As detecções e informações dos QR Codes serão salvas no arquivo `detecoes_e_codigos_qr.txt`.

## Estrutura do Código

### Importações

O código importa as bibliotecas necessárias para manipulação de imagens e leitura de QR Codes:

```python
import cv2
import numpy as np
from pyzbar.pyzbar import decode
```

### Carregamento da Rede Neural

O modelo MobileNet SSD é carregado utilizando a função `cv2.dnn.readNetFromCaffe`:

```python
net = cv2.dnn.readNetFromCaffe(prototxt, model)
```

### Definição das Classes

As classes de objetos que o modelo pode detectar são definidas em uma lista:

```python
CLASSES = [
    "background", "aeroplane", "bicycle", "bird", "boat",
    "bottle", "bus", "car", "cat", "chair", "cow", "diningtable",
    "dog", "horse", "motorbike", "person", "pottedplant",
    "sheep", "sofa", "train", "tvmonitor"
]
```

### Funções Principais

1. **`processa_qr_code(frame, output_file)`**: Detecta e desenha contornos em torno de códigos QR na imagem, e salva as informações decodificadas em um arquivo de texto.

2. **`processar_camera_e_gravar(arquivo_de_saida)`**: Captura o vídeo da câmera, processa cada frame para detectar objetos e códigos QR, e grava as detecções no arquivo de saída.

### Execução

A função `processar_camera_e_gravar` é chamada com o nome do arquivo de saída:

```python
arquivo_de_saida = 'detecoes_e_codigos_qr.txt'
processar_camera_e_gravar(arquivo_de_saida)
```

