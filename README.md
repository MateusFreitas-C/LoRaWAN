# Introdução
<p> A Internet das Coisas tornou-se importante na forma como gerimos o mundo que nos rodeia. As soluções IoT sem fio de curto alcance geralmente dependem de uma conexão Bluetooth ou Wi-Fi.
Soluções de longo alcance, como rastreamento de ativos ou monitoramento do uso de serviços públicos, geralmente dependem de redes de longa distância de baixo consumo de energia, como LoRaWAN.</p>

<p>A partir do momento em que, devido ao aumento dos dispositivos de IoT, foi dada a necessidade de uma rede que consuma pouca energia, uma comunicação de longo alcance e baixo custo para conectar estes dispositivos. A LPWAN (Low Power Wide Area Network) preenche esses requisitos, porém com menor taxa de transmissão de dados e latência.</p>


## LoRaWAN®
<p>LoRaWAN® é um protocolo de software que utiliza a camada física do LoRa®. Como será mostrado abaixo a arquitetura básica de uma rede LoRaWAN® é composta por: dispositivos que contém sensores LoRaWAN®, Gateways, Servidor de Rede e Servidores de Aplicação.</p>

![Image](https://github.com/MateusFreitas-C/LoRaWAN/blob/main/img/architeture.jpeg)

### 1. Características do LoRaWAN®

* Cobre longas distâncias de transmissão, podendo chegar entra 2 e 5 Km em áreas urbanas e até 10 Km em campo aberto.
* Baixo consumo de energia o que aumenta a vida de dispositivos alimentados por baterias.
* Baixa taxa de transmissão (0.3 - 50 Kpbs)
* Utiliza frequências abaixo de 1 Ghz
* O padrão LoRaWAN® define a estrutura do pacote de dados, define como os pacotes serão processados no servidor e como serão encriptados.
* LoRaWAN® utiliza uma topologia de rede em estrela onde a topologia em estrela é empregada, mas as mensagens são recebidas por todas as estações base no intervalo.

### 2. Dispositivos
<p>Os dispositivos LoRaWAN® pode enviar (uplink) e receber (downlink) pacotes de dados de e para gateways.</p>

<p>Os dispositivos LoRaWAN® são divididos em diferentes classes.</p>

#### 2.1 Classe A
* Todos os dispositivos devem ser compatíveis com essa classe
* Envia dados a qualquer momento
* Só recebe dados após o envio de um uplink.
* O dispositivo sempre inicia a comunicação.
* É o modo de operação mais eficiente energicamente.
* O dispositivo pode entrar em sono profundo após a transmissão.

#### 2.2 Classe B
* Os dispositivos podem receber downlinks em janelas especificadas de tempo
* Devido a isso consome mais energia que a Classe A

#### 2.3 Classe C
* Pode receber mensagens a qualquer momento
* Dispositivo está sempre ouvindo e esperando downlinks
* Consome mais energia

##### Observação: Não há emparelhamento entre dispositivos e Gateways.

### 3. Network Server
* É responsável pela conexão com os gateways
* Responsável pela escolha da classe dos dispositivos
* Responsável pela escolha de parâmetros de radio dos dispositivos
* Identifica os dispositivos
* Mantém uma fila de downlinks
* Seleciona o gateway que enviará o downlink para o dispositivo baseado no RSSI e SNR.
* Decodifica pacotes recebidos de gateways conectados e codifica pacotes destinados aos nós conectados a eles.
* Se várias cópias do mesmo pacote forem recebidas por meio de vários gateways, o servidor de rede determinará qual mensagem manter.

### 4. Manipulando Taxa de Dados
<p>Quando se fala em manipulação de taxa de dados existem 3 fatores primordiais: TX, Spreading Factor e Bandwidth</p>

* TX ou Potência de Transmissão é um tipo de compensação, uma TX maior resulta em menor consumo de energia e menor alcance de sinal e uma TX maior, maior o alcance e o consumo.
* A taxa de dados em si é uma combinação entre Bandwidth e Spreading Factor. Essa combinação determina quão rápido os dados serão transmitidos.
* Se a taxa de dados for aumentada (aumentando a bandwidth ou diminuindo o spreading factor) é possível transmitir o mesmo número de bytes em menos tempo.

<p>Aumentando a taxa de dados, ocasionalmente, será possível enviar um pacote maior de dados. No entando, quanto maior o pacote, mais tempo o pacote fica no ar, ou seja, mais tempo para
ser transmitido, podendo atingir o tempo máximo de um pacote no ar e um dispositivo consome mais energia quando sua transmissão passa mais tempo no ar.</p>


### 5. Gateways

<p>As estações base LoRaWAN® são chamadas de gateways e são conectados a um servidor de rede por meio de um backhaul de maior taxa de transferência. Os gateways encaminham o pacote recebido para o servidor de rede junto com os metadados, como horário de chegada, indicador de intensidade de sinal (RSSI) e a relação sinal/ruído SNR.</p>

<p>Quando um pacote é enviado, ele é recebido por todos os gateways que estão ao alcance. Na chegada dos pacotes os gateways possuem um relógio sincronizado com GPS, registram o timestamp de chegada de cada sinal.</p>

<p>Quando pelo menos 3 gateways recebem um mesmo pacote, é possível calcular a posição do dispositivo baseado nos metadados do pacote. Quantos mais gateways recebe o pacote, mais precisa a localização.</p>
