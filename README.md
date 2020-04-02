# Jekyll Github Pages Docker

O intuito desse projeto é fornecer um ambiente de execução local, baseado em docker, para quem precisa trabalhar com GH Pages e Jekyll.

Para a execução desse projeto, é necessário que você tenha o Docker instalado. O kitematic ou outro
gerenciador podem vir a ser úteis.

## Preparação

### Construção da imagem

O primeiro passo é a construção da imagem. Esse passo deve ser executado antes de executar a imagem ou após qualquer mudança que você venha a fazer nela.

Para construir a imagem do contêiner, abra o terminal, na pasta do projeto, e execute o comando.

```shell
docker build -t [NOME_DO_PROJETO] .
```

Exemplo:

```shell
docker build -t nomedocapeta .
```

### Preparação da pasta

Após construir a imagem, dentro da pasta do projeto, crie a pasta `vendor/bundle`.

### Primeira execução do contêiner

Para executar o contêiner, o seguinte comando deve ser usado:

```shell
docker run --rm -it -v "/d/repositorios/[NOME_DO_PROJETO]:/srv/jekyll" -v "/d/repositorios/[NOME_DO_PROJETO]/vendor/bundle:/usr/local/bundle" -p 4000:4000 -p 35729:35729 --name [NOME_DO_PROJETO] [NOME_DO_PROJETO] bash
```

### Criação do site

Ao executar o contêiner, o terminal mostrará o *bash* aguardando os comandos. Então, use o comando `jekyll new` para criar o site. Você já estará na pasta do projeto, portanto, não deve mudar de pasta.

```shell
jekyll new --force .
```

O parâmetro `--force` é necessário, pois a pasta do projeto já contem arquivos.

### Pra executar o servidor de desenvolvimento

Para executar o servidor de testes do jekyll, use o comando `jekyll serve`:

```shell
jekyll serve --watch --force-polling --livereload
```

Após a execução do `jekyll serve`, verifique, no Kitematic, qual a o IP para acessar o container ou execute, no terminal do host, o comando `docker-machine ip`. O endereço para acesso é [http://IP_DO_DOCKER_MACHINE/[NOME_DO_PROJETO]]([http://IP_DO_DOCKER_MACHINE/[NOME_DO_PROJETO]])

Sempre que alterar algum dos arquivos de configuração do Jekyll, mate o servidor jekyll, com o comando `ctrl + c`, no terminal, e execute novamente o comando `jekyll serve`.

### Conectando num container que está rodando

Normalmente, continuamos conectardos ao contêiner, para reuniciar o `jekyll serve`, caso seja necessário mexer no arquivo de configuração.

Entretando, se essa conexão for rompida e o contêiner continuar ativo, execute o `docker exec` para reconectar.

```shell
docker exec -it [NOME_DO_PROJETO] bash
```
