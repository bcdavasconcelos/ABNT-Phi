[![DOI](https://raw.githubusercontent.com/bcdavasconcelos/CSL-ABNT-para-Autores-Antigos/main/zenodo.4305064.svg)](https://zenodo.org/badge/latestdoi/303481460)

# ABNT-Phi

O [ABNT-Phi](https://github.com/bcdavasconcelos/ABNT-Phi) é um arquivo no formato *[Citation Style Language](https://en.wikipedia.org/wiki/Citation_Style_Language)* (CSL) que serve como conjunto de regras para determinar como os dados contidos na bibliografia devem ser exibidos no texto. Ele foi desenvolvido especialmente para a conversão de documentos utilizando o [Pandoc](https://pandoc.org/MANUAL.html#citation-rendering), mas também pode ser utilizado em programas como o [Zotero](https://www.zotero.org) para gerar bibliografia em diversos processadores de texto (*e.g.* Microsoft Word, LibreOffice, *etc*). 

A motivação para adaptar o estilo [ABNT tradicional](https://github.com/citation-style-language/styles/blob/master/associacao-brasileira-de-normas-tecnicas.csl) em uma variante especializada na área da Filosofia e Estudos Antigos deve-se ao fato de que este, bem como os demais estilos CSL, jamais levam em conta a necessidade de incluir nas citações no corpo do texto algum dado para além de AUTOR e ANO. Nestas áreas, entretanto, frequentemente citamos obras clássicas a partir de um [sistema de abreviações](http://dge.cchs.csic.es/lst/lst1.htm) consagrado no meio acadêmico especializado. Além disso, eventualmente pode ser mais relevante incluir o nome do editor ou do tradutor do texto, visto que o nome do autor já é conhecido e está pressuposto.   

## Especificidade do ABNT-Phi

Consideremos as entradas bibliográficas abaixo em formato BibTeX:

```bibtex

@incollection{EN,
author = {Aristóteles},
editor = {Bekker, Immanuel},
title = {Ἠθικὰ Νικομάχεια},
booktitle = {Aristotelis Opera},
shorttitle = {EN},
pages = {1094a01-1181b23},
year = {1831},
publisher = {Reimer},
location = {Berlim}
}

@book{DAReeve,
author = {Aristóteles},
translator = {Reeve, C. D. C.},
annote = {REEVE},
title = {De Anima},
year = {2017},
publisher = {Hackett},
location = {Indianápolis}
}

```

Ao citar estas entradas utilizando o estilo ABNT tradicional, o resultado seria `(ARISTÓTELES 1831)` e `(ARISTÓTELES 2017)`. 

O ABNT-Phi, ao contrário, dará preferência ao conteúdo de dois campos em particular. 

1. `shorttitle` serve para abreviações. Se o campo estiver preenchido, **apenas** a abreviação será impressa, em *itálico* e **sem o ano**.  
2. `annote` serve para nome(s) pertinente(s) que deve(m) substituir o nome do autor. O conteúdo será impresso *exatamente como se encontra* (sem capitalização ou qualquer outra modificação) seguido do ano.  

A ordem de preferência, portanto, é `shorttitle` depois `annote`. Se shorttitle estiver preenchido, seu conteúdo terá preferência e apenas ele será impresso. Caso não possua, então `annote` terá preferência e seu conteúdo será impresso seguido do ano (`year`). Logo, ao citar as entradas acima, teríamos `EN` e `Reeve 2017`.  

Na prática, isso quer dizer que você pode utilizar esse estilo para manipular toda a citação de uma determinada obra e terá a opção de escolher o conteúdo a ser impresso e se o ano deve ser incluído ou não (se utilizar `shorttitle` o ano ficará de fora; se utilizar `annote` ele será impresso normalmente).  

O estilo pode ser utilizado com o Pandoc (v. `2.14` em diante) e com gerenciadores de bibliografia como Zotero e Mendeley.  

# Instruções para testar

- Faça o download e instale o [Pandoc](https://pandoc.org/MANUAL.html) (esse estilo também pode ser utilizado com o Zotero ou o Mendeley, mas eu não uso nenhum desses dois programas regularmente).  
- Baixe o conteúdo deste repositório, mude o nome para Pandoc e mova para a sua pasta do Dropbox (ou alguma outra de sua preferência).  
- Para acrescentar a bibliografia a uma conversão do Pandoc, basta adicionar alguns elementos ao comando, como a flag `-C`  seguida de `--csl=` e o endereço do arquivo CSL; `--bibliography=` e o arquivo da bibliografia.  

No meu caso, os arquivos estão na seguinte localização:  

`~/Dropbox/Pandoc/refs.bib`  
`~/Dropbox/Pandoc/abnt-phi.csl`  

Portanto, devo acrescentar:

```bash
-C "--bibliography=$HOME/Dropbox/Pandoc/refs.bib" "--csl=$HOME/Dropbox/Pandoc/abnt-phi.csl" 
```

O comando completo, portanto, seria:

```bash
pandoc -f markdown "$HOME/Dropbox/Pandoc/test.md" -t docx -o "$HOME/Dropbox/Pandoc/test.docx" -C "--csl=$HOME/Dropbox/Pandoc/abnt-phi.csl" "--bibliography=$HOME/Dropbox/Pandoc/refs.bib"
```

![Esq: fonte | Dir: versão renderizada](./test.png)  

Para fazer download do ABNT-Phi, visite o repositório no [Github](https://github.com/bcdavasconcelos/ABNT-Phi).  
Uma versão mais antiga desse projeto pode ser encontrada em [CSL ABNT para autores antigos](https://github.com/bcdavasconcelos/CSL-ABNT-para-Autores-Antigos).
