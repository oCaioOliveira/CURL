# Tutorial cURL
### O que é?
- É um comando disponível na maioria dos sistemas baseado em Unix. Ele é usado como abreviação para “Client URL”. Comandos Curl são destinados para funcionar como uma forma de verificar a conectividade da URL, além de ser uma ótima ferramenta de transferência de dados.

### Quais protocolos ele suporta?
- HTTP e HTTPS;
- FTP e FTPS;
- IMAP e IMAPS;
- POP3 e POP3S;
- SMB e SMBS;
- SFTP;
- SCP;
- TELNET;
- GOPHER;
- LDAP e LDAPS;
- SMTP e SMTPS.

> _Estes são os protocolos mais importantes, porém existem outros também. Curl é empoderado por  libcurl, que é uma biblioteca de transferência URL_.

### Começando a trabalhar

- Antes de tudo é necessário fazer login na VPS
- Em seguida é necessário verifiicar a verção atual do Curl usando o seguinte comando:
> curl --version
>
> Obteremos o retorno da verção do curl com a lista de protocolos utilizados

### Comandos Curl - _Sintaxe Básica_

> _A sintaxe Básica do curl se assemelha com:_
>
> curl [options] [URL]

- O uso mais simples do Curl é para mostrar o conteudo de uma página:

> _exemplo com testdomain.com_
>
>_curl testdomain.com_

##### _observação : Isto renderizará o código-fonte completo da página inicial do domínio. Se nenhum protocolo foi especificado, o curl interpretará como HTTP._

### Opções de Comandos Curl de Arquivos

- Comandos curl podem fazer downloads de arquivos de um local remoto. Você pode fazer isto de duas formas:

>-O vai salvar o arquivo no diretório atual em funcionamento com  o mesmo nome do arquivo remoto.
>
>-o permite especificar um nome de diferente de arquivo ou local.
Abaixo, mostramos um exemplo disso:

>curl -O http://testdomain.com/testfile.tar.gz

- O comando acima vai salvar isto como testfile.tar.gz.

> curl -o newtestfile.tar.gz http://testdomain.com/testfile.tar.gz

- O comando acima vai salvar isto como newtestfile.tar.gz.

- Se por alguma razão, o download for interrompido, você pode reiniciá-lo usando curl. Você pode fazer isto com o seguinte comando:

> curl -C - -O  http://testdomain.com/testfile.tar.gz

- Usando curl, nós podemos fazer download de múltiplos arquivos, como mostramos abaixo:

> curl -O http://testdomain.com/testfile.tar.gz 
> -O http://mydomain.com/myfile.tar.gz

- Se você quer fazer o download de diversos arquivos de uma URL múltipla, liste todas elas em um arquivo. Comandos curl podem ser combinados com xargs para fazer o download de diferentes URL.

- Por exemplo, se tivermos um arquivo chamado allUrls.txt que contém uma lista de todas URLs para serem baixadas, então o exemplo abaixo pode ser usado para fazer download de todos os arquivos.

> xargs –n 1 curl -O < allUrls.txt

### Comandos curl para HTTP

- Curl também pode ser usado quando há um proxy server. Se você está atrás de um proxy server listado no portão 8090 de sampleproxy.com, por exemplo, faça download dos arquivos como mostra abaixo:
    > curl -x  sampleproxy.com:8090 -U username:password -O http:// testdomain.com/testfile.tar.gz 
    
- Uma solicitação típica de HTTP sempre vai ter um cabeçalho. O cabeçalho do HTTP envia as informações adicionais sobre o servidor remoto junto com a solicitação atual. Mesmo que através de uma ferramenta de navegador do desenvolvedor você possa verificar a informação, também pode fazê-lo usando uma url de comando.

Abaixo está um exemplo de como recuperar informações de um site.

> curl -I www.testdomain.com

#### Usando curl, você pode fazer um GET e um POST request. A GET request será como abaixo:

> curl http://mydomain.com

#### Um POST request será como mostramos aqui:

> curl –data “text=Hello” https://myDomain.com/firstPage.jsp

- No text=Hello está parâmetro de POST request. este comportamento será similar aos formulários HTML.

_Você também pode especificar métodos múltiplos de HTTP em um único comando curl. Faça isso usando a opção –next, como esta:_

- _curl –data “text=Hello” https://myDomain.com/firstPage.jsp --next https://myDomain.com/displayResult.jsp

## Aqui, há um exemplo de POST request seguido por um GET request.

- Toda solicitação HTTP terá um agente usuário que é enviado como parte da solicitação. Isto indica que os detalhes do navegador do cliente. Por padrão, uma solicitação curl contém o curl e detalhes do número da versão do agente usuário. A saída é como mostramos abaixo:

> “GET / HTTP/1.1” 200 “_” ”curl/7/29/0”

Você pode alterar esta informação de agente de usuário padrão usando o comando abaixo:

>curl -I http://mydomain.com –-user-agent “My new Browser”

Agora a saída alterada será:

> “GET / HTTP/1.1” 200 “_” ”My new Browser”_

### Limitando Saídas Curl
- Ao usar curl você não pode saber o tamanho das saídas. Você pode restringir a largura de banda para garantir que não será esmagado pelo curl.

- O comando abaixo restringe a largura de banda em 100K:

> curl --limit-rate 100K http://testdomain.com/samplefile.tar.gz -O

##  CURL Cookie

