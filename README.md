# BIMaster_TCC
Repositorio criado para o TCC da Pós-Graduação

<!-- antes de enviar a versão final, solicitamos que todos os comentários, colocados para orientação ao aluno, sejam removidos do arquivo -->

# Análise de radiografias utilizando Redes Neurais para auxílio no diagnóstico de pneumunia.

#### Aluno: [Walner de Assis Passos](https://github.com/Walner-DS/BIMaster_TCC).
#### Orientadora: [Evelyn Conceição Santos Batista](https://github.com/evysb).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](https://github.com/Walner-DS/BIMaster_TCC/modelo_auxilio_diagnostico_pneumunia.py).

---

### Resumo

O trabalho foi desenvolvido para classificar imagens de radiografias de tórax utilizando aprendizagem profunda, com o objetivo de auxiliar no diagnóstico de pneumonia, classificando as imagens em três categorias, “Normal”, “Pneumonia Bacteriana” e “Pneumonia Viral”.

Foram utilizados modelos de redes neurais convulsionais com a técnica de Transfer Learning, excluindo a camada de topo das redes e definindo uma camada FC que atenda o caso.

Foram analisadas as redes VGG19, VGG16, ResNet152V2, MobileNetV3Large, IbceotionV3 e DenseNet201 com uma configuração padrão e selecionada as redes com melhor desempenho para refinamento dos parâmetros do modelo, tendo como resultado:

