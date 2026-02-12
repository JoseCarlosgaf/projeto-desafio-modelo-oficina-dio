# projeto-desafio-modelo-oficina-dio
Cria o esquema conceitual para o contexto de oficina com base na narrativa fornecida.

Este projeto apresenta a modelagem conceitual de um sistema de controle e gerenciamento de ordens de serviço (OS) para uma oficina mecânica com o objetivo de estruturar, a partir da narrativa fornecida, todas as entidades, atributos e relacionamentos necessários para representar o funcionamento do sistema de forma consistente e normalizada.

O modelo foi desenvolvido utilizando MySQL Workbench para construção do Diagrama Entidade-Relacionamento (DER).

Objetivo é permitir o controle de clientes e seus veículos, equipes de mecânicos, execução de ordem de serviço, serviços realizados, peças utilizadas, autorização do cliente e cálculo do valor da OS.

Estruturas:
Cliente: idCliente, Nome e Cpf - Um cliente pode possuir vários veículos
Veículo: idVeiculo. Nome, Modelo, Marca, Cor, Placa, Cliente_IdCliente | Relacionamento Cliente 1-N Veículo | Um veículo pode gerar várias OS
Equipe: idEquipe, NomeEquipe - Uma equipe é responsável por executar ordens de serviço e é compota por vários mecânicos
Mecânico: idMecanico, Codigo, Nome, Endereço, Especialidade, Equipe_idEquipe | Relacionamento Equipe 1-N Mecânico
OS: idOrdemServiço, Numero, DataEmissao, DataConclusao, Status, Tipo, ValorTotal, autorizado, data_autorizacao, Veiculo_idVeiculo, Equipe_idEquipe | Relacionamento Veiculo 1-N OrdemServico, Equipe 1-N OrdemServico
* o Campo ValorTotal representa a soma dos valores dos serviços e das peças utilizadas na OS
* o campo autorizado indica se o cliente aprovou a execução do serviço, em qual estágio do serviço estamos.
Serviço: idSevico, DescricaoServico, Valos_mao_obra | OrdemServico N-N Servico, OrdemServico_has_Servico (tabela associativa)
Peça: idPeca, NomePeca, Tipo, valor | Relacionamento OrdemServico N-N Peça | OrdemServico_tem_Peca (tabela associativa)'

Equipe vinculada à Ordem de Serviço
Embora a narrativa mencione que o veículo é designado a uma equipe, optou-se por vincular a equipe à Ordem de Serviço, pois:
Um mesmo veículo pode ser atendido por equipes diferentes em momentos distintos, a Ordem de Serviço representa o evento operacional e essa decisão torna o modelo mais flexível e realista.

ValorTotal na Ordem de Serviço
O campo ValorTotal é armazenado para fins de controle financeiro, embora possa ser derivado da soma: Serviços executados e Peca 

Uso de tabelas associativas
Foram criadas tabelas intermediárias para evitar redundâncias para representar relacionamentos N:N: OrdemServico_has_Servico e OrdemServico_tem_Peca

O esquema foi estruturado respeitando princípios de normalização: Sem redundância de atributos descritivos, chaves primárias bem definidas, chaves estrangeiras representando relacionamentos e separação adequada entre entidades e eventos

Ferramentas: MySQL Workbench e Modelagem Entidade-Relacionamento (DER)
