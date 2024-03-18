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
* Como não será utilizado as pseudo-instruções `&` e `@`, deve-se considerar que o endereço da primeira instrução é `0x0000`.

Além disso, considere que o arquivo `.asm` a ser lido está no dispositivo `300`.
Enquanto, o arquivo `.mvn` deve ser escrito no disposivito `301`.

### Glossário

* `<s>`: caracter ASCII espaço.
* Label: rótulo composto por exatamente 2 caracteres ASCII.
* MNEM: mneumônico representando uma das 16 instruções.
* Comments: comentários, iniciados por `<s>;`, com uma quantidade qualquer de caracteres. Mas essa quantidade é sempre par e dentro de um comentário nunca haverá o caracter `\n`.
* Address: Endereço da instrução composto por 4 dígitos hexadecimais codificados em ASCII.
* Instruction: Instrução composta por seu opcode e seu operando, totalizando 4 dígitos hexadecimais codificados em ASCII.

O trabalho pode ser feito em dupla ou individualmente. Recomenda-se utilizar as bibliotecas desenvolvidas nos laboratórios 7 e 8.

### Exemplo

Neste repositório, foram disponibilizados 2 arquivos com a formatação exata da entrada e da saída esperada para o montador absoluto, cujos nomes são: `exemplo_input.asm` e `exemplo_output.mvn`.

## Perguntas

Seguem algumas perguntas a serem respondidas no relatório - em linhas gerais - depois da codificação:

1.  O que teria que ser mudado no seu código para comportar rótulos com um número arbitrário de caracteres?

2.  O que teria que ser mudado no seu código para lidar com espaçamentos de tamanho qualquer, e não apenas de tamanho 2?

3. O que teria que ser mudado no seu código para lidar com as pseudo-instruções? Por exemplo `&`, `@` e `K`.

4.  O que teria que ser mudado no seu código para comportar a definição
    de externals? E para a definição de entry points?

5.  O que teria que ser mudado no seu código para tratar erros no arquivo lido ? Como símbolos não resolvidos ou uso de instruções inexistentes.

6. O que teria que ser mudado no seu código para lidar com valores hexadecimais ?

Nota: Além dessas perguntas, deve-se explicar o funcionamento do seu código, para tal pode-se utilizar imagens, trechos de código, etc.

## Entrega

Dois ou mais arquivos devem ser entregues:

1.  **Montador absoluto:** arquivo(s) ASM utilizados para a codificação do montador, 
    além da versão em MVN chamado `montador.mvn` (gerado pelo `mvn-cli`).

2.  **Relatório:** um arquivo chamado `relatorio_<NUSP1>_<NUSP2>.pdf` para
    trabalhos realizados em dupla, ou `relatorio_<NUSP>.pdf` para individuais
    contendo os detalhes de como foram realizadas as implementações de cada tópico (ex. resolução de símbolos, tratamento de comentários, conversão de MEM2OP, etc.), além das respostas às perguntas propostas,e outras informações que julgarem úteis.
    O relatório pode conter imagens das execuções de teste. O relatório **deve** ser feito em LaTeX, pessoalmente recomendo a utilização do [Overleaf](https://pt.overleaf.com/).

3.  Outros arquivos que julgar necessário.

## Observações Gerais

* O montador absoluto deve ser executado pela MVN com endereço inicial `0x0000`.

* Os arquivos de entrega foram modificados para permitir que os alunos codifiquem o trabalho utilizando 1 ou mais arquivos ASM. Sendo que, o arquivo MVN da entrega é simplesmente o arquivo gerado pelo `mvn-cli`, a partir do(s) arquivo(s) ASM.

* Recomenda-se a utilização de comentários e nomes de rótulos autoexplicativos para facilitar a correção do trabalho.

* Recomenda-se configurar a formatação do seu editor de texto para considerar a tecla `tab` como sendo 2 espaços (`<s>`) e a tecla `enter` como sendo apenas 1 `\n` (LF). No `vscode`, é possível realizar essas modificações no canto direito da barra inferior.

* Uma maneira de conferir a formatação da saída do montador com o arquivo `exemplo_output.mvn` é utilizar o comando `diff <arquivo1> <arquivo2>`. Outra ideia, seria utilizar o próprio sistema de versionamento do git, ou seja sobrescrever o arquivo `exemplo_output.mvn` com a versão gerada pelo seu montador e utilizar o git/github para observar as diferenças.
