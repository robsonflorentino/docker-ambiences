# Instruções de uso

Esta é uma imagem simples do Apache, incluindo suporte SSL. Para usar essa imagem efetivamente, você precisará montar:

* /var/www/html para o conteúdo do seu site (por exemplo, usando "-v /home/nome/site:/var/www/html")
* /var/log/apache2, opcional, se você quiser armazenar arquivos de logs que sejam visíveis fora do contêiner
* /etc/ssl, opcional, se você deseja usar SSL com chaves reais.

## Um lembrete no SSL

De acordo com os padrões, o Apache usará a chave "snakeoil" incluída ao servir SSL. Obviamente isso não é suficiente ou aconselhável em ambientes de produção, então você deve montar suas chaves reais em "/etc/ssl". Se você nomeá-los "certs/ssl-cert-snakeoil.pem" e "private/ssl-cert-snakeoil.key", você poderá obter a configuração padrão. Caslo contrário, você devetá incluir uma checagem de site. Se vocé não quiser usar SSL, podera desabilitar o encaminhamento da porta 443 ao iniciar o contêiner(Veja logo abaixo).

## Exemplos simples

Assumindo que seu conteúdo esta em "/home/user/site", o exemplo abaixo será o suficiente para atendê-lo. Observe que muitos usuários do Docker incentivam a montagem de dados de um contêiner de armazenamento, em vez de diretamente do arquivo.

* "It works!" : `docker run -p 80:80 -p 443:443 -d rflorent/apache` e navegue até o endereço IP do host usando http ou https

* Servindo o conteúdo atual com suporte SSL: `docker run -p 80:80 -p 443:443 -v /home/user/site:/var/www/html -d rflorent/apache`

* Servindo o conteúdo atual sem suporte SSL: `docker run -p 80:80 -v /home/user/site:/var/www/html -d rflorent/apache`

* Servindo o conteúdo atual sem usar as portas padrões: `docker run -p 8080:80 -p 8443:443 -v /home/user/site:/var/www/html -d rflorent/apache`