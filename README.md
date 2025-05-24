# S.O. 2025.1 - Atividade 03 - Compilação de código dentro de docker fedora

## Informações gerais

- **Objetivo do repositório**: Repositório para atividade avaliativa dos alunos
- **Assunto**: Implementação de tarefas (processos)
- **Público alvo**: alunos da disciplina de SO (Sistemas Operacionais) do curso de TADS (Superior em Tecnologia em Análise e Desenvolvimento de Sistemas) no CNAT-IFRN (Instituto Federal de Educação, Ciência e Tecnologia do Rio Grande do Norte - Campus Natal-Central).
- disciplina: **SO** [Sistemas Operacionais](https://github.com/sistemas-operacionais/)
- professor: [Leonardo A. Minora](https://github.com/leonardo-minora)
- aluno: Robson Alves(https://github.com/Alencast)

## Sumário

1. Tutorial introdutório de Dockerfile
2. Prática

---

## Parte 1. Tutotirla introdutório de Dockerfile

**Tutorial Introdutório a Dockerfile** by [deepseek](https://chat.deepseek.com/).

Neste tutorial, você aprenderá os conceitos básicos de **Dockerfile**, como criar uma imagem personalizada e executar um container com mapeamento de volumes.  

---

### 1.1. O que é um Dockerfile?
Um **Dockerfile** é um arquivo de texto que contém instruções para construir uma imagem Docker. Essas instruções definem:  
- A **imagem base** (ex: `fedora`, `ubuntu`, `python`).  
- **Comandos** a serem executados (instalação de pacotes, configurações).  
- **Diretórios de trabalho** e **variáveis de ambiente**.  
- **Mapeamento de portas** e **volumes**.  

---

### 1.2. Criando Nosso Primeiro Dockerfile

#### 1.2.1. Crie um arquivo `Dockerfile`
Abra um editor de texto (VS Code, Notepad++, etc.) e cole o seguinte conteúdo:  

```dockerfile
# Define a imagem base (Fedora)
FROM fedora:latest

# Atualiza os pacotes e instala utilitários básicos
RUN dnf -y update && \
    dnf -y install findutils && \
    dnf -y install fish && \
    dnf clean all

# Cria um diretório para a aplicação
RUN mkdir -p /app

# Define o diretório de trabalho padrão
WORKDIR /app

# Comando padrão ao iniciar o container
CMD ["fish"]
```

#### 1.2.2: Entendendo as Instruções
- **`FROM`**: Define a imagem base (aqui, usamos Fedora).  
- **`RUN`**: Executa comandos dentro do container (atualizar pacotes, instalar programas).  
- **`WORKDIR`**: Define o diretório padrão onde comandos serão executados.  
- **`CMD`**: Define o comando padrão ao iniciar o container (`bash` abre um terminal interativo).  

---

### 1.3. Construindo a Imagem Docker

No terminal (PowerShell ou CMD), navegue até a pasta onde está o `Dockerfile` e execute:  

```bash
docker build -t minha-imagem-fedora .
```
- **`-t minha-imagem-fedora`**: Define um nome para a imagem.  
- **`.`**: Indica que o Dockerfile está no diretório atual.  

---

### 1.4. Executando o Container com Mapeamento de Volume

Para mapear uma pasta do Windows para dentro do container, use:  

#### 1.4.1. No PowerShell
```bash
docker run -it --rm -v ${PWD}:/app minha-imagem-fedora
```

#### 1.4.2. No CMD (Prompt de Comando)
```bash
docker run -it --rm -v %cd%:/app minha-imagem-fedora
```

#### 1.4.3. Explicação do Comando
- **`-it`**: Modo interativo (permite digitar comandos no terminal do container).  
- **`--rm`**: Remove o container automaticamente após sair.  
- **`-v ${PWD}:/app`**: Mapeia o diretório atual do Windows (`${PWD}` ou `%cd%`) para `/app` no container.  

---

### 1.5. Verificando o Funcionamento

Dentro do container, execute:  
```bash
ls
```
Você verá os arquivos do seu diretório Windows mapeados em `/app`.  

Para sair do container, digite:
```bash
exit
```

---

### 1.6. Próximos Passos
Agora que você já sabe criar um Dockerfile básico, pode:  
✅ **Instalar outras dependências** (ex: `RUN dnf install gcc`)  
✅ **Expor portas** (ex: `EXPOSE 80`) para aplicações web  
✅ **Copiar arquivos** (ex: `COPY . /app`)  
✅ **Definir variáveis de ambiente** (ex: `ENV VAR=valor`)  

---

### 1.7. Conclusão
Você aprendeu:  
✔ Como criar um **Dockerfile**  
✔ Como **construir uma imagem** Docker  
✔ Como **mapear pastas** do Windows para o container  
✔ Como **executar e interagir** com o container  



### 🔗 1.8. Recursos Úteis
- [Documentação Oficial do Dockerfile](https://docs.docker.com/engine/reference/builder/)  
- [Tutoriais Docker para Iniciantes](https://docker-curriculum.com)  


---


## Parte 2. Prática

### 2.1. Introdução
Nesta prática, você aprenderá a usar um **Dockerfile** para criar um ambiente isolado capaz de **compilar e executar código em C**. O objetivo é:  
- Criar uma imagem Docker com as ferramentas necessárias (`gcc`).  
- Mapear um diretório do host (Windows/Linux) para o container.  
- Compilar e executar um programa em C diretamente no container.  

**Pré-requisitos:**  
✔ Docker instalado ([Download Docker Desktop](https://www.docker.com/products/docker-desktop))  
✔ Editor de texto (VS Code, Sublime, etc.)  
✔ Conhecimento básico de C  

---

### 2.2. Desenvolvimento das Atividades

#### 2.2.1. Fork e indentificação do aluno

1. Fork desse repositório para seu pessoal (de estudo).
2. Modifique o README procurando por FIXME na linha 10 por seu nome (coloque link para sua conta github).
3. Realize as atividades abaixo.

#### 2.2.2. Preparando o Ambiente
1. Crie uma pasta no seu sistema (ex: `docker-c-practice`).  
2. Dentro dela, crie dois arquivos:  
   - `Dockerfile` (instruções para a imagem Docker).  
   - copie corretamente os códigos-fonte do [capítulo de implementação de tarefa do livro texto da disciplina](https://wiki.inf.ufpr.br/maziero/lib/exe/fetch.php?media=socm:socm-05.pdf)

#### 2.2.3. Conteúdo do `Dockerfile`

Veja tutorial acima e crie seu Dockerfile no mesmo diretório dos códigos-fonte


#### 2.2.4. Construindo a Imagem Docker

Veja tutorial acima e construa a sua imagem docker.

#### 2.2.5. Executando o Container

Veja tutorial acima e execute o tutorial.

Lembre:
1. instalar o `gcc`.
2. você esta no terminal `fish`, ele tentará te ajudar.
3. você esta no diretório `app` do conteiner que é uma referência para o diretório que está o Dockerfile e os códigos-fonte em c do Windows.

Para **compilar e executar** seus códigos-fontes.  
```bash

```

---

### 2.3. Relatório da Prática (Template para Entregar)

**Lembre** que o relatório:
- deve estar no mesmo repositório, 
- deve ser em markdown, 
- deve conter imagens da tela capturada,
- apesar da atividade ser coletiva, relatório deve ser individual.

**Nome:** Robson Alves de Alencastro
**Data:** 24/05/2025 

### 1. Objetivo
O objetivo principal da atividade foi utilizar um Dockerfile para criar um ambiente isolado e configurado com as ferramentas necessárias para compilar e executar os programas em C desenvolvidos na aula anterior. O Dockerfile foi configurado com uma imagem base do Fedora e o shell Fish, sendo necessário instalar manualmente o compilador GCC e suas dependências para garantir o funcionamento correto dos códigos. Com o ambiente pronto, foi possível testar os conceitos de S.O em C:

* Criação de processos filhos com fork()

* Substituição de programas em execução com execve()

* Sincronização entre processos pai e filho usando wait()

* Execução concorrente com múltiplas threads (pthread)

* Esses experimentos permitiram observar na prática como um sistema operacional gerencia processos e threads, além de reforçar a importância do Docker na padronização de ambientes de desenvolvimento.

### 2. Passos Executados  
####  Comando 1  : Construção da Imagem Docker
Comando: docker build -t minha-imagem-fedora .
Esse comando cria uma imagem Docker a partir do Dockerfile no diretório atual.
![image](https://github.com/user-attachments/assets/a3fd625e-2902-487a-ba05-00318a9f28c1)


Função:

Constrói uma nova imagem Docker a partir do Dockerfile presente no diretório atual.

A flag -t define o nome da imagem como minha-imagem-fedora.

O . no final indica que o contexto de construção é o diretório atual (onde estão o Dockerfile, fork.c e thread.c).

####  Comando 2: docker run -it --rm -v ${PWD}:/app minha-imagem-fedora
Esse comando executa um contêiner Docker com um volume compartilhado entre o contêiner e o host, removendo o contêiner após a conclusão.

![image](https://github.com/user-attachments/assets/b0c737c2-9f2b-483c-bb6c-86bb12c2fffa)

#### Comando 3: ls -l
O comando é utilizado para visualizar as informações sobre os arquivos e diretórios disponíveis.

![image](https://github.com/user-attachments/assets/7ce02ea6-3395-4291-b61f-aebeba7e1ad3)

#### Comando 4: dnf update -y
Esse comando atualiza todos os pacotes instalados no sistema para as versões mais recentes disponíveis nos repositórios. A opção -y confirma automaticamente todas as solicitações, permitindo que o processo ocorra sem interrupções.

![image](https://github.com/user-attachments/assets/f249e667-760c-4155-9b12-b3e0d32340bd)

O que acontece durante o build:

1.O Docker lê as instruções do Dockerfile.

2.Instala as dependências (gcc, glibc-devel, etc.) na imagem base do Fedora.

3.Copia os arquivos fork.c e thread.c para o diretório /app no container.

4.Compila os programas, gerando os executáveis fork_program e thread_program.


## 3. Resultados Obtidos
#### Primeiro Programa: fork.c
![image](https://github.com/user-attachments/assets/79b6e3a4-b6db-4297-8534-22fe896fc2d2)

O código em questão utiliza a função fork() para criar um processo filho. O processo pai aguarda a finalização do filho antes de continuar sua execução, utilizando a função wait().

Após ser criado, o processo filho executa o comando /bin/date por meio da função execve(), o que substitui o código do processo filho pela execução do comando, exibindo a data e hora atual.

Após a chamada de execve(), o processo filho imprime a data e, em seguida, tanto o pai quanto o filho exibem a mensagem "Tchau !".

Problemas enfrentados e soluções:
A saída esperada seria:

yaml
Copiar
Editar
Fri May Data/Hora
Tchau !
Tchau !
No entanto, foi exibido apenas um:

yaml
Copiar
Editar
Fri May Data/Hora
Tchau !
Isso ocorreu porque o processo filho foi substituído pelo comando date após a execução da função execve(), e, com isso, não executou o printf("Tchau !") que vinha depois. A função execve() não retorna em caso de sucesso, pois o processo atual é completamente substituído pela nova execução.

Como resultado, apenas o processo pai executou o printf("Tchau !").

✅ Solução:
Para que ambos os processos (pai e filho) imprimam "Tchau !", o printf("Tchau !") no processo filho deve ser colocado antes da chamada ao execve(). Assim, a mensagem será exibida antes que o processo seja substituído pelo comando date.

#### Segundo programa: Thread.c

![image](https://github.com/user-attachments/assets/75bd0dfd-fade-4dcc-9a80-01f3423646b7)


O código cria cinco threads, e cada uma delas executa a mesma rotina: imprime "Hello World!", aguarda 5 segundos e, em seguida, imprime "Bye bye World!". Como as threads são executadas de forma concorrente, a ordem das mensagens pode variar a cada execução, mas todas seguem esse mesmo padrão de comportamento.


### 4. Conclusão  
Os códigos mostraram na prática conceitos importantes de concorrência e paralelismo. Com fork() e execve(), foi possível criar processos que rodam de forma paralela, cada um com sua própria execução. Já com pthread_create(), conseguimos criar várias threads que funcionam dentro do mesmo processo, executando tarefas ao mesmo tempo. Também usamos wait() e pthread_exit() para garantir que tudo aconteça na ordem certa, sem conflitos.

Tudo foi rodado em um ambiente isolado criado com Docker, o que garantiu que os testes fossem consistentes e fáceis de repetir. O uso do Docker ajudou bastante, pois cria um ambiente limpo e controlado, ideal para desenvolvimento e testes.

Esses conceitos são muito úteis em sistemas que precisam lidar com várias tarefas ao mesmo tempo, como servidores web, jogos, sistemas de monitoramento ou aplicações que processam muitos dados. O uso de fork() e execve() pode ser ideal quando se quer processos separados para lidar com diferentes requisições. Já as threads funcionam melhor quando precisamos de mais leveza e rapidez, como em aplicações em tempo real.

Aprender e aplicar essas ideias é um passo importante para quem quer desenvolver sistemas mais eficientes e preparados para grandes cargas.
