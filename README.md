README - Modelo de Dados Oficina Mecânica

Objetivo:
Este projeto representa o modelo conceitual e lógico de um sistema de controle e gerenciamento de ordens de serviço em uma oficina mecânica. 
O modelo foi desenvolvido para ser implementado no MySQL Workbench.

------------------------------------------------------------
Estrutura Geral
------------------------------------------------------------
O sistema é composto por nove entidades principais:

1. Cliente
   - Armazena dados dos clientes da oficina.
   - Atributos: idCliente, Código, Nome, Endereço, Telefone.
   - Relacionamento: Um cliente pode possuir vários veículos (1:N).

2. Veículo
   - Representa os veículos trazidos pelos clientes.
   - Atributos: idVeículo, Placa, Modelo, Ano, Marca.
   - Relacionamento: Cada veículo pertence a um cliente e pode gerar várias ordens de serviço (1:N).

3. Ordem de Serviço
   - Registra os serviços e peças utilizados em cada atendimento.
   - Atributos: idOrdemDeServiço, Número, Data de emissão, Valor total, Status, Autorização do serviço, Data de conclusão.
   - Relacionamentos:
     - Associada a um veículo (N:1).
     - Executada por uma equipe (N:1).
     - Relacionada a vários serviços e peças (N:M).

4. Equipe
   - Agrupa os mecânicos responsáveis pela execução das ordens de serviço.
   - Atributos: idEquipe, Código, Nome da equipe.
   - Relacionamento: Uma equipe é composta por vários mecânicos (1:N) e executa várias ordens de serviço (1:N).

5. Mecânico
   - Representa os profissionais que realizam os serviços.
   - Atributos: idMecânico, Código, Nome, Endereço, Especialidade.
   - Relacionamento: Cada mecânico pertence a uma equipe (N:1).

6. Serviço
   - Define os tipos de serviços disponíveis na oficina.
   - Atributos: idServiço, Código, Descrição, Valor.
   - Relacionamento: Associado à Ordem de Serviço por meio da tabela intermediária "Serviço a ser realizado" (N:M).

7. Serviço a ser realizado
   - Tabela de associação entre Ordem de Serviço e Serviço.
   - Atributos: OrdemDeServiço_id, Serviço_id.
   - Relacionamento: Permite que uma OS tenha múltiplos serviços e um serviço esteja presente em várias OS.

8. Peça
   - Representa as peças utilizadas nos reparos.
   - Atributos: idPeça, Código, Descrição, Valor unitário.
   - Relacionamento: Associada à Ordem de Serviço por meio da tabela intermediária "Peças trocadas" (N:M).

9. Peças trocadas
   - Tabela de associação entre Ordem de Serviço e Peça.
   - Atributos: OrdemDeServiço_id, Peça_id.
   - Relacionamento: Permite que uma OS tenha várias peças e uma peça possa ser usada em diferentes OS.

------------------------------------------------------------
Resumo dos Relacionamentos
------------------------------------------------------------
- Cliente → Veículo: 1:N
- Veículo → Ordem de Serviço: 1:N
- Ordem de Serviço → Equipe: N:1
- Equipe → Mecânico: 1:N
- Ordem de Serviço → Serviço: N:M
- Ordem de Serviço → Peça: N:M

------------------------------------------------------------
Observações Técnicas
------------------------------------------------------------
- O campo "Autorização do serviço" indica se o cliente aprovou a execução (valor binário).
- O "Valor total" da OS é calculado pela soma dos serviços e peças associados.
- As tabelas intermediárias ("Serviço a ser realizado" e "Peças trocadas") garantem a integridade dos relacionamentos N:M.
- Todas as chaves primárias são do tipo INT e as estrangeiras seguem o padrão idEntidade.
