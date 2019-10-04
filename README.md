# Especificações técnicas de cartografia e informação geográfica de referência - reCart

Oficina de Dados Abertos, 3 e 4 de outubro, 2019, Águeda

## Objetivo

* Olhar para a nova especificação da Cartografia
    * Simbologia
    * Modelo de dados
        
* Encaixar esta cartografia no contaxto do SIG municipal
    * Relacionar a cartografia com os modelos de dados de trabalho (relacionar com SIG interno)
    * Migrar cartografia existente para o novo modelo (e ter de borla os novos estilos, ferramentas, etc)
    * Relacionar esta cartografia com SIG externos usando links/ids permanentes (DGT, INE, SNIAMB, REN, etc)

* Ponto de vista do Município (e não do produtor)

## Documentos de apoio

[Regulamentação](http://www.dgterritorio.pt/cartografia_e_geodesia/regulacao/)

[Especificações técnicas](http://www.dgterritorio.pt/filedownload.aspx?schema=f7664ca7-3a1a-4b25-9f46-2056eef44c33&channel=adab3c46-b36f-437d-a04f-cba7c3b3664e&content_id=96B7FE9A-D4A3-4003-8BEE-0A8897C4FE07&field=storage_image&lang=pt&ver=1&filetype=pdf&dtestate=2019-07-30143601)

## Temas do reCart

### Unidades administrativas

### Toponímia

### Altimetria

### Hidrografia

### Transportes

### Construções

### Ocupação do solo

### Infraestruturas e serviços de interesse público

### Mobiliário urbano e sinalização

## Comentários

* Nova versão do `recart`
    * Com a simbologia em base de dados
        * Inclui simbologia para o QGIS e Geoserver (SLD)
        * Tabela `layer_style`
        * ![](https://i.imgur.com/dpAh89X.png)
        * Múltiplas simbologia
            * Simbologia simplificada
    * Simbologia SVG
        * [SVG](https://gist.github.com/ntma/088b6cd460358d4d122d499c6c8c23e5)
    * Projeto QGIS (projeto pode ser reutilizado)
        * Acesso com pg_services 

* Simbologia
    * Unidades do mapa
        * Simbologia pensada para impressão a 1:10k
        * Redifinir as dimensões em função das unidades do mapa

* Simbologia
    * Etiquetas
        * Para alguns temas, o recurso a etiquetas aumenta a legibilidade, como a elevação nas curvas de nível mestra, nalguns tipos de edifício, em alguns espaços públicos, etc.
        
* Modelo de dados
    * Tudo no esquema public
        * Separar temas em esquemas
    * Separar diferentes tipos de geometrias em diferentes camadas
        * Exemplo (separação de `area_curso_de_agua` e `curso_de_agua`)

* Modelo de dados
    * Procedimentos
        * Suporte ao ciclo de vida através do histório de todos os objectos
        * Possibilidade de ver todo o histório e reverter qualquer alteração
        * Mecanismo transparente ao utilizador (automatizado no lado da base de dados)
        * Triggers para gestão do ciclo de vida das entidades segundo directiva INSPIRE adaptado ao modelo Recart: https://gitlab.com/snippets/1901117
![](https://i.imgur.com/4WrYnlE.png)
![](https://i.imgur.com/7gYJwxv.png)
![](https://i.imgur.com/exArPJp.png)

## Outras contribuições

## Contribuição para o QGIS

O conjunto Postgresql e QGIS respondem às necessidades dos municípios em geral. Em particular, para suportar as novas especificações (eventualmente mantendo a proposta de base de dados), é necessário melhorar o QGIS em termos de suporte a tabelas com geometrias de diversos tipos.
* Suportar múltiplas geometrias do tipo 3d
* Suportar estilos diferentes consoante o tipo de geometria

## Visualizadores

### OpenLayers + Geoserver

#### Altimetria

![](https://i.imgur.com/nPCU53P.png)

#### Hidrografia

![](https://i.imgur.com/Z3idrHG.png)

### QGIS Server + projeto QGIS

## Hale Studio
Hale studio é uma ferramenta que permite realizar transformações entre diferentes modelos de dados. Disponível no [GitHub](https://github.com/halestudio/hale) sobre GPLv3.

Foi elaborado um caso de estudo com a transformação e importação dos cursos de água disponibilizados pela SNIAmb para o Recart.

* Tuturial [Hale Studio para harmonização em Recart](http://md.geomaster.pt/xPUnJ23GQb68sCajKevIuQ#)
* [Regras de alinhamento](https://geo.di.uminho.pt/owncloud/index.php/s/QQkqdDt11K6w2Ob/download)

### Análise
* Alternativa mais acessível a scripts sql
* Formaliza as relações estabelecidas entre os modelos de dados
![](https://i.imgur.com/Kx904TV.png)
* Alinhado com directiva INSPIRE