![image](https://github.com/user-attachments/assets/bf28377e-549f-416c-9512-83258ded9784)
![image](https://github.com/user-attachments/assets/ff003dc1-dd80-4b8b-8115-ba87bcef7ea6)

### Summary

The work was developed to classify chest X-ray images using deep learning, with the aim of assisting in the diagnosis of pneumonia. The model classifies images into three categories, “Normal”, “Bacterial Pneumonia” and “Viral Pneumonia”.

Convulsive neural network models were used using the Transfer Learning technique, excluding the top layer of the networks and defining an FCC layer.

The VGG19, VGG16, ResNet152V2, MobileNetV3Large, IbceotionV3 and DenseNet201 networks were analyzed with a standard configuration and the DenseNet201 network was selected, the network with the best performance for refining the model parameters, resulting in:

![image](https://github.com/user-attachments/assets/bf28377e-549f-416c-9512-83258ded9784)
![image](https://github.com/user-attachments/assets/4dd41dca-07a9-4da1-9f88-819167d79339)


### 1. Introdução

O crescente uso da IA na área médica, proporciona oportunidades e desafios para o meio acadêmico e científico para criação de modelos e sistemas que facilitem a análise de doenças e diagnósticos cada vez mais precisos, trazendo uma segurança e brevidade no início do tratamento.
Este trabalho tem como objetivo ajudar neste processo, auxiliando no diagnóstico de Pneumonia através da análise de imagens de radiografia de Tórax de pacientes suspeitos de contaminação seja viral ou bacteriana.


### 2. Modelagem

>**2.1.	Base de Dados:**
   
>> Foi utilizada uma base de dados com 1650 imagens disponibilizadas na base de dados do kaggle com a seguinte distribuição:

>>>![image](https://github.com/user-attachments/assets/c685e526-7771-4697-aa68-c684b94e9467)

>2.2.	Pré-processamento:

>> As imagens foram padronizadas para um formato 244 x 244 e transformação de monocromática para RGB atribuindo coloração proporcional aos valores de intensidade nas variações de preto e branco.

>>>![image](https://github.com/user-attachments/assets/24de6c43-a76c-4da0-83fe-50138756e430)

>2.3. Construção da Rede:

>> Inicialmente utilizamos a rede VGG16 com a última camada desabilitada,  pesos da “imagenet” , Adam como otimizador, "binary_crossentropy" como função de perda e acurácia como métrica de validação.
 
>> A última camada, FCC, foi definida com as seguintes camadas:
>>> . 01 camada AveragePooling2D;
>>> . 01 Flatten;
>>> . 01 Dense com 64 neurônio de saída e “relu” como função de ativação;
>>> . 01 Dropout de 0.5
>>> . 01 Dense com 03 neurônio de saída e “softmax” como função de ativação;

> 2.3. Treinamento:
> 
>> O treinamento inicial foi realizado com as seguintes configurações para o modelo:
> 
>>> . 100 épocas com 86 etapas cada.
> 
>>> . learning_rate = 1e-3
> 
>>> . weight_decay = 1e-3/100 (número de épocas)
>>>
>> Após a realização de testes, treinamentos e ajustes definimos a seguinte configuração para o modelo:

>> A última camada, FCC, foi definida com a seguinte estrutura:
>> 
>>> . 01 camada AveragePooling2D;
>>> 
>>> . 01 Flatten;
>>> 
>>> . 01 Dense com 256 neurônio de saída e “relu” como função de ativação;
>>> 
>>> . 01 Dense com 128 neurônio de saída e “relu” como função de ativação;
>>> 
>>> . 01 Dense com 64 neurônio de saída e “relu” como função de ativação;
>>> 
>>> . 01 Dense com 03 neurônio de saída e “softmax” como função de ativação;
>>> 
>> Como os seguintes parâmetro par o mmodelo:
>> 
>>> . 20 épocas com 26 etapas cada.
> 
>>> . learning_rate = 1e-3
> 
>>> . weight_decay = 1e-3/26 (número de épocas)

> 2.4. Rede testadas
> > Definida o modelo de melhor resultado, realizamos testes com as seguintes redes:
> > > . VGG19;
> > > 
> > > . ResNet152V2;
> > > 
> > > . MobileNetV3Large;
> > > 
> > > . IbceotionV3;
> > > 
> > > . DenseNet201

### 3. Resultados

#### VGG16:

>> ![image](https://github.com/user-attachments/assets/1b97b653-6046-446a-8a5b-637bd8bb3fee)
>> ![image](https://github.com/user-attachments/assets/772951fb-55b8-49b6-8d31-9fbaf932ecb7)

#### ResNet152V2:

>> ![image](https://github.com/user-attachments/assets/d680ae14-6c2b-4a12-a4b1-196c2ce6dbbf)
>> ![image](https://github.com/user-attachments/assets/e0731839-01d7-42d8-a86b-fc732a03bb20)

#### MobileNetV3Large:

>> ![image](https://github.com/user-attachments/assets/fa6fa0d9-a854-4992-a66e-0fba92345ec4)
>> ![image](https://github.com/user-attachments/assets/7f17a89c-2488-45ff-8345-78da955691ef)

#### InceptionV3:

>> ![image](https://github.com/user-attachments/assets/2a31da45-c93d-47bd-82f9-b8cbfba24cbb)
>> ![image](https://github.com/user-attachments/assets/d4e2afe8-ffcc-48c9-a728-e896e82b0a6f)

#### VGG19:

>> ![image](https://github.com/user-attachments/assets/a3f28293-bc15-44dd-b265-b443f5b7bb75)
>> ![image](https://github.com/user-attachments/assets/fd004482-9a0c-46a8-b120-b851cf8e6686)

#### DenseNet201:

>> ![image](https://github.com/user-attachments/assets/56c1859f-a4c9-4837-b6b6-2dc752a4a475)
>> ![image](https://github.com/user-attachments/assets/6f509340-d0ea-4b5d-be9a-0ef0f764a728)


### 4. Conclusões
>Entre as redes testadas podemos destacar os resultados obtidos pela ResNet152V2 e pela DenseNet201 listados abaixo:

>> #### ResNet152V2:

>>> ![image](https://github.com/user-attachments/assets/d680ae14-6c2b-4a12-a4b1-196c2ce6dbbf)
>>> ![image](https://github.com/user-attachments/assets/e0731839-01d7-42d8-a86b-fc732a03bb20)

>> #### DenseNet201:

>>> ![image](https://github.com/user-attachments/assets/56c1859f-a4c9-4837-b6b6-2dc752a4a475)
>>>![image](https://github.com/user-attachments/assets/6f509340-d0ea-4b5d-be9a-0ef0f764a728)

Com destaque do DenseNet201 por ter conseguido prever corretamente todos os casos de Pneumonia, zerando os resultados “Falsos Negativos”, contribuindo significativamente com a triagem dos pacientes. Porém, apresentou uma baixa taxa de acerto na classificação de “Normal”, com grandes números de Falsos Positivos, principalmente para o tipo Viral.

Com os resultados obtidos, fica claro a possibilidade de utilização do modelo no auxílio ao diagnóstico de Pneumonia através da análise de imagens de radiografia de tórax.


----

Matrícula: 201.190.005

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*


