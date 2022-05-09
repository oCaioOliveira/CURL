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

## Resumo 

- Curl é um comando inteligente e poderoso. É muito útil quando você depende de linhas de comando. Ele tem diversas opções e suporta protocolos múltiplos. Esta é uma ótima razão para aprender este comando.

- Lembre-se, se você quer aprender comandos avançados, simplesmente consulte o manual que deve estar presente em todas as versões Unix.

> man curl

Espero que este tutorial seja um bom começo para você usar o Curl.

