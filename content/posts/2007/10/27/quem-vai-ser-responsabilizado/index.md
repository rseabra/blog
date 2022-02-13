---
title: "Quem vai ser responsabilizado?"
date: "2007-10-27"
tags: 
  - "growling"
  - "tech"
---

É já bem público por várias fontes que o site da última campanha da Optimus tinha graves falhas de segurança.

Era algo mais ou menos nesta onda:

\# mysql -u CENSURADO -p -h CENSURADO lojaoptimusnet
Enter password:
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MySQL monitor.  Commands end with ; or \\g.
Your MySQL connection id is 385 to server version: 4.1.20-log

Type 'help;' or '\\h' for help. Type '\\c' to clear the buffer.

mysql> show databases;
+-------------------------------+
| Database                      |
+-------------------------------+
| afiliados                     |
| clubexxp\_forum                |
| clubexxp\_forum\_backup         |
| clubexxp\_teste                |
| drsaude                       |
| enginsite\_addons              |
| lojaoptimusnet                |
| mobilegames                   |
| mysql                         |
| newsletters\_adslnovis         |
| newsletters\_barclaycard       |
| newsletters\_creditopessoal    |
| newsletters\_drsaude           |
| newsletters\_edp5d             |
| newsletters\_europassistance   |
| newsletters\_exchange          |
| newsletters\_experimentapascoa |
| newsletters\_ezalo             |
| newsletters\_fiducial          |
| newsletters\_geral             |
| newsletters\_geralnovis        |
| newsletters\_guardsat          |
| newsletters\_homecare          |
| newsletters\_myjobs            |
| newsletters\_optimus           |
| newsletters\_optimus\_a         |
| newsletters\_optimushome       |
| newsletters\_optimushomerec    |
| newsletters\_optimuspopular    |
| newsletters\_poupardinheiro    |
| newsletters\_readersdigest     |
| newsletters\_saudedirect       |
| newsletters\_saudefinance      |
| newsletters\_tele2             |
| newsletters\_testes            |
| newsletters\_unibanco          |
| newsletters\_unibanco\_classico |
| newsletters\_unibanco\_mini     |
| newsletters\_users             |
| pharmahouse                   |
| projectos                     |
| sites\_includes                |
| tele2\_coberturas              |
+-------------------------------+
43 rows in set (0.14 sec)

Reparem nos nomes de algumas das bases de dados albergadas por estes senhores a quem a Optimus contratou o serviço. Provavelmente há ali informação extremamente valiosa para spam, phishing e sabe-se lá mais o quê.

Só que agora quem é que vai ser responsabilizado? Os incompetentes ou quem conseguiu aceder e executar este comando?

Pela lei do crime informático, quem conseguiu aceder e executar o comando cometeu um crime. Mas vamos ser realmente honestos: a irresponsabilidade revelada por estes incompetentes é muito mais criminosa, uma vez que albergam dados pessoais e evidentemente não tomam os cuidados necessários para impedir a sua divulgação ilegítima, que sem dúvida deve ser considerada para efeitos práticos como tendo sido distribuída por pessoas com fins menos legítimos.

Os clientes que sabem ter dados pelas entidades relacionadas deveriam exigir explicações às entidades relacionadas...
