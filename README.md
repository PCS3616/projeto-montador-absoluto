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
* Realizar o apenas tratamento da pseudo-instrução K, além das demais 16 instruções;
* Desconsiderar o uso de _entry_points_ e _externals_;
* Não implementar tratamento de erro, isto é supõe-se que todo arquivo de entrada está corretamente formatado;
* Os arquivos a serem montados terão no máximos 50 linhas de código;
* Os dois formatos possíveis de uma linha do arquivo `.asm` são:
  * `Label`\<s>\<s>`MNEM`\<s>\<s>`Label`\<s>\<s>`Comments`\<s>`\n`
  * `Label`\<s>\<s>`K`\<s>\<s>`/Value`\<s>\<s>`Comments`\<s>`\n`

### Glossário

* `<s>`: caracter ASCII espaço.
* Label: rótulo composto por exatamente 2 caracteres ASCII.
* MNEM: mneumônico representando uma das 16 instruções.
* Value: valor hexadecimal, codificado em ASCII, composto por exatamente 4 dígitos.
* Comments: comentários, iniciados por `<s>;`, com uma quantidade qualquer de caracteres. Mas essa quantidade é sempre par e dentro de um comentário nunca haverá o caracter `\n`.

O trabalho pode ser feito em dupla ou individualmente. Recomenda-se utilizar as bibliotecas desenvolvidas nos laboratórios 7 e 8.

### Desafio: Ainda vai ter?

Se tudo funcionar até aqui,
*depois de remover todas as simplificações que foram adotadas para o montador absoluto*,
o próximo passo é desenvolver um montador relocável. Deve ser adicionada
a possibilidade de inserção dos símbolos `&` e `@` no código origem e o
montador deverá gerar os códigos calculando os nibbles iniciais, de acordo
com o visto no teoria.


## Perguntas

Seguem algumas perguntas a serem respondidas - de forma geral - depois da codificação:

1.  O que teria que ser mudado no seu código para comportar rótulos com um número arbitrário de caracteres?

2.  O que teria que ser mudado no seu código para lidar com espaçamentos de tamanho qualquer, e não apenas de tamanho 2?

3. O que teria que ser mudado no seu código para lidar com outras pseudo-instruções? Por exemplo `&` e `@`.

4.  O que teria que ser mudado no seu código para comportar a definição
    de externals? E para a definição de entry points?

5.  O que teria que ser mudado no seu código para tratar erros no arquivo lido ? Como símbolos não resolvidos ou uso de instruções inexistentes.

## Entrega

Dois ou mais arquivos devem ser entregues:

1.  **Montador absoluto:** um arquivo em ASM chamado `montador.asm`
    contendo o código que faz a montagem de arquivos ASM.

2.  **Relatório:** um arquivo chamado `relatorio_<NUSP1>_<NUSP2>.pdf` para
    trabalhos realizados em dupla, ou `relatorio_<NUSP>.pdf` para individuais
    contendo uma descrição resumida do problema e dos conceitos e uma descrição
    detalhada das etapas de resolução, da estratégia utilizada em cada módulo
    e outras informações que julgarem úteis. O relatório pode conter imagens
    das execuções de teste;

3.  Outros arquivos que julgar necessário.
