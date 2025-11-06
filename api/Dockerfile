# /api/Dockerfile

# 1. Escolha uma imagem base leve do Python
# (Use a versão que você desenvolveu, ex: 3.10, 3.11, etc.)
FROM python:3.10-slim

RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

# 2. Defina o diretório de trabalho dentro do contêiner
# Todos os comandos seguintes rodarão a partir daqui
WORKDIR /app

# 3. Copie APENAS o arquivo de requisitos primeiro
# Isso é uma otimização de cache importante.
COPY requirements.txt .

# 4. Instale as dependências
# O Docker "lembrará" dessa camada. Se você só mudar seu código .py,
# ele não vai reinstalar tudo de novo, tornando o build muito mais rápido.
RUN pip install --no-cache-dir -r requirements.txt

# 5. Copie o RESTANTE do seu código da API
# (Copia tudo da pasta /api do host para /app no contêiner)
COPY . .

# 6. Defina o comando para rodar sua API
# (Exemplo se você usa Flask. Ajuste para o seu caso)
# O "0.0.0.0" é crucial para que a API seja acessível
# de fora do contêiner (pelo Docker Compose).
CMD ["python", "main.py"]
