# uPyBodyTempIR-PYBD

Código de interface gráfica para Pyboard-D. Versão mais nova do uPyBodyTempIR para Pyboard-D (uPyBodyTempIR-PYBD_v0.5.py), código produzido para iniciativas contra o [COVID-19](https://gitlab.com/rcolistete/computacaofisica-privado/-/tree/master/uPyBodyTempIR). Tal produção entra nos requisitos propostos pela FAPES, como consta no resumo das atividades de abril ([202004_Atividades](https://github.com/EduardoDestefani/IC-Mag-privado/blob/master/Atividades/202004-12_Atividades_IC_FAPES_especial/202004_Atividades/202004_Atividades.md)).

O resultado, foram quatro versões de códigos funcionais, sendo a v0.5, a mais inteligente, pois utiliza o novo módulo [ulab](https://gitlab.com/rcolistete/micropython-samples/-/blob/master/Pyboard/Firmware/v1.12_with_ulab/ulab_v0.54.0_2020-07-26/Pyboard_D_SF2W/pybd-sf2_ulab_sp_v1.12-662-gf8531fe04_2020-07-26.dfu) e menos linhas. Todas as versões estão disponíveis em; https://gitlab.com/rcolistete/computacaofisica-privado/-/tree/master/uPyBodyTempIR/uPyBodyTempIR-PyboardD



O código principal está na sua quinta versão (v0.5).


## Etapas de Funcionamento

O código funciona de acordo com os seguintes parâmetros; coleta de medidas, armazenamento e processamento dos dados. Isso é feito de acordo com o estímulo escolhido, que no caso, foi pressionar o botão USR do Pyboard-D, simulando o que seria um sensor de proximidade. Daí as etapas são:


#### Ociosidade
Nesta etapa, o microcontrolador (Pyboard-D) espera um estímulo externo que o faça executar a coleta de dados. Nesse caso, ele aguarda que o botão USR seja pressionado. Enquanto isso, ele apresenta uma mensagem "Esperando proximidade ...".


#### Coleta de dados
Nesta etapa, o botão é pressionado, simulando uma pessoa perto, e o microcontrolador começa a coletar as medidas fornecidas da função principal. Todos os valores que estejam no intervalo pré-estabelecido no script serão armazenados em uma lista de 8 valores. Caso esses valores atendam os critérios do intervalo proposto, o microcontrolador parte para a próxima etapa. 

Durante a coleta de dados o microcontrolador apresenta uma mensagem escrita "Carregando ...", junto a um LED verde. Caso a pessoa se afaste durante o processo de coleta de dados, o microcontrolador pede para que a mesma "Se aproxime!" junto a um LED vermelho, se a pessoa afastou-se diversas vezes da zona de medida, um total igual a 8 valores, o Pyboard mostra uma mensagem dizendo "Não há alguém próximo." e pula para a etapa de **Pós processamento**. Isso é feito para evitar um grande desvio padrão na temperatura final na etapa **Processamento de dados**.


#### Processamento de dados
Nesta etapa, o microcontrolador executa uma análise estatística da lista de 8 valores, tirando média e desvio padrão da mesma. Caso cada um dos valores estejam dentro do intervalo da média +/- o desvio padrão, o microcontrolador fornece a medida dizendo "Medida feita!", a temperatura e o resultado (Normal, Febre, Febre Alta e Hipertermia). Caso as medidas não estejam de acordo, ele pede para que a pessoa tente novamente e indica que a mesma pode ter se afastado com uma mensagem "Não há alguém próximo.", dito anteriormente.


#### Pós processamento
Nesta etapa, o microcontrolador já analisou e indicou a temperatura da pessoa, em seguida ele executa um comando de delay (atraso) dizendo "Aguarde ..." e apaga os dados para uma próxima medida.
