# Magento
## Módulos e Templates de Página
 O Magento realiza uma busca hierarquizada que tem por objetivo encontrar os módulos e os templates necessários para que a página da loja virtual funcione.

Ao ser inicializada, a busca prioriza encontrar os arquivos de módulos e temas que foram definidos pelo usuário. Esses arquivos servem a função de sobrescreverem os arquivos padrão do Magento, que estão alocados nas pastas `app/base/` e `app/code/core`. 

Ou seja, alterações nas páginas do Magento são definidas em seus próprios arquivos. Sendo assim, os arquivos padrão do Magento não podem ser alterados. É uma boa prática e, também, é a forma mais segura de se aplicar alterações nas páginas do Magento, uma vez que os arquivos padrão são substituídos e gerados ao se atualizar a plataforma, o que pode ocasionar na perda das alterações.

## Locais Importantes
- `app/code/community` são os módulos baixados, módulos desenvolvidos pela comunidade.
- `app/code/local` são os módulos locais, desenvolvidos pelo usuário.
- `app/design/frontend/base` arquivos padrão do tema do Magento.
- `app/design/frontend/<companyName>/<themeName>/` arquivos de temas instalados.
- `app/etc/local.xml` arquivo de configurações does usuários do PHP e MySQL, além de outras configurações do Magento
- `var/log` arquivos de log
- `etc/`   pasta de aplicações utilizadas pelo servidor, como PHP e MySQL

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMzODIyOTI4N119
-->