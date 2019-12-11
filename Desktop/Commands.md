# Comandos Variados  e Informações sobre Linux

## `../../../` 

- `/` é o mesmo que root
- `.` pasta atual  
  
##  `grep -rnw <local> -e '<term>'`
## /var/log  
>  Arquivos de log do servidor .

## `man <?>`  
> Manual, guia para um comando <?>.
  
## `tail -n<num> <filename>`  
> Número das últimas linhas de um arquivo.
## Meta-caractere `~`  
> Retorna à pasta padrão do usuário,
  
## `pwd`
>  Mostra o caminho atual.
  
## `htop`  
>  Monitoramento de tarefas do sistema
  
## `free -h`  
> Quantidade de memória física e virtual livre no sistema.

> Não é possível particionar um servidor caso ele tenha swap memory .
  
## `nano`
>  Editor de texto, simples.    
>  
# Comando  `ls`
- **l**i**s**t -**l**ong

### `ls -l`  
> Mostra mais informações sobre os arquivos, como permissões.

-  -**l**ong

  
### `ls -a`  
>  Ative a exibição de arquivos ocultos.

> `ls -la` **<=>** `ls - al`  
As opções são intercambiáveis (-l e -a são opções).
 
- -**a**ll

# Comando  `df` 
> Espaço disponível em disco.

**d**isk **f**ree
### `df -h`  
> **Problema**: mais de 60%  de espaço sendo  utilizado.

 -**h**umanreadable
  
### `df -i`  
> Index node é um tipo de **estrutura de dados** que descreve um objeto do sistema de arquivo. Ele consiste nos meta-dados de um arquivo ou diretório, como última data de modificação, e permissões de acesso.

> A pasta /var/cache/ ocupa muitos inodes.

-**i**node (**i**ndex **node**)
  
### `du -hs *`  
> Uma session ocupa muito inodes. Para diminuir o número de inodes, é necessário realizar a integração com o redis.

- **d**isk **u**sage
- -**h**umanreadable
- -**s**ummarize 
- **\*** selects everything from the current directory

# Sobre o Redis  
> Artíficio do MySQL.
  
# Configurações NGINX
## `@nginx/log`  
>  Log de requisições.
  
## `@nginx/errorlog`  
> Erros do servidor.

## `@/sites-enabled/<sitename.>`
> **Configurações do site**, como versão do PHP.

> `php -v` executa o arquivo PHP disponível na pasta `/bin` do linux, exibindo informações sobre aquele PHP específico. 
> No entanto, cada servidor (site) possui sua própria versão do PHP, que pode ser consultada no arquivo de configurações do site.
  
# Sobre MySQL

## `nano /etc/mysql/my.cnf`  
>  Arquivo de configurações (setup) do MySQL.

> Ocupa 50% da ram. Divide ram com PHP, mas MySQL é prioridade.
  
## service mysql restart  
> Este comando deve ser executado para cada alteração realizada nos arquivos de configuração.
  
## `@php/{ fpm && cli }/php.ini`  
> Todas as variáveis alteradas no arquivo php.ini dentro de uma das pastas também devem ser alteradas no outro arquivo php.ini da outra pasta.

# Sobre PHP  

## `service <app> status`  
> O PHP cria processos para que seu funcionamento não seja interrompido. Esses processos criados são chamados de processos filhos, e o número de processos filhos é configurável. O **limite de processos filhos** é geralmente 15.
  
> Averiguar as últimas linhas do arquivo de log do PHP para que se possa consultar se o número de processos filhos foi atingido durante o funcionamento do servidor.
  
## `/etc/php/pool.dd/www.conf`  
> Arquivo de configuração onde se altera número de processos filhos.

> `pm.maxchildren`  é o nome da variável.

  
> O **espaço em disco** e o **número de processos** são as principais fontes a serem consultadas caso um site esteja fora do ar .
  

## `php -i`  
> Exibe o arquivo de configurações do PHP.
  
## `php -i | grep <term>`  
 > Procura por um termo específico no arquivo de configurações do PHP.

## `php reload`  
> Atualiza as configurações do PHP. Diferente de `service <app> restart` , que reinicia o serviço (processo).

# Permissões de Arquivos  

 `{ - || d || i }` `rwx` `rwx` `rwx`

> **Indicadores:** 
> - `-` é um arquivo.
> - `d` é um diretório.
> - `i` e um link.

 [External Link \[>\]](https://www.pluralsight.com/blog/it-ops/linux-file-permissions)

## `drwxrwxrwx`

para permissões para usuário que criou a pasta | permissões para os usuários pertencentes ao grupo do usuário que criou a pasta  
// 644 arquivo | 775 pasta -@chmod  
  
@ [/] chown user:group <t>  
// muda o usuário  
  
-r  
// recursivo, muda para todo o conteúdo da pasta  
//- chown -r ..  
  
@ sites-available chmod 700  
// o atalho @sites-enabled herda as permissões  
// assim, o cliente não tem permissões para o arquivos  
  
CTRL+D  
// deslogar do usuário  
  
  
mysqldump -u<user> -p <db> > <filename.sql>  
// -p solicita o password  
  
banco de dados e usuário @ name  
// não pode exceder 16 chars.  
  
@ atualizar app/etc/local.xml  
// ambiente de staging -> sessões em arquivo  
// atualizar credencias db  
// arquivo de configuração magento 1
// magento 2 é outro nome, conf.php
  
web/unsecure&&secure/url @ phpmyadmin @> table core_data  
// atualizar o domínio do site  
// domínio deve terminar em barra (/)  
  
certbot --nginx certonly  
// gerar certificado ssh  
  
cat  
// imprime o arquivo  
  
@@ Problemas com o Magento solicitando a instalação após a duplicação de um site  
// local.xml ou banco de dados  
  
@@ mostrar linha atual  
// nano -c ...  
  
find <local> -name '<file>'  
// e.g.: -type d // busca somente diretórios  
  
grep -rnw '<local>' -e '<text>'  

zip -r staging_nina.zip ./ -x var\/cache\/\* var\/log\/\* var\/report\/\* _bkp111118_00hvictorfr_nina.sql backup-funcionando.sql.gz app\/etc\/db1304.sql  

apt-mark hold \<name\>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNTY0MjQxNDEsMTk0OTU1MDAzNCwzNT
QzMzg0MjVdfQ==
-->