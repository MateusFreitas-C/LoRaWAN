# Introdução
<p> A Internet das Coisas tornou-se importante na forma como gerimos o mundo que nos rodeia. As soluções IoT sem fio de curto alcance geralmente dependem de uma conexão Bluetooth ou Wi-Fi.
Soluções de longo alcance, como rastreamento de ativos ou monitoramento do uso de serviços públicos, geralmente dependem de redes de longa distância de baixo consumo de energia, como LoRaWAN.</p>

<p>Em todos esses casos, para que os dispositivos funcionem, eles precisam transferir dados, no entanto, existem muitos desafios quando se trata de transferir dados, como por exemplo a conectiviade e o consumo de energia.</p>

<p>Pensando nesses desafios a comunicação por redes LPWAN (Low Power Wide Area Network) tem ganhado fama por propor soluções para resolver esses desafios. Protocolos como SigFox NB-IoT e LoRa®
fazem parte das LPWANs.</p>


## LoRaWAN®
<p>LoRaWAN® é um protocolo de software que utiliza a camada física do LoRa®. Como será mostrado abaixo a arquitetura básica de uma rede LoRaWAN® é composta por: dispositivos que contém sensores LoRaWAN®, Gateways, Servidor de Rede e Servidores de Aplicação.</p>

![Image](https://github.com/MateusFreitas-C/LoRaWAN/blob/main/img/architeture.jpeg)

### 1. Características do LoRaWAN®

* Cobre longas distâncias de transmissão, podendo chegar entra 2 e 5 Km em áreas urbanas e até 10 Km em campo aberto.
* Baixo consumo de energia o que aumenta a vida de dispositivos alimentados por baterias.
* Baixa taxa de transmissão (0.3 - 50 Kpbs)
* Utiliza frequências abaixo de 1 Ghz
* O padrão LoRaWAN define a estrutura do pacote de dados, define como os pacotes serão processados no servidor e como serão encriptados.

### 2. Dispositivos
<p>Os dispositivos LoRaWAN® pode enviar (uplink) e receber (downlink) pacotes de dados de e para gateways.</p>

<p>Os dispositivos LoRaWAN são divididos em diferentes classes.</p>

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

#### Classe C
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

### 4. Manipulando Taxa de Dados
<p>Quando se fala em manipulação de taxa de dados existem 3 fatores primordiais: TX, Spreading Factor e Bandwidth</p>

* TX ou Potência de Transmissão é um tipo de compensação, uma TX maior resulta em menor consumo de energia e menor alcance de sinal e uma TX maior, maior o alcance e o consumo.
* A taxa de dados em si é uma combinação entre Bandwidth e Spreading Factor. Essa combinação determina quão rápido os dados serão transmitidos.
* Se a taxa de dados for aumentada (aumentando a bandwidth ou diminuindo o spreading factor) é possível transmitir o mesmo número de bytes em menos tempo.

<p>Aumentando a taxa de dados, ocasionalmente, será possível enviar um pacote maior de dados. No entando, quanto maior o pacote, mais tempo o pacote fica no ar, ou seja, mais tempo para
ser transmitido, podendo atingir o tempo máximo de um pacote no ar e um dispositivo consome mais energia quando sua transmissão passa mais tempo no ar.</p>
