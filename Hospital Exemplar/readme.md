# **🏨 HOSPITAL EXEMPLAR**

### **📌 Objetivo:** Criar uma modelagem de banco de dados para o gerenciamento hospitalar. A estrutura foi projetada para armazenar informações sobre médicos, pacientes, consultas, convênios, receitas médicas e outros dados relevantes.

---

**Status da Atividade:**

✅Parte 1 | ✅ Parte 2 | ⏳ Parte 3 | ⏳ Parte 4 | ⏳ Parte 5 [Em Andamento]

---

### ✅ PARTE 1 - Mãos a Obra

**Analise a seguinte descrição e extraia dela os requisitos para o banco de dados em um diagrama, fluxograma ou afins: O hospital necessita de um sistema para sua área clínica que ajude a controlar consultas realizadas.**

* Os médicos podem ser generalistas, especialistas ou residentes e têm seus dados pessoais cadastrados em planilhas digitais;
* Cada médico pode ter uma ou mais especialidades, que podem ser pediatria, clínica geral, gastroenterologia e dermatologia;
* Alguns registros antigos ainda estão em formulário de papel, mas será necessário incluir esses dados no novo sistema;
* Os pacientes também precisam de cadastro, contendo dados pessoais (nome, data de nascimento, endereço, telefone e e-mail), documentos (CPF e RG) e convênio;
* Para cada convênio, são registrados nome, CNPJ e tempo de carência;
* As consultas também têm sido registradas em planilhas, com data e hora de realização, médico responsável, paciente, valor da consulta ou nome do convênio, com o número da carteira;
* Também é necessário indicar na consulta qual a especialidade buscada pelo paciente;
* Deseja-se ainda informatizar a receita do médico, de maneira que, no encerramento da consulta, ele possa registrar os medicamentos receitados, a quantidade e as instruções de uso;
* A partir disso, espera-se que o sistema imprima um relatório da receita ao paciente ou permita sua visualização via internet.

---

### ✅ PARTE 2 - Não era exatamente assim

**Considere a seguinte descrição:**

* No hospital, as internações têm sido registradas por meio de formulários eletrônicos que gravam os dados em arquivos. Para cada internação, são anotadas a data de entrada, a data prevista de alta e a data efetiva de alta, além da descrição textual dos procedimentos a serem realizados;
* As internações precisam ser vinculadas a quartos, com a numeração e o tipo;
* Cada tipo de quarto tem sua descrição e o seu valor diário (a princípio, o hospital trabalha com apartamentos, quartos duplos e enfermaria);
* Também é necessário controlar quais profissionais de enfermaria estarão responsáveis por acompanhar o paciente durante sua internação. Para cada enfermeiro(a), é necessário nome, CPF e registro no conselho de enfermagem (COREN);
* A internação, obviamente, é vinculada a um paciente – que pode se internar mais de uma vez no hospital – e a um único médico responsável.

  ![1730018777977](image/readme/1730018777977.png)

  [Esta planilha ilustra a estrutura dos dados utilizados na atividade.]

  ![1730006072290](image/readme/1730006072290.png)

  [Este diagrama ilustra a estrutura e os relacionamentos dos dados utilizados na atividade.]

---

### ⏳ PARTE 3 -Jogando nas regras que você criou

**Crie scripts de povoamento dos documentos desenvolvidas na atividade anterior
Observe as seguintes atividades:**

* Inclua ao menos dez médicos de diferentes especialidades;
* Ao menos sete especialidades (considere a afirmação de que entre as especialidades há pediatria, clínica geral, gastrenterologia e dermatologia);
* Inclua ao menos 15 pacientes;
* Registre 20 consultas de diferentes pacientes e diferentes médicos (alguns pacientes realizam mais que uma consulta);
* As consultas devem ter ocorrido entre 01/01/2015 e 01/01/2022;
* Ao menos dez consultas devem ter receituário com dois ou mais medicamentos;
* Inclua ao menos quatro convênios médicos, associe ao menos cinco pacientes e cinco consultas;
* Criar entidade de relacionamento entre médico e especialidade;
* Criar entidade de relacionamento entre internação e enfermeiro;
* Arrumar a chave estrangeira do relacionamento entre convênio e médico;
* Criar entidade entre internação e enfermeiro;
* Colocar chaves estrangeira dentro da internação (Chaves Médico e Paciente);
* Registre ao menos sete internações;
* Pelo menos dois pacientes devem ter se internado mais de uma vez;
* Ao menos três quartos devem ser cadastrados;
* As internações devem ter ocorrido entre 01/01/2015 e 01/01/2022;
* Considerando que a princípio o hospital trabalha com apartamentos, quartos duplos e enfermaria, inclua ao menos esses três tipos com valores diferentes;
* Inclua dados de dez profissionais de enfermaria;
* Associe cada internação a ao menos dois enfermeiros;
* Os dados de tipo de quarto, convênio e especialidade são essenciais para a operação do sistema e, portanto, devem ser povoados assim que o sistema for instalado.

---

### ⏳PARTE 4 - Inserindo Dados

**Pensando no banco que já foi criado para o Projeto do Hospital, realize algumas alterações nas tabelas e nos dados usando comandos de atualização e exclusão:**

* Crie um script que adicione uma coluna “em_atividade” para os médicos, indicando se ele ainda está atuando no hospital ou não;
* Crie um script para atualizar ao menos dois médicos como inativos e os demais em atividade.

---

### PARTE 5 - Consultas

**Crie um script e nele inclua consultas que retornem:**

1. Todos os dados e o valor médio das consultas do ano de 2020 e das que foram feitas sob convênio.
2. Todos os dados das internações que tiveram data de alta maior que a data prevista para a alta.
3. Receituário completo da primeira consulta registrada com receituário associado.
4. Todos os dados da consulta de maior valor e também da de menor valor (ambas as consultas não foram realizadas sob convênio).
5. Todos os dados das internações em seus respectivos quartos, calculando o total da internação a partir do valor de diária do quarto e o número de dias entre a entrada e a alta.
6. Data, procedimento e número de quarto de internações em quartos do tipo “apartamento”.
7. Nome do paciente, data da consulta e especialidade de todas as consultas em que os pacientes eram menores de 18 anos na data da consulta e cuja especialidade não seja “pediatria”, ordenando por data de realização da consulta.
8. Nome do paciente, nome do médico, data da internação e procedimentos das internações realizadas por médicos da especialidade “gastroenterologia”, que tenham acontecido em “enfermaria”.
9. Os nomes dos médicos, seus CRMs e a quantidade de consultas que cada um realizou.
10. Todos os médicos que tenham "Gabriel" no nome.
11. Os nomes, CORENs e número de internações de enfermeiros que participaram de mais de uma internação.
