# SED-transporte-carga-2

# Sistema de Transporte de Carga

Este projeto foi desenvolvido para a disciplina de **Sistemas a Eventos Discretos** e modela um sistema de transporte de carga utilizando **Uppaal** para a modelagem de autômatos temporizados.

## Descrição do Projeto

O sistema de transporte de carga consiste em uma via circular composta por **8 seções** e **3 veículos**. O objetivo do projeto é garantir a movimentação dos veículos na via de forma segura, respeitando as restrições de trânsito em cada seção e a necessidade de reabastecimento dos veículos após um número específico de voltas.

### Regras do Sistema

- **Via Circular**: A via é composta por 8 seções numeradas de 1 a 8.
- **Veículos**: Existem 3 veículos no sistema.
  - O **Veículo 1** precisa reabastecer a cada **1 volta completa** na via.
  - O **Veículo 2** precisa reabastecer a cada **2 voltas completas** na via.
  - O **Veículo 3** precisa reabastecer a cada **3 voltas completas** na via.
- **Semáforos**: Entre cada seção existe um semáforo que controla a entrada dos veículos na próxima seção, **exceto entre as seções 2 e 3**.
- **Segurança**: Apenas **um veículo** pode estar em uma seção por vez.
- **Tempo de Deslocamento**: O tempo para deslocar de uma seção para outra é de **10 unidades de tempo**.
- **Operação de Carregamento/Descarregamento**: A cada mudança de seção, o veículo precisa parar para carregar/descarregar por pelo menos **25 unidades de tempo**.
- **Reabastecimento**: Para reabastecer, o veículo deve entrar no estacionamento pela seção 1.

### Propriedades a Serem Satisfeitas

- Em **nenhum momento** deve haver mais de um veículo em uma mesma seção.
- Cada veículo **não deve exceder sua autonomia** de voltas antes de reabastecer.
- O sistema deve ser **livre de deadlocks**, garantindo que todos os veículos continuem a circular de forma adequada.
  
## Estrutura do Autômato

- **Seções**: Cada seção é modelada como um estado no autômato.
- **Semáforos**: Representados por variáveis booleanas que indicam se a seção está livre (`True`) ou ocupada (`False`).
- **Combustível**: Cada veículo tem uma variável que representa seu nível de combustível, que é decrementado a cada seção percorrida. 
  - O combustível é calculado como `8 * N`, onde `N` é o número do veículo.
  - Exemplo: Veículo 1 tem `8` unidades de combustível, Veículo 2 tem `16` e Veículo 3 tem `24`.
 
    ![image](https://github.com/user-attachments/assets/c3753d1e-3993-4448-90ff-75467e1727b3)

## Implementação no Uppaal

A modelagem foi feita no software Uppaal, utilizando autômatos temporizados para cada veículo. A lógica segue a estrutura de:
1. **Estado Inicial**: O veículo começa no estacionamento.
2. **Transição Entre Seções**: A transição para a próxima seção só é permitida se:
   - O veículo tem combustível suficiente.
   - A seção de destino está livre.
   - O semáforo entre a seção atual e a próxima está verde.
3. **Decremento de Combustível**: A cada transição bem-sucedida entre seções, o combustível do veículo é decrementado.
4. **Reabastecimento**: Quando o combustível se esgota, o veículo deve entrar no estacionamento para reabastecer e só então retornar à via.

### Simulação

Na simulação, verificamos:
- A movimentação correta dos veículos entre as seções.
- O respeito aos tempos de deslocamento e carregamento.
- O reabastecimento adequado dos veículos após o número de voltas definido.
- A ausência de deadlocks no sistema.

## Como Rodar o Projeto

1. **Instale o Uppaal**: Baixe e instale o Uppaal em seu sistema a partir do [site oficial](http://www.uppaal.org/).
2. **Abra o Projeto**: Importe o arquivo `.xml` do projeto para o Uppaal.
3. **Simule**: Execute a simulação para visualizar a movimentação dos veículos no sistema e verificar o cumprimento das propriedades especificadas.

## Autores

- **Marcos Vinícius**
- **Vitor Trindade**

Disciplina de **Sistemas a Eventos Discretos** \
Professor: **Dr. Kyller Gorgonio**
