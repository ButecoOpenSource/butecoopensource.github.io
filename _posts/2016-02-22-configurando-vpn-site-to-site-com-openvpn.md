---
layout: wordpress
title: Configurando VPN site-to-site com OpenVPN
excerpt: |
  Resumo
  O OpenVPN é um software livre e open-source para criar redes privadas virtuais do tipo ponto-a-ponto ou server-to-multiclient através de túneis criptografados entre computadores. Ele é capaz de estabelecer conexões diretas entre computadores mesmo que estes estejam atrás de Nat Firewalls sem necessidade de reconfiguração da sua rede. Ele foi escrito por James Yonan e publicado sob licença GNU General Pulic Licence (GPL)
date: 2016-02-22 23:24:51
author: daniel_magevski
permalink: /configurando-vpn-site-to-site-com-openvpn/
image: /assets/wp-content/uploads/2016/01/openvpn-logo.png
categories:
  - Ferramentas
tags:
  - openvpn
  - redes
  - vpn
---

Irei mostrar uma configuração básica de uma VPN Site-to-Site com o <a href="https://openvpn.net/" target="_blank">OpenVPN</a>

Iremos seguir esse esquema de rede que fiz no<a href="https://www.gns3.com/" target="_blank"> GNS3</a>

<a href="/assets/wp-content/uploads/2016/01/screenshot.png" rel="attachment wp-att-4433"><img class="alignnone wp-image-4433" src="/assets/wp-content/uploads/2016/01/screenshot.png" alt="screenshot" width="687" height="416" /></a>

Estou utilizando um <a href="https://pt.wikipedia.org/wiki/Servidor_virtual_privado" target="_blank">SVP</a> - Servidor Virtual Privado (VPS - <em>Virtual Private Server</em>) para demonstrar a instalação e configuração, meu ambiente de instalação é um Debian 8.2.

<em>Distributor ID: Debian</em>
<em> Description: Debian GNU/Linux 8.2 (jessie)</em>
<em> Release: 8.2</em>
<em> Codename: jessie</em>

<strong>Resumo</strong>

O OpenVPN é um software livre e open-source para criar redes privadas virtuais do tipo ponto-a-ponto ou server-to-multiclient através de túneis criptografados entre computadores. Ele é capaz de estabelecer conexões diretas entre computadores mesmo que estes estejam atrás de Nat Firewalls sem necessidade de reconfiguração da sua rede. Ele foi escrito por James Yonan e publicado sob licença GNU General Pulic Licence (<a href="https://pt.wikipedia.org/wiki/GNU_General_Public_License" target="_blank">GPL</a>)

<strong>Instale o OpenVPN e também o easy-rsa</strong>

<code>apt-get install openvpn easy-rsa</code>

Agora entramos no diretório do OpenVPN, utilizamos o comando make-cadir (disponibilizado pelo pacote easy-rsa) para criar um diretório chamado <code>easy-rsa</code> que conterá vários <em>scripts</em> úteis. Entramos no diretório <code>easy-rsa</code> e editamos o arquivos chamado vars.

<code>root@wolf:~# cd /etc/openvpn/
root@wolf:/etc/openvpn# make-cadir easy-rsa
root@wolf:/etc/openvpn# cd easy-rsa/
root@wolf:/etc/openvpn/easy-rsa# nano vars</code>

<strong>Agora vá ate o final e edite os seguintes valores</strong>
<pre># These are the default values for fields
# which will be placed in the certificate.
# Don't leave any of these fields blank.
export KEY_COUNTRY="BR"
export KEY_PROVINCE="Espirito-Santo"
export KEY_CITY="Vila-Velha"
export KEY_ORG="Butecopensource"
export KEY_EMAIL="daniel@butecopensource.org"
export KEY_OU="butecopensource.org"
</pre>
Após editar o arquivo use:

<code>source vars</code>

e depois

<code>./clean-all</code>

<strong>Criando os certificados</strong>

Durante esse processo você será perguntado dos valores para alguns campos, os quais definimos no arquivo <code>vars</code> que ficarao entre colchetes, quando for o Common Name utilize o nome da máquina.

<strong>Gerando o certificado da sua unidade certificadora</strong>

