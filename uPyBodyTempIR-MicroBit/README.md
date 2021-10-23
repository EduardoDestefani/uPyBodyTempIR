# uPyBodyTempIR-MicroBit

Pseudocódigo da interface gráfica do BBC Micro:bit. O **módulo statistics não é utilizado** devido a **pouca memória** do BBC Micro:bit. Código produzido para iniciativas contra o [COVID-19](https://gitlab.com/rcolistete/computacaofisica-privado/-/tree/master/uPyBodyTempIR). 

Tal produção entra nos requisitos propostos pela FAPES, como consta no resumo das atividades de abril ([202004_Atividades](https://github.com/EduardoDestefani/IC-Mag-privado/blob/master/Atividades/202004-12_Atividades_IC_FAPES_especial/202004_Atividades/202004_Atividades.md)).

O código principal está na sétima versão (v0.7).

## Etapas de Funcionamento

O código funciona de acordo com os seguintes parâmetros; coleta de medidas, armazenamento e processamento dos dados. Isso é feito de acordo com o estímulo escolhido, que no caso, foi pressionar o botão USR do Pyboard-D, simulando o que seria um sensor de proximidade. Daí as etapas são:

#### Ociosidade
Nesta etapa, o microcontrolador (BBC Micro:bit) espera um estímulo externo que o faça executar a coleta de dados. Nesse caso, ele aguarda que ele seja inclinado com a tela apontada para cima. Feito isso, ele apresenta um "smile" (":)") como resposta.

#### Coleta de dados
Nesta etapa, ele é inclinado com a tela apontada para cima, simulando uma pessoa perto, e o microcontrolador começa a coletar as medidas fornecidas da função principal. Todos os valores que estejam no intervalo pré-estabelecido no script serão armazenados em uma lista de 8 valores. Caso esses valores atendam os critérios do intervalo proposto, o microcontrolador parte para a próxima etapa. Durante a coleta de dados o microcontrolador exibe um relógio na tela de LEDs. Caso a pessoa se afaste durante o processo de coleta de dados, o microcontrolador exibe uma face "sad" (":(") na tela.


#### Processamento de dados
Nesta etapa, o microcontrolador executa uma análise estatística da lista de 8 valores, tirando média e desvio padrão da mesma. Caso cada um dos valores estejam dentro do intervalo da média +/- o desvio padrão, o microcontrolador fornece a medida após uma imagem de "diamond". A temperatura e o resultado (Normal, Febre, Febre Alta e Hipertermia) são exibidos na tela.

#### Pós processamento
Nesta etapa, o microcontrolador já analisou e indicou a temperatura da pessoa, em seguida ele executa um comando de delay (atraso) dizendo "Se afaste." e apaga os dados para uma próxima medida.


Integrantes; Daniel, Diego, Eduardo Destefani (líder), Luis Felipe Viana, Nélio, Pedro Henrique, Thiago Ferreira.