- Comandos Curl podem ser usados para verificar quais os cookies são baixados em qualquer  URL. Então, se você está acessando https://www.samplewebsite.com, então você pode imprimir um arquivo, salvar os cookies e acessá-lo usando cat ou editor VM.

Abaixo você vê um exemplo do comando:

>curl --cookie-jar Mycookies.txt https://www.samplewebsite.com /index.html -O

- Similar a isto, se você tiver cookies em um arquivo, então você pode enviá-lo para o site. Veja o exemplo abaixo:

>curl --cookie Mycookies.txt https://www. samplewebsite.com
## Resumo 

- Curl é um comando inteligente e poderoso. É muito útil quando você depende de linhas de comando. Ele tem diversas opções e suporta protocolos múltiplos. Esta é uma ótima razão para aprender este comando.

- Lembre-se, se você quer aprender comandos avançados, simplesmente consulte o manual que deve estar presente em todas as versões Unix.

> man curl

Espero que este tutorial seja um bom começo para você usar o Curl.

# Procedimentos Importantes do Curl
### Fazendo o download de arquivos 

- Vamos utilizar aqui a mídia de instalação da ultima versão do Ubuntu como exemplo. Para fazer o download de um arquivo, salvando com o mesmo nome do arquivo definido pelo servidor, basta usar a opção -O.


> curl -O https://releases.ubuntu.com/20.04.1/ubuntu-20.04.1-desktop-amd64.iso

-  O download será iniciado e as informações sobre ele serão exibidas:

| % Total | % Received | % Xferd | Average Dload | Speed Upload | Time total| Time Spent | Time Left | Current Speed |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 3 2656M | 3 83.3M  | 0 | 0 | 6638k | 0 | 0:06:49  | 0:00:12 | 9014k |

- Para escolher o nome do arquivo que será salvo, basta adicionar o nome desejado no final do comando:

>curl -O https://releases.ubuntu.com/20.04.1/ubuntu-20.04.1-desktop-amd64.iso ubuntu20.iso

- Também é possivel esconder informações do progresso do download usando a opção -s: 

> curl -s -O https://releases.ubuntu.com/20.04.1/ubuntu-20.04.1-desktop-amd64.iso ubuntu20.iso

- Ou também podemos definir uma barra de progresso simples ao invés da informação completa utilizando o -#:

> curl -# -O https://releases.ubuntu.com/20.04.1/ubuntu-20.04.1-desktop-amd64.iso ubuntu20.iso
>
> Nesse caso o pregresso do downloado será demonstrado com uma sequência de #:
>
> #######                    5,4%

- Caso o download seja interrompido é possivel utilizar a opção -C para dar continuidade:

> curl -C - -O https://releases.ubuntu.com/20.04.1/ubuntu-20.04.1-desktop-amd64.iso
>
> O hífen (-) após o 'C' indica ao curl que ele deve descobrir automaticamente onde e como continuar o download.

### Interagindo com API's REST com GET e POST

- Por padrão o curl usa o método HTTP GET para realizar as requisições. Para realizar uma requisição GET executamos o seguinte comando:

> curl https://jsonplaceholder.typicode.com/posts
> 
> http ilustrativo 

- O retorno será um JSON contendo uma lista de Posts:

>[
>
  >{
    
    "userId": 1,
    
    "id": 1,
    
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
> },
>
>{

    "userId": 1,

    "id": 2,

    "title": "qui est esse",

    "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
  >},
  >
  >{

    "userId": 1,
    "id": 3,
    "title": "ea molestias quasi exercitationem repellat qui ipsa sit aut",
    "body": "et iusto sed quo iure\nvoluptatem occaecati omnis eligendi aut ad\nvoluptatem doloribus vel accusantium quis pariatur\nmolestiae porro eius odio et labore et velit aut"
  >},
  >
  >[continua ...]

- Também é possivel especificar qual método usar, passando a opção -X e o método como argumento:

> curl -X GET https://jsonplaceholder.typicode.com/posts

- Para realizar a criação de um POST executamos o seguinte comando:

> curl -i -X POST https://jsonplaceholder.typicode.com/comments \
>     -H 'Content-Type: application/json' \
>     -d $'{
>            "postId": 101,  
>            "name": "Fulano da Silva",  
>            "email": "fulano@gmail.com",  
>            "body": "De acordo ao manual do curl ( disponível online [...]"
>          }' 

- Resultando em:

>HTTP/2 201
>date: Tue, 05 Jan 2021 01:17:53 GMT  
>content-type: application/json; charset=utf-8  
>content-length: 168  
>set-cookie: __cfduid=d4f15935c351e1b9ece6e8d8cdb1ffa1a1609809470; expires=Thu, 04-Feb-21 01:17:50 GMT; path=/; domain=.typicode.com; HttpOnly; SameSite=Lax  
>x-powered-by: Express
[continua ...]

>{  

    "postId": 101,
    "name": "Fulando da Silva",
    "email": "fulano@gmail.com",
    "body": "De acordo ao manual do curl ( disponível online [...]",
    "id": 501
>}

- A opção -H permite adicionar um cabeçalho e a -d permite passar os dados da requisição. Nesse caso, definimos que o conteúdo é no formato JSON e passamos o conteúdo da requisição que será usado para criar uma conta. Podemos ver no resultado que o status foi 201, indicando que um novo recurso foi criado.



