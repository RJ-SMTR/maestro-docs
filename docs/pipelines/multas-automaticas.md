# Multas Automáticas

Versão: v1.0

## Definicões

- **Linha**: Conjunto de servicos, usualmente descrito por números, ex: 123, 720.
- **Servico**: Conjunto de itinerários, usualmente descrito pela linha e identificador do servico, ex: 123 RA, 720 PR. As linhas tem servicos normais e específicos, como 'Parador', 'Expresso', 'Noturno', etc.
- **Itinerário**: Trajetos executados por veículos que param em pontos específicos e tem frequência de saída ou frota determinada.
- **Consórcio**: Empresa responsável pela operacao dos itinerários. Usualmente, consórcios operam linhas com exclusividade.
- **Frota determinada**: Número de veículos que deverão operar em uma linha definido pela SMTR
- **Faixa horária**: intervalo de 10 minutos comecando no primeiro minuto da hora, ex: 6:00, 6:10, 6:20. A faixa horária será desconsiderada caso ocorra mais que 2 falhas na captura dos dados de GPS pela SMTR. A captura é executada a cada 1 minuto, portanto, espera-se 8 capturas a cada faixa horária.
- **Frota operante**: Número de veículos distintos em operacão que emitem um sinal de gps em determinada faixa horária. Os veículos considerados em operacão são aqueles que
    - não estão em garagens (ver documentaçåo da pipeline de gps). Veja aqui a lista de garagens consideradas [TODO]
    - [NÃO IMPLEMENTADO] tem o serviço do gps associado ao mesmo trajeto que está sendo realizado no instante da emissão do sinal (ver documentaçåo da pipeline de gps).
    - [NÃO IMPLEMENTADO] não ficaram tiveram velocidade menor que 3km/h por mais que 10 minutos consecutivos.

## Frota operante abaixo da frota determinada

- O Código Disciplinar do Servico Público de Transporte de Passageiros por meio de Ônibus do Município do Rio de Janeiro [1] dispõe sobre as condicões para aplicacão de multas aos consóricios que operarem linhas abaixo da frota determinada no Artigo 17.I. Porém, o regulamento não explicita como operacionalizar a aplicacão dessas multas via gps. Portanto, a SMTR define,neste documento, um conjunto de regras para operacionalizar a aplicacão das multas via gps.
- Segundo o Código de Contuta do SPPO no Artigo 17.I, as condicões para aplicacão da multa abaixo da frota determinada são as seguintes:
     - Se frota determinada é menor ou igual que 5, então ele estará sujeito a multa se a frota operante é menor que a frota determina.
     - Se frota determinada for maior que 5, então ele estará sujeito a multa se:
         - a frota operante for menor que 80% da frota determinada, para dias úteis
         - a frota operante for menor que 50% da frota determinada, para sábados
         - a frota operante for menor que 40% da frota determinada, para domingos
- As regras para operacionalizar a aplicacão das multas via gps definidas pela SMTR
     1. Somente uma multa será aplicada por pico da manhã e da tarde. Portanto, cada linha está sujeita à duas multas por dia. Cada consórcio tem um pico diferente dado a natureza da operacão (ver tabela 1)
     2. Para cada linha e faixa horária será calculada a frota operante. Se frota operante não satistifizer as condicões do artigo XVII, então a linha naquela faixa horária será considerada abaixo da frota determinada.
     3. As multas serão aplicadas para um pico se:
        1. existirem 3 faixas horárias (30 minutos) consecutivas abaixo da frota determinada
        2. existirem 8 faixas horárias (80 minutos) não consecutivas abaixo da frota determinada


Tabela 1: Picos por consórcio

| Consórcio    | Pico Manhã  | Pico Tarde    |
| ------------ | ----------- | ------------- |
| Intersul     | 6:00 - 9:00 | 16:00 - 19:00 |
| Internorte   | 5:30 - 8:30 | 16:00 - 19:00 |
| Transcarioca | 5:30 - 8:30 | 16:00 - 19:00 |
| Santa Cruz   | 5:00 - 8:00 | 17:00 - 20:00 |

Referências:
[1]: https://doweb.rio.rj.gov.br/apifront/portal/edicoes/imprimir_materia/31457/1900