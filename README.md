# Montador Absoluto da MVN

## Introdução

Este projeto é um complemento da disciplina "Sistemas de Programação".
Para entender corretamente o que deve ser feito, deve-se ter claro todos
os processos e códigos estudados e utilizados em grande parte da
disciplina, de forma que estão resumidos a seguir.

## Base de Sistemas de Programação

O montador é um programa que foi de suma importância durante muitos
experimentos do laboratório. Ele é um tipo de compilador de muito baixo
nível e, por isso, é mais simples que um compilador usual. Este
código, como utilizado na disciplina, é responsável por ler um arquivo
escrito em ASM, a linguagem de montagem da MVN, e transformá-lo em
linguagem de máquina, traduzindo os mnemônicos e operando sobre os
endereços de cada variável. O montador que foi utilizado no curso foi
escrito em uma linguagem de alto nível e tem funcionalidades bastante
avançadas, permitindo a geração de código relocável, entre outras funções.

Um montador absoluto é uma versão mais simples do montador que foi
utilizado. Nele, assume-se que todos os endereços já são absolutos, ou
seja, despreza-se as pseudo-instruções `&` e `@` do ASM. Para o
processo de montagem absoluta, deve-se, primeiramente, determinar os
endereços de cada rótulo definido no código e transformar todas as
instruções codificadas em linguagem de montagem para linguagem de
máquina, considerando os endereços previamente definidos para os
rótulos. Também deve-se tratar potenciais erros de escrita no código do
usuário, tomando as medidas cabíveis.

## O trabalho

O trabalho consiste na implementação de um montador absoluto que
converta códigos em ASM para seu análogo em MVN.

Deverá ser lido um arquivo, da forma como foi feito nos laboratório, que
contenha o código origem e deverá ser escrito, em um outro arquivo, o
código destino, realizando as conversões dos mnemônicos e dos rótulos,
como descrito acima. A possibilidade de inserir _externals_ e _entry points_
no código pode ser ignorada.

Já que um montador genérico como o usado na disciplina seria de difícil
construção em linguagem de montagem, serão adotadas simplificações
para garantir uma implementação minimamente funcional. As simplificações adotadas serão:

* Alinhar o código de forma que todos os elementos tenham número par de
  caracteres (símbolos, espaços separadores, imediatos, separador de linha
  etc.);
* Cada símbolo terá dois caracteres;
* Cada linha terminará com o par de caracteres `<s>\n`;
* O fim de arquivo `EOF` será indicado por `0000`;
* Realizar o apenas tratamento das 16 instruções;
* Desconsiderar o uso de _entry_points_ e _externals_;
* Não implementar tratamento de erro, isto é supõe-se que todo arquivo de entrada está corretamente formatado;
* Os arquivos a serem montados terão no máximos 50 linhas de código;
* O único formato possível de uma linha do arquivo `.asm` é:
  * `Label`\<s>\<s>`MNEM`\<s>\<s>`Label`\<s>\<s>`Comments`\<s>`\n`
* O formato esperado para cada linha do arquivo `.mvn` gerado é:
  * `Address`\<s>\<s>`Instruction`\<s>`\n`

Além disso, considere que o arquivo `.asm` a ser lido está no dispositivo `300`.
Enquanto, o arquivo `.mvn` deve ser escrito no disposivito `301`.

### Glossário

* `<s>`: caracter ASCII espaço.
* Label: rótulo composto por exatamente 2 caracteres ASCII.
* MNEM: mneumônico representando uma das 16 instruções.
* Value: valor hexadecimal, codificado em ASCII, composto por exatamente 4 dígitos.
* Comments: comentários, iniciados por `<s>;`, com uma quantidade qualquer de caracteres. Mas essa quantidade é sempre par e dentro de um comentário nunca haverá o caracter `\n`.
* Address: Endereço da instrução composto por 4 dígitos hexadecimais codificados em ASCII.
* Instruction: Instrução composta por seu opcode e seu operando, totalizando 4 dígitos hexadecimais codificados em ASCII.

O trabalho pode ser feito em dupla ou individualmente. Recomenda-se utilizar as bibliotecas desenvolvidas nos laboratórios 7 e 8.

## Perguntas

Seguem algumas perguntas a serem respondidas no relatório - de forma geral - depois da codificação:

1.  O que teria que ser mudado no seu código para comportar rótulos com um número arbitrário de caracteres?

2.  O que teria que ser mudado no seu código para lidar com espaçamentos de tamanho qualquer, e não apenas de tamanho 2?

3. O que teria que ser mudado no seu código para lidar com as pseudo-instruções? Por exemplo `&`, `@` e `K`.

4.  O que teria que ser mudado no seu código para comportar a definição
    de externals? E para a definição de entry points?

5.  O que teria que ser mudado no seu código para tratar erros no arquivo lido ? Como símbolos não resolvidos ou uso de instruções inexistentes.

Nota: Além dessas perguntas, deve-se explicar o funcionamento do seu código, para tal pode-se utilizar imagens, trechos de código, etc.

## Entrega

Dois ou mais arquivos devem ser entregues:

1.  **Montador absoluto:** um arquivo em ASM chamado `montador.asm`
    contendo o código que faz a montagem de arquivos ASM.

2.  **Relatório:** um arquivo chamado `relatorio_<NUSP1>_<NUSP2>.pdf` para
    trabalhos realizados em dupla, ou `relatorio_<NUSP>.pdf` para individuais
    contendo os detalhes de como foram realizadas as implementações de cada tópico (ex. resolução de símbolos, tratamento de comentários, conversão de MEM2OP, etc.), além das respostas às perguntas propostas,e outras informações que julgarem úteis.
    O relatório pode conter imagens das execuções de teste. O relatório **deve** ser feito em LaTeX, pessoalmente recomendo a utilização do [Overleaf](https://pt.overleaf.com/).

3.  Outros arquivos que julgar necessário.