<code>root@wolf:/etc/openvpn/easy-rsa# ./build-ca</code>
<pre>Generating a 2048 bit RSA private key
.+++
...+++
writing new private key to 'ca.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [BR]:
State or Province Name (full name) [Espirito-Santo]:
Locality Name (eg, city) [Vila-Velha]:
Organization Name (eg, company) [Butecopensource]:
Organizational Unit Name (eg, section) [butecopensource.org]:
Common Name (eg, your name or your server's hostname) [Butecopensource CA]:
Name [EasyRSA]:
Email Address [daniel@butecopensource.org]:
root@wolf:/etc/openvpn/easy-rsa#
</pre>
<strong>Gerando chave para o Servidor</strong>

Gerando a chave para o servidor. Utilize o comando <code>build-key-server</code> seguido do nome do servidor (<em>hostname</em>).

<code>root@wolf:/etc/openvpn/easy-rsa# ./build-key-server server</code>
<pre>Generating a 2048 bit RSA private key
..................................+++
................................................................+++
writing new private key to 'server.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [BR]:
State or Province Name (full name) [Espirito-Santo]:
Locality Name (eg, city) [Vila-Velha]:
Organization Name (eg, company) [Butecopensource]:
Organizational Unit Name (eg, section) [butecopensource.org]:
Common Name (eg, your name or your server's hostname) [server]:
Name [EasyRSA]:
Email Address [daniel@butecopensource.org]:

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
Using configuration from /etc/openvpn/easy-rsa/openssl-1.0.0.cnf
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
countryName :PRINTABLE:'BR'
stateOrProvinceName :PRINTABLE:'Espirito-Santo'
localityName :PRINTABLE:'Vila-Velha'
organizationName :PRINTABLE:'Butecopensource'
organizationalUnitName:PRINTABLE:'butecopensource.org'
commonName :PRINTABLE:'server'
name :PRINTABLE:'EasyRSA'
emailAddress :IA5STRING:'daniel@butecopensource.org'
Certificate is to be certified until Jan 2 22:29:18 2026 GMT (3650 days)
Sign the certificate? [y/n]:y
1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated
root@wolf:/etc/openvpn/easy-rsa#
</pre>
Agora vamos gerar uma chave <a href="https://pt.wikipedia.org/wiki/Diffie-Hellman" target="_blank">Diffie-Hellman</a> e que será utilizada pelo cliente e servidor durante a troca de chave, pode demorar um certo tempo.
Obs: Não gere chave com valor igual o menor que 1024 bits, por padrão esse <em>script</em> gera em 2048 bits

<code>root@wolf:/etc/openvpn/easy-rsa# ./build-dh</code>
<pre>Generating DH parameters, 2048 bit long safe prime, generator 2
This is going to take a long time
............................+++
</pre>
<strong>Gerando chave para o cliente</strong>

Nesse tutorial iremos gerar somente uma chave, para a filial, porém dependendo de como você irá implementar sua VPN você pode criar mais.

<code>root@wolf:/etc/openvpn/easy-rsa# ./build-key filial</code>
<pre>Generating a 2048 bit RSA private key
..............................................................................................................+++
......................+++
writing new private key to 'filial.key'
-----
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
Using configuration from /etc/openvpn/easy-rsa/openssl-1.0.0.cnf
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows/code&gt;
countryName :PRINTABLE:'BR'
stateOrProvinceName :PRINTABLE:'Espirito-Santo'
localityName :PRINTABLE:'Vila-Velha'
organizationName :PRINTABLE:'Butecopensource'
organizationalUnitName:PRINTABLE:'butecopensource.org'
commonName :PRINTABLE:'filial'
name :PRINTABLE:'EasyRSA'
emailAddress :IA5STRING:'daniel@butecopensource.org'
Certificate is to be certified until Jan 2 23:13:45 2026 GMT (3650 days)
Sign the certificate? [y/n]:y
1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated
root@wolf:/etc/openvpn/easy-rsa#
</pre>
<strong>Excluar os arquivos desnecessários</strong>

<code>rm keys/*.csr</code>

Pronto, agora precisamos pegar os arquivos no servidor e passar cliente,

<code>root@wolf:/etc/openvpn/easy-rsa# cd keys</code>
<code>root@wolf:/etc/openvpn/easy-rsa/keys# ls</code>
<pre>01.pem ca.key filial.key index.txt.attr.old serial.old
02.pem dh2048.pem index.txt index.txt.old server.crt
ca.crt filial.crt index.txt.attr serial server.key
</pre>
Iremos precisar dos arquivos, <strong>filial.crt,  filial.key, dh2048.pem</strong>

Vocẽ pode copiar esses arquivos com softwares como <a href="https://filezilla-project.org/" target="_blank">FileZilla</a> (Linux e Windows) ou <a href="https://winscp.net/eng/download.php" target="_blank">WinSCP</a> (Windows).

<strong>Configuração do OpenVPN para o servidor</strong>

<code> Crie o arquivo /etc/openvpn/server.conf </code>

Caso você cria o nome do servidor direrente de "server", lembre de mudar o nome do <strong>"crt"</strong> e <strong>"key"</strong>

Veja o arquivo de configuração.

```sh
##############################
####### OpenVPN Server #######
####### Site-to-Site##########
##############################
####### DANIEL MAGEVSKI ######
##############################


# Para testar os arquivos de configuracao:
# openvpn --config /etc/openvpn/arquivo.conf

# Para fazer NAT, execute:
# sysctl -w net.ipv4.ip_forward=1
# iptables -t nat -s $IP_REDE/$MASCARA_REDE -A POSTROUTING -o $PORTA_INTERNET -j MASQUERADE


##############################
#     Dados da conexão
##############################


# Interface da VPN
dev tun0
# Endereço IP servidor/filial
ifconfig  $Ip-Servidor $IpFilial

# Protocolo
proto udp

# Porta VPN
port 1194

# Parametro necessario para utilizar conexão com certificados X509
tls-server

# Caminho para o arquivo contendo parametros Diffie Hellman
dh /etc/openvpn/easy-rsa/keys/dh2048.pem

# Local do arquivo de certificado (.crt) da unidade certificadora
ca /etc/openvpn/easy-rsa/keys/ca.crt

# Local do arquivo de certificado (.crt) do servidor
cert /etc/openvpn/easy-rsa/keys/$server.crt

# Local da chave (.key) do servidor. Este arquivo deve ser mantido secreto
key /etc/openvpn/easy-rsa/keys/$server.key

##############################
#   Qualidade da conexão
##############################


# Pinga o host remoto a cada $x segundos sem atividade na rede, se ele
# nao responder por $z segundos a conexão é reiniciada.
# Quando a conexão é interrompida o cliente tenta restabelece-la  periodicamente
# Uso: keepalive $x $z
keepalive 10 120

# Compacta os dados da conexão utilizando o pacote lzo (deve estar
# instalado no host)
# Se estiver habilitado no servidor, o cliente também deve habilitar
comp-lzo

# mantem as chaves carregadas mesmo durante o reinicio do serviço.
persist-key

# mantem o tunel aberto mesmo durante o reinicio do serviço.
persist-tun

# Fica tentando, indefinidamente, resolver o nome do host do servidor. Útil
# em hosts que não estão permanentemente conectados à internet.
resolv-retry infinite

# Mantem o tunel aberto mesmo se o ip do outro host mudar
float

# É uma boa prática diminuir os privilégios do OpenVPN após a inicialização.
user nobody 
group nogroup

# Define o quão verboso será o log.
# 0 é silencioso, exceto por erros fatais
# 4 é rasoável para o uso geral
# 5 e 6 podem ajudá-lo a debugar problemas de conexão
# 9 é extremamente verboso
verb 3


# Informações de status da conexão
status /var/log/openvpn/matriz-staus.log
# Arquivo de log
log-append /var/log/openvpn/matriz.log

##############################
####    Referências   ########
##############################

# http://tobias.ws/blog/acesso-seguro-a-internet-atraves-do-openvpn/
# http://openvpn.net/howto.html#mitm
# http://www.hardware.com.br/tutoriais/openvpn_2/
```

Agora vamos adicionar a rota, criando um arquivo dentro do diretório /etc/init.d:
 <code>echo "route add -net 192.168.1.0 netmask 255.255.255.0 gw 10.8.0.1 dev tun0" &gt; /etc/init.d/rota &amp;&amp; chmod +x rota &amp;&amp; update-rc.d rota defaults</code>

Após criada a rota, será iniciado o serviço:
 <code>service openvpn start</code>

Precisamos compartilhar a internet do servidor, execute:
 <code>sysctl -w net.ipv4.ip_forward=1</code>

<code>iptables -t nat -s 10.8.0.0/24 -A POSTROUTING -o eth0 -j MASQUERADE</code>

10.8.0.0/24 é a rede da VPN e eth0 é a interface do servidor que está conectada com a internet.

<strong>Configuração no cliente</strong>

Crie o arquivo client.ovpn e lembre de substituir e $Cliente nos parâmentos cert e key, $Servidor no remote.

Veja o arquivo de configuração.


```sh
##############################
####### OpenVPN Server #######
####### Site-to-Site##########
##############################
####### DANIEL MAGEVSKI ######
##############################

##############################
##### Dados da conexão  ######
##############################


# Define que esta máquina é um cliente
client

# Endereço do servidor
remote  $Servidor 1194 #Por padrão a porta é 1194

# Interface da VPN
dev tun0

# Endereço IP filial/servidor
ifconfig $IpFilial $Ip-Servidor 

# Protocolo
proto udp

nobind

# Se você está conetando à internet através de um proxy HTTP, defina o parâmetro
# http-proxy.
# http-proxy-retry faz com que uma nova tentativa seja feita em casa de falha
# de conexão
;http-proxy-retry
;http-proxy $ip $porta


##############################
#      Certificados X509
##############################

# Local do arquivo dh.pem
dh dh2048.pem

# Local do arquivo de certificado (.crt) da unidade certificadora
ca ca.crt

# Local do arquivo de certificado (.crt) do cliente
cert filial.crt

# Local da chave (.key) do cliente. Este arquivo deve ser mantido secreto
key filial.key


##############################
#   Qualidade da conexão
##############################

# Pinga o host remoto a cada $x segundos sem atividade na rede, se ele
# nao responder por $z segundos a conexão é reiniciada.
# Quando a conexão é interrompida o cliente tenta restabelece-la  periodicamente
# Uso: keepalive $x $z
keepalive 10 120

# Compacta os dados da conexão utilizando o pacote lzo (deve estar
# instalado no host)
# Se estiver habilitado no servidor, o cliente também deve habilitar
comp-lzo

# mantem as chaves carregadas mesmo durante o reinicio do serviço.
persist-key

# mantem o tunel aberto mesmo durante o reinicio do serviço.
persist-tun

# Fica tentando, indefinidamente, resolver o nome do host do servidor. Útil
# em hosts que não estão permanentemente conectados à internet.
resolv-retry infinite

# mantem o tunel aberto mesmo se o ip do outro host mudar
float

##############################
#           Outros
##############################

# Define o quão verboso será o log.
# 0 é silencioso, exceto por erros fatais
# 4 é rasoável para o uso geral
# 5 e 6 podem ajudá-lo a debugar problemas de conexão
# 9 é extremamente verboso
verb 3

# Informações de status da conexão
status openvpn-status.log
#status /var/log/openvpn/matriz-staus.log
# Arquivo de log
;log         openvpn.log
;log-append  openvpn.log


##############################
####    Referências   ########
##############################

# http://tobias.ws/blog/acesso-seguro-a-internet-atraves-do-openvpn/
# http://openvpn.net/howto.html#mitm
# http://www.hardware.com.br/tutoriais/openvpn_2/
```

Agora vamos adicionar a rota crie um arquivo rota

<code> echo "route add -net 192.168.0.0 netmask 255.255.255.0 gw 10.8.0.2 dev tun0" &gt; /etc/init.d/rota &amp;&amp; chmod +x rota &amp;&amp; update-rc.d rota defaults </code>

Agora vamos acessa-la, entra dentro do diretório onde está as chaves e digite,
<code>openvpn client.ovpn </code>

Ele irá imprimir na tela os dados na conexão, se tudo ocorreu bem aparecerá, <strong>Initialization Sequence Completed</strong>

Qualquer dúvida escreva nos comentários.
