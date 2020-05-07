---
layout: post
title:  "Prompt: Comandos de Rede"
date:   2020-02-07 00:00:00
description: # Primeiro post
img: semconexao.jpg # Add image post (optional)
---

Sou usuário do Windows e já tive bastante problemas de conexão, simplesmente não entrava em nenhum site, nas minhas pesquisas vários tutoriais indicavam pra reinstalar o navegador, testar outro navegador, entrar no modo anônimo, limpar o cache, redefinir o Protocolo IP, desabilitar o Proxy no DNS e nada disso resolvia, foi então que resolvi buscar comandos avançados do Prompt de Comando que reiniciasse as configurações de rede. 

---

1. Para abrir o Prompt vá no *Menu Iniciar*, em seguida na pasta Acessórios, clique com o botão direito e execute como administrador.

	![acessorios]({{site.baseurl}}/assets/img/foto-post1.jpg)
 
2. Tela do Prompt

	![prompt]({{site.baseurl}}/assets/img/foto-post2.jpg)

3. Digite os seguintes comandos:

	```dos
	C:\>NETSH INT IP RESET all
	C:\>netsh winsock reset all
	C:\>ipconfig /release 
	C:\>Ipconfig /flushdns
	```

4. Reinicie o computador

---
O Windows oferece várias soluções por meio da interface gráfica simplificada, usar a linha de comando requer mais conhecimento, sendo mais utlizado por quem administra servidores, executando rotinas complexas com mais velocidade e segurança. 

