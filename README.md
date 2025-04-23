# mackenzie_IoT

Projeto de um sistema de irrigação inteligente e automatizado que utiliza sensores de umidade do solo para monitoramento contínuo e atuadores para controlar uma bomba d'água. A comunicação entre os dispositivos é feita via protocolo MQTT, permitindo transmissão eficiente e remota de dados para um painel de supervisão. Essa abordagem visa otimizar o uso da água, reduzir o desperdício e contribuir para os Objetivos de Desenvolvimento Sustentável (ODS 6) – Água Potável e Saneamento – ao promover práticas mais sustentáveis na agricultura e gestão hídrica, com impacto positivo na conservação de recursos e economia de água.

O sistema de irrigação inteligente é um protótipo baseado em IoT que realiza a leitura da umidade do solo usando um sensor FC-28. A cada 3 segundos, o microcontrolador ESP8266 lê os dados do sensor e, conforme o valor, decide se deve ligar ou não a bomba de água, acionada via relé.

O controle é feito automaticamente com base em faixas de umidade predefinidas e também pode ser realizado manualmente, remotamente, por meio de um painel de controle na plataforma Adafruit IO, que utiliza o protocolo MQTT. A solução é ideal para pequenas hortas, jardins ou cultivos urbanos, promovendo uso eficiente da água e contribuindo para o ODS 6 (Água Potável e Saneamento).

Componentes utilizados:

- Microcontrolador: ESP8266 NodeMCU — controla o sistema, faz leitura do sensor, ativa o relé e publica/subscreve mensagens MQTT.
- Sensor: FC-28 (sensor de umidade do solo) — mede a umidade do solo através de variações capacitivas.
- Relé 3V: Aciona a bomba de irrigação ao receber sinal lógico do ESP8266.
- Bomba de água 12V: Utilizada para irrigação automatizada.
- Fonte de alimentação 12V: Alimenta a bomba e a placa ESP8266 (via placa reguladora).
- Protoboard: Montagem temporária do circuito.
- Jumpers: Conexão dos componentes sem solda.
- Placa reguladora de tensão (3.3V / 5V): Converte 12V para alimentar ESP8266 e sensores.

Desenvolvimento e configurações:

- O circuito é montado sobre protoboard.
- Portas ESP8266 com sensor FC-28:
3V3 -	VCC
GND	- GND
A0	- AO

- Portas ESP8266 com relé:
3V3 -	VCC
GND	- GND
D1  - NI
   
- Conexão da bomba: fio negativo direto na fonte, fio positivo ligado ao terminal NO (Normally Open) do relé, e COM no positivo da fonte.

Interface com o usuário: Dashboard do Adafruit IO com gráficos e botões de controle (documento Adafruit.pdf com detalhes dos procedimentos de configuração do dashboard).
Protocolo de comunicação: MQTT (Message Queuing Telemetry Transport).
Publicação de dados: umidade do solo → feed MQTT “umidade-solo”.
Subscrição de comandos: estado da bomba → feed “estado-bomba”.

Documento CODE_UPLOAD.pdf detalha passo a passo o processo de instalação, configuração e uso do software Arduino IDE para a conexão do computador com a placa ESP8266 e o upload do código.
Módulos e bibliotecas usados:
PubSubClient: Biblioteca usada no Arduino IDE para comunicação MQTT.
WiFi.h: Para conectar o ESP8266 à rede Wi-Fi.

Fluxo de comunicação:
Sensor FC-28 → ESP8266 → MQTT Broker (Adafruit IO) → Interface Web.
Interface Web → Broker MQTT → ESP8266 → Relé → Bomba de Água.

O projeto implementa comunicação via internet usando TCP/IP, conectando-se à rede Wi-Fi local. Toda a troca de informações entre o microcontrolador e o painel de monitoramento ocorre por MQTT, com o ESP8266 operando como publisher e subscriber de tópicos no broker da Adafruit IO.

Através dessa arquitetura, o sistema permite:

- Controle remoto da bomba de água.
- Monitoramento em tempo real da umidade do solo.
- Respostas rápidas (< 600 ms) entre comandos e ações.

  
