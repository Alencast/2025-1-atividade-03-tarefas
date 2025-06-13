# Define a imagem base (Fedora)
FROM fedora:latest

# Atualiza os pacotes e instala:
# - GCC (compilador C)
# - Fish Shell (para terminal interativo)
# - Bibliotecas essenciais (glibc-devel para pthread)
RUN dnf -y update && \
    dnf -y install gcc fish findutils glibc-devel && \
    dnf clean all

# Cria um diretório para a aplicação
RUN mkdir -p /app

# Copia os arquivos .c para o container
COPY fork.c thread.c /app/

# Define o diretório de trabalho padrão
WORKDIR /app

# Compila os programas C
RUN gcc fork.c -o fork_program && \
    gcc thread.c -o thread_program -pthread

# Permissão de execução (opcional)
RUN chmod +x /app/fork_program /app/thread_program

# Comando padrão: inicia o Fish Shell (interativo)
CMD ["fish"]