---
layout: wordpress
title: Configurações do OpenSSH que podem fazer toda a diferença
date: 2016-03-09 23:57:19
author: alexandrevicenzi
permalink: /configuracoes-do-openssh-que-podem-fazer-toda-a-diferenca/
image: /assets/wp-content/uploads/2016/03/OpenSSH_logo.png
categories:
  - Dicas
tags:
  - linux
  - openssh
  - segurança
  - ssh
---

Para quem possui algum servidor, ou até para em seu computador pessoal, algumas configurações padrão do servidor SSH são extremamente permissivas, vulneráveis a ataques, e quem sabe até invasão com técnicas de <a href="https://en.wikipedia.org/wiki/Brute-force_attack" target="_blank">força bruta</a>.

Entre algumas dicas mais simples para aumentar a segurança estão configurar o seu firewall corretamente ou até desabilitar o acesso SSH. Para servidores, esta última opção não é válida. Sendo assim vamos conferir algumas configurações que podem fazer toda a diferença na hora de algum espertinho tentar invadir seu servidor.

<!--more-->

As configurações do <code>sshd</code>,daemon SSH, estão por padrão no arquivo <code>/etc/ssh/sshd_config</code>. Então, escolha o seu editor favorito para alterar este arquivo.

<strong>Alterando a porta padrão</strong>

Por padrão o SSH utiliza a porta 22, uma boa prática é mudar este valor pois a maioria dos ataques são executados diretamente nesta porta. Dê preferência às portas altas, pois em uma varredura rápida de um atacante sem alvo específico com NMAP, não será mapeada.

<code>Port 22222</code>

<strong>Versão do protocolo</strong>

A versão 1 do protocolo SSH possui várias falhas de criptografia e não deve ser utilizada.

<code>Protocol 2</code>

<strong>Login apenas por chave SSH</strong>

Uma boa prática é permitir apenas login com chaves SSH, isto garante a autenticidade do cliente. Login através de senha é suscetível a força bruta, utilizando de dicionários com senhas junto com programas como o <a href="https://pt.wikipedia.org/wiki/John_the_Ripper" target="_blank">john the ripper</a>, utilizar certificados você mitiga este risco.

<code>PasswordAuthentication no</code>

<strong>Login sem senha</strong>

Quando login através de senha está habilitado, uma boa prática é não permitir login de usuário que não possui senha.

<code>PermitEmptyPasswords no</code>

<strong>Login root</strong>

Permitir o login SSH através do usuário root é desaconselhável, prefira usar uma conta de usuário e após conectado faça login como superusuário.

<code>PermitRootLogin no</code>

<strong>Tempo máximo para login</strong>

Indica o tempo máximo em segundos que o cliente SSH tem para se logar com sucesso ao servidor.

<code>LoginGraceTime 30</code>

<strong>Tempo máximo sem atividade</strong>

Permitir que um usuário fique horas conectados a uma sessão SSH sem executar nenhum comando é desaconselhável. É recomendado definir um tempo máximo em segundos para desconectar o usuário sem atividade.

<code>ClientAliveInterval 300</code>

<strong>Testando as alterações</strong>

Sempre que uma alteração é feita no arquivo é aconselhável executar um teste para verificar se a sintaxe está correta, sendo assim execute o comando:

<code>/usr/sbin/sshd -t</code>

Se nenhuma mensagem foi exibida tudo está correto.

<strong>Reiniciando o sshd</strong>

Reiniciar o serviço irá variar de distribuição para distribuição, pois tudo depende do <em>init system</em> utilizado por ela. No Systemd você pode executar o comando <code>systemctl restart sshd</code>, no Upstart <code>service sshd restart</code> e por fim no SysV o <code>/etc/init.d/sshd restart</code>.

<strong>Consideração final</strong>

Essas configurações são simples, mas podem evitar uma dor de cabeça no futuro. Para saber mais sobre as demais configurações do OpenSSH confira a referência.

<strong>Dica especial :D</strong>

E se eu tiver suspeitas de que meu servidor está sendo invadido? ou, sou paranóico com a segurança do meu servidor. O que eu posso fazer? <em>tcp_wrapper</em>, <em>fail2ban</em>? Ou porque não receber um e-mail toda vez que alguém logar via ssh no meu servidor?

Existe um arquivo que você pode alterar chamado <code>sshrc</code> que fica no diretório padrão da sua pasta de configuração do ssh, por exemplo <code>/etc/ssh/sshrc</code>. Neste exemplo vamos enviar um email através programa chamado <em>sendEmail</em>, confira.

<pre><code class="bash">
ip=`echo $SSH_CONNECTION | cut -d &quot; &quot; -f 1`

logger -t ssh-wrapper $USER login from $ip
mensagem=`echo &quot;User $USER just logged in from $ip&quot;`
echo $mensagem | sendEmail -o tls=yes -f meu_email@gmail.com -t email_destino@gmail.com -s &quot;smtp.gmail.com:587&quot; -m &quot;$mensagem&quot; -u &quot;$mensagem&quot; -xu 'meu_usuario@gmail.com' -xp 'minha_senha'
</code></pre>

<em>Nota, caso use o Gmail, é necessário desabilitar uma funcionalidade de segurança que permite aplicativos menos seguros acessar sua conta, para saber mais <a href="https://www.google.com/settings/security/lesssecureapps" target="_blank">clique aqui</a>.</em>

<strong>Referência</strong>

<a href="http://www.freebsd.org/cgi/man.cgi?sshd(8)" target="_blank">sshd -- OpenSSH SSH daemon</a>
<a href="http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man5/sshd_config.5?query=sshd_config" target="_blank">sshd_config — OpenSSH SSH daemon configuration file</a>