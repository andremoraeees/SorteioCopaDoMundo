O projeto tem como objetivo realizar o Sorteio da Copa do Mundo de Futebol 2026.

O sorteio consiste em 4 potes, com 12 seleções nacionais em cada, separados pelo ranking da FIFA.

🔹 Equipes do mesmo pote não se enfrentam;
🔹 Todos os grupos devem conter ao menos 1 seleção da UEFA e no máximo 2;
🔹 Para as demais confederações, é permitido apenas uma seleção de cada confederação por grupo;
🔹 Equipes da repescagem que podem ocupar múltiplas confederações;

1️⃣ Extração e Poda do Espaço Amostral
Nesta fase, o objetivo é reduzir o número de combinações antes de iniciar o sorteio pesado.

- Importação: O código lê os 4 potes a partir de uma fonte externa (Excel).
- Criação de Flags: São gerados indicadores binários para cada confederação (UEFA, CONMEBOL, etc.) por seleção.
- Produto Cartesiano Restrito: Em vez de gerar todas as combinações matemáticas possíveis, o código realiza Joins sucessivos entre os potes, aplicando a cláusula HAVING para descartar imediatamente qualquer grupo que fira as travas geográficas básicas (ex: mais de 2 seleções da UEFA ou mais de 1 de outras confederações).

Resultado: Uma tabela de "Possibilidades Válidas" significativamente menor que o espaço amostral original.

2️⃣ Processamento com Backtracking
Aqui reside o "core" da inteligência do projeto. O algoritmo tenta montar o quadro completo de 12 grupos.

- Seleção Iterativa: O código escolhe a primeira combinação válida para o Grupo 1.
- Propagação de Restrições: Ao fixar um grupo, o algoritmo remove todas as seleções utilizadas das tabelas de possibilidades dos grupos subsequentes.
- Gestão de Tentativas e Erros (Backtracking): Caso o algoritmo chegue a um ponto onde não existam mais combinações válidas para os grupos restantes (um "impasse" lógico), ele identifica a Tentativa Frustrada, retrocede ao grupo anterior, descarta a escolha que levou ao erro e tenta um novo caminho.
- Regras Dinâmicas: Durante o loop, o código monitora variáveis globais (como o limite de grupos com "dupla UEFA") para garantir que o sorteio final seja equilibrado de acordo com as restrições pré-estabelecidas.

Resultado Final: Uma tabela contendo os grupos definidos com os nomes das seleções e suas respectivas confederações formatadas.

3️⃣ Camada de Auditoria e Validação 
Após a geração dos 100% de sucesso, o código submete o resultado a um rigoroso teste de estresse:

- Verificação de Unicidade: Garante que nenhuma seleção foi escalada em dois grupos diferentes.
- Check Geográfico: Uma varredura final valida se todos os 12 grupos respeitam as regras de confederações da FIFA.

Resultado Final: Uma tabela contendo os grupos definidos com os nomes das seleções, suas respectivas confederações formatadas, e o indicador de cada regra aplicada.

/*===============================================================================================================================*/
/*===============================================================================================================================*/

Para executar via SAS:

1) Acesse https://welcome.oda.sas.com/;
2) Faça o Sign In;
3) Clique em Lauch:
4) Ao abrir o SAS Studio, no menu a esquerda clique em Server Files and Folders;
5) Clique com o botão direito em "Files (Home)", em seguida em "New", "Folder";
6) Crie uma folder com o nome de "sorteio_copa";
7) Clique com o botão direito na folder "sorteio_copa", e faça o upload nos arquivos "Input_Potes.xlsx" e "Sorteio_Copa.sas".
8) Clique novamente com o botão direito na folder "sorteio_copa", em seguida clique em "Properties";
9) Copie o valor apresentado para "Location";
10) Abra o program "Sorteio_Copa.sas";
11) Na primeira linha, substitua o valor declaraado de caminho, pelo valor copiado no passo 9.
12) Clique no ícone de disquete para salvar o código e ele estará pronto para sua execução.
