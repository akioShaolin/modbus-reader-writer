# Cronologia e proveniência

Os números nos nomes históricos não são números de versão. As datas das fotos e das conversas ancoram os ensaios; as datas na tabela são as de modificação dos arquivos preservados, não dias garantidos de criação ou de teste.

| Data do arquivo | Nome histórico | Cópia sanitizada | O que ficou |
|---|---|---|---|
| 29/09/2025 | `1.esp07_modbus_test/1.esp07_modbus_test.ino` | `primeiro-teste-biblioteca` | Tentativa com `readHreg()` e callback. |
| 30/09/2025 | `2.modbus_manual/2.modbus_manual.ino` | `quadro-rtu-manual` | Quadro FC03 e CRC construídos à mão; direção do RS485 e saídas de depuração separadas. Há chamadas a funções que não estão neste arquivo. |
| 01/10/2025 | `5.escrita_de_reg_limitacao/5.escrita_de_reg_limitacao.ino` | `ensaio-escrita-fc06` | Escrita no setup e leitura depois. |
| 09/10/2025 | `4.requisicao/4.requisicao.ino` | `requisicoes-de-leitura` | Leituras manuais em mais de um dispositivo e endereço. O código aceitava as duas ordens de CRC na recepção; a especificação RTU define byte baixo primeiro. |
| 04/11/2025 | `10.writer_modbus_reserved/10.writer_modbus_reserved.ino` | `rascunho-fila-e-retries` | Fila, códigos de resposta, timeout e retransmissões num ramo maior e incompleto. Ter fila não tornava as esperas não bloqueantes. |
| 10/11/2025 | `12.leitura_reg_pot/12.leitura_reg_pot.ino` | `leitura-potencia-sem-escrita` | Retorno ao ensaio de leitura; chamadas FC06 comentadas no original. |
| 09/03/2026 | `20.leitorModbus/leitorModbus/leitorModbus.ino` | `leitor-web` | Leitura genérica via navegador, usando biblioteca de novo. |

A busca pela biblioteca e a primeira bancada aparecem em 26/09/2025. Em outubro, leituras e escritas foram ensaiadas em equipamento, mas as datas não permitem colocar todas as sessões numa única sequência. Em novembro há dois ramos com propósitos diferentes. Em 09/03/2026, as capturas registram dois resultados para o pedido `ADDR 0x002B COUNT 1`: `21320 / 0x5348` e `0 / 0x0000`. O endereço sozinho não explica a diferença.

## O que mudou nas cópias

- SSID e senha do ponto de acesso foram substituídos por exemplos; o endereço local padrão do AP foi preservado. IDs, endereços de protocolo da instalação e a potência nominal de configuração foram trocados por dados de bancada. O endereço `0x002B` do ensaio CHINT também virou o exemplo do leitor.
- Um comentário com o nome da concessionária e comentários de mapeamento que expunham a configuração ou misturavam referência e offset foram retirados ou substituídos. Código de montagem de quadro, CRC, temporização e fluxos das tentativas foi preservado.
- Os rascunhos `ensaio-escrita-fc06` e `rascunho-fila-e-retries` têm um `#error` de proteção por padrão: não são firmware para instalação. A cópia de leitura de novembro mantém a escrita comentada.
- O README anterior, os sketches originais, o diário retrospectivo e toda a mídia bruta estão sob `archive-original/` na cópia local, com os caminhos relativos originais. Um manifesto SHA-256 no mesmo diretório permite comparar os arquivos. O diretório inteiro fica fora do Git.

## Mídia selecionada

| Arquivo em `docs/media/` | Origem e tratamento |
|---|---|
| `prototipo-ubox.webp` | `20251006-prototipo.jpg`, vista geral do gabinete. |
| `primeiro-teste.webp` | `20250926-teste.jpg`, enquadramento original com os dados da tela ocultados. |
| `objetivo-inicial.webp` | `o-comeco.png`, recorte da pergunta inicial. |
| `descoberta-biblioteca.webp` | `interacao-com-manus-e-descoberta-do-emelianov.png`, recorte da busca de 26/09. |
| `serial-e-debug.webp` | `software-serial.png`, recorte só da mensagem sobre o hardware. |
| `pergunta-sobre-flush.webp` | `pergunta-sobre-o-flush.png`, recorte só da pergunta. |
| `chint-resposta-5348.webp` | `20260309-chint-foxess.jpg`, apenas formulário e resultado. |
| `chint-resposta-0000.webp` | `20260309-chint-generico.jpg`, apenas formulário e resultado. |

Os WebPs não carregam EXIF, GPS, XMP ou IPTC. As conversas ilustram dúvidas do período; a referência para o comportamento do protocolo é a documentação técnica, não as respostas antigas do chat.
