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

O trabalho pode ser feito em duplas ou individualmente. Definir escopo
de uso da biblioteca, mensagens de erro coerentes, eventuais limitações
e funcionalidades não comentadas acima fazem parte do trabalho.

### Desafio

Se tudo funcionar até aqui, o próximo passo é desenvolver um
montador relocável. Deve ser adicionada a possibilidade de inserção dos
símbolos `&` e `@` no código origem e o montador deverá gerar os
códigos calculando os nibbles iniciais, de acordo com o visto no teoria.


## Perguntas

Seguem algumas perguntas a serem respondidas depois da codificação:

1.  Os algoritmos propostos podem ser mais eficientes? Como? Se sim, por
    que a forma menos eficiente foi escolhida?

2.  Os códigos escritos podem ser mais eficientes? Como? Se sim, por que
    a forma menos eficiente foi escolhida?

3.  Qual foi a maior dificuldade em implementar o montador?

4.  O que teria que ser mudado no seu código para comportar a definição
    de externals? E para a definição de entry points?

5.  O que aconteceria com a execução do seu código se for fornecido um
    arquivo com um código incorreto? Um código muito grande poderia
    gerar problemas.

## Entrega

Dois ou mais arquivos devem ser entregues:

1.  **Montador absoluto:** um arquivo em MVN chamado `montador.asm`
    contendo o código que faz a montagem de arquivos ASM.

2.  **Relatório:** um arquivo chamado `relatorio_<NUSP1>_<NUSP2>.pdf` para
    trabalhos realizados em dupla, ou `relatorio_<NUSP>.pdf` para individuais
    contendo uma descrição resumida do problema e dos conceitos e uma descrição
    detalhada das etapas de resolução, da estratégia utilizada em cada módulo
    e outras informações que julgarem úteis. O relatório pode conter imagens
    das execuções de teste;

3.  Outros arquivos que julgar necessário.
