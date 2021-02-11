# qa-teste-pratico
[Processo seletivo QA] Teste Prático IA


Dada a seguinte User Story: 
Como Gerente de Marketing, gostaria que fosse enviada uma mensagem para o cliente, participante do clube de clientes, quando pelo menos um dos produtos comumente consumidos por ele entrar em promoção.
Critérios de aceitação: 
A mensagem deve ter o formato: "Olá , os seguintes produtos que você costuma consumir estão em promoção! 
Vem conferir: "<Nome do produto>: <De> por <preço da promoção>"
A mensagem só deve ser enviada para o cliente se o produto que entrar em promoção for de consumo do mesmo e o cliente não efetuou sua compra nos últimos 5 dias.
A mensagem deve conter no máximo 3 produtos de consumo contínuo do cliente, sendo estes sempre os mais relevantes para o mesmo.
O sistema deverá salvaguardar a informação de que a mensagem foi enviada para o cliente.
Pede-se:

1)	De acordo com sua experiência, escreva os possíveis cenários de testes.

Resposta:
Fluxo Principal:
CT01- Mensagem ao cliente que atende os requisitos da promoção.
Resultado Esperado: Mensagem deve ser enviada ao cliente com a informação <Nome do produto>: <De> por <preço da promoção>

Fluxos Alternativos:
CT02: Mensagem ao cliente que nunca consumiu o produto.
Resultado Esperado: Mensagem não deve ser enviada ao cliente

CT03: Mensagem ao cliente que consumiu o produto a menos de 5 dias da promoção                
Resultado Esperado: Mensagem não deve ser enviada ao cliente

CT04: Mensagem ao cliente que consumiu o produto a mais de 5 dias e possui mais de 3 produtos relevantes no seu cadastro              
Resultado Esperado: Mensagem deve ser enviada ao cliente, com observância de apenas apresentar os 3 produtos mais relevantes para o mesmo.

CT05: Verificar log de retorno da mensagem                 
Resultado Esperado: Log deve gravar o envio da mensagem ao cliente.

2) Alex precisou ausentar-se do trabalho e a atividade de escrever os
testes unitários dessa User Story foi redirecionada para você.
Utilizando-se de uma linguagem de programação que você tenha
maior familiaridade e conhecimento em TDD, escreva os testes
unitários necessários.

Resposta:
Não tenho vivencia em testes unitários. 

3) Dada a estrutura de dados relacional abaixo, desenvolva a query que
será responsável por recuperar os 5 produtos de maior incidência
nas compras dos clientes (não levar em consideração a quantidade,
mas apenas se determinado produto apareceu ou não numa
compra) nos últimos 3 meses.

Resposta:
SELECT RESULTADO.idcliente, RESULTADO.idproduto, RESULTADO.incidencia FROM  (	
	select cli.id as idcliente,
		   pc.id_produto as idproduto,
		   count(*) as incidencia,
		   Row_Number() OVER (PARTITION BY cli.id ORDER BY count(*) desc) AS rn
	from _produto_compra pc
	left join _compra c on (pc.id_compra = c.id)
	left join _cliente cli on (c.id_cliente = cli.id)
	where DATEDIFF(MONTH, c.data, GETDATE()) <= 3
	group by cli.id, pc.id_produto
) RESULTADO
WHERE RESULTADO.RN <= 5

4) Na cerimônia de retrospectiva de uma dada sprint, o time pontuou as seguintes problemáticas: 
● Funcionalidades implementadas de forma incompleta 
● Dificuldade em realizar correções de não conformidades (manutenção do código). 
● Dificuldade em rastrear os erros apontados nas baterias de testes realizadas. 
De posse deste feedback, o ScrumMaster do projeto solicitou uma reunião entre o líder técnico e você para que a "Definição de Pronto" do projeto fosse revisada. Segue abaixo a definição citada. De acordo com sua experiência, o que você mudaria nela? Além disso, você acharia necessário provocar algum outro tipo de ação em conjunto com o time de desenvolvimento? Comente. 

Resposta:
Seria necessário entender o motivo da dificuldade em rastrear no código os erros apontados, em seguida, realizar a adoção de um padrão de escrita (caso não exista) e inclusão de comentários facilitando assim, a manutenção do código criado.
Para os erros apontados pela equipe QA, poderíamos verificar uma melhor descrição dos erros e dependendo da complexidade, trabalharmos com ferramentas de gravação de tela, facilitando o entendimento pela equipe de desenvolvimento.

Definição de Pronto: 
1.	A funcionalidade/correção foi implementada;
2.	Passou na revisão de código para saber se está dentro dos padrões da empresa;
3.	Passou nos testes unitários com cobertura mínima de 80%;
4.	A funcionalidade/correção foi testada no ambiente de QA;
5.	Todos os critérios de aceitação atendidos;
6.	Atualizado com o controle de versão e permanecer compilando;
7.	Softwares de apoio e documentação atualizados;

