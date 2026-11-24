# Modbus Reader / Writer

Eu queria programar a injeção de energia por horário. Para chegar lá, reaproveitei um SolarView uBox com ESP-07 e RS485 e comecei pela pergunta que cabia na bancada: como faço para ler um registrador?

O período registrado vai de **26/09/2025 a 09/03/2026**. Este acervo reúne os sketches que guardei quando um teste respondia a uma pergunta e abria outra. Eles não são versões de uma biblioteca, tampouco um controlador de exportação pronto para instalar.

## Os checkpoints

| Sketch | O que eu estava investigando |
|---|---|
| [primeiro-teste-biblioteca](sketches/primeiro-teste-biblioteca/) | Primeira tentativa com `ModbusRTU.h`, `readHreg()` e callback. Nesse ponto, depuração e Modbus ainda dividiam a mesma UART. |
| [quadro-rtu-manual](sketches/quadro-rtu-manual/) | Montagem byte a byte de FC03 e cálculo do CRC16. A UART0 ficou no RS485 e a SoftwareSerial passou a levar os logs ao PC. O arquivo ficou com chamadas auxiliares que não acompanham a cópia. |
| [ensaio-escrita-fc06](sketches/ensaio-escrita-fc06/) | Ensaio de escrita única no início do sketch, seguido de leituras. A escrita e a releitura passaram a responder perguntas diferentes. |
| [requisicoes-de-leitura](sketches/requisicoes-de-leitura/) | Leituras em mais de um endereço e dispositivo, recepção com timeout e margem para passar de TX de volta para RX. |
| [rascunho-fila-e-retries](sketches/rascunho-fila-e-retries/) | Ramo incompleto: filas, códigos de erro, espera de resposta e retransmissões. Começava a ganhar responsabilidades de um controlador maior. |
| [leitura-potencia-sem-escrita](sketches/leitura-potencia-sem-escrita/) | Variação de outro ensaio: a rotina FC06 permanece no arquivo, mas as chamadas de escrita estão comentadas no original. |
| [leitor-web](sketches/leitor-web/) | Retorno à biblioteca com um leitor HTTP local: escolher endereço e quantidade e receber os valores brutos em decimal e hexadecimal por WebSocket. |

No Modbus RTU desses testes, o cliente fazia um pedido por vez no barramento RS485 e o dispositivo consultado respondia pelo seu ID. O código de função distinguia leitura de escrita. No meio do caminho, o que parecia só uma chamada de biblioteca virou um quadro com endereço, quantidade ou valor e CRC. O tempo para liberar o transceptor depois de enviar o pedido também passou a fazer parte do diagnóstico.

O leitor web fechou esta etapa. Em 9 de março, dois medidores CHINT responderam à mesma leitura de `0x002B` com valores diferentes. Entender a razão ficou para outra investigação. A experiência daqui ajudou a separar problemas maiores em outros projetos Modbus.

## Como ler este acervo

- A [cronologia](docs/cronologia.md) relaciona os nomes originais, as datas dos arquivos e os ajustes feitos para compartilhar as cópias.
- As cópias têm IDs e endereços de bancada ilustrativos, não reproduzem o mapa nem a configuração da instalação e não são adequadas para uso em campo. Os dois rascunhos com escrita ativa têm um bloqueio de compilação por padrão. As lacunas e limitações históricas não foram reimplementadas.
- `docs/media/` guarda somente cópias revisadas, sem metadados pessoais. O vídeo, os dumps, as capturas não selecionadas e os arquivos brutos não fazem parte da coleção pública. Os originais permanecem no acervo local, excluídos por `.gitignore`.
- Referências: [Modbus Organization](https://www.modbus.org/modbus-specifications), [biblioteca modbus-esp8266](https://github.com/emelianov/modbus-esp8266) e [core Arduino para ESP8266](https://github.com/esp8266/Arduino).
