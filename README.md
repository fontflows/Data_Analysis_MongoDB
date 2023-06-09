<h1 align="center"> Análise de Dados de Pedidos por Whatsapp Usando MongoDB e Mongoose </h1>
<hr><h2>Atenção</h2></hr>
<p>Na última versão atualizada, depois de finalizada a parte de análise de dados, foi adicionada uma interface web dentro da paste "python" na raiz do projeto. Observa-se que, para essa versão, o front(python) e o backend(app.js, conversation.js e messages.js) estão prontos, porém, a infraestrutura de conexão ainda está sendo desenvolvida. Recomenda-se alterar as configurações de segurança para permitir a chamada de dados do back no front. </p>
<hr></hr>
<p>O código consiste em um aplicativo que usa o MongoDB para armazenar mensagens de texto enviadas por clientes para lojas e agrupa essas mensagens em conversas, com base no número de telefone do cliente e no identificador da loja.</p> 

<h2>app.js</h2>
<p>O arquivo app.js é o arquivo principal, que inicia a conexão com o MongoDB usando o pacote mongoose e chama a função groupMessagesIntoConversations() para agrupar as mensagens em conversas.</p>
<p>A função groupMessagesIntoConversations() é responsável por buscar todas as mensagens do banco de dados, ordená-las pelo carimbo de data/hora em que foram recebidas e agrupá-las em conversas. Ele faz isso usando um loop for que itera sobre todas as mensagens e verifica se a mensagem pertence a uma conversa existente ou se é o início de uma nova conversa.</p>
<p>Se a mensagem é o início de uma nova conversa, a função cria um novo objeto de conversa com o ID da conversa, o número de telefone do cliente, o carimbo de data/hora em que a mensagem foi recebida, o identificador da loja, o identificador do menu da loja e uma matriz vazia de mensagens. Em seguida, ele adiciona a mensagem atual à matriz de mensagens e salva a conversa no banco de dados usando o método save() do mongoose.</p>
<p>Se a mensagem não é o início de uma nova conversa, a função verifica se a diferença entre o carimbo de data/hora da mensagem atual e o carimbo de data/hora da última mensagem na conversa atual é maior que quatro horas. Se for maior, a função cria uma nova conversa com a mensagem atual e salva-a no banco de dados. Se não for maior, a função simplesmente adiciona a mensagem atual à matriz de mensagens da conversa atual e salva a conversa no banco de dados.</p>
<p>A função também calcula o número total de conversas para cada identificador de menu de loja e exibe a lista de identificadores de menu e o número total de conversas para cada um.</p>

<h2>messages.js</h2>
<p>O arquivo messages.js contém a definição do esquema de mensagem para o banco de dados MongoDB e o modelo correspondente. O esquema é definido utilizando o pacote mongoose e contém as seguintes propriedades:</p>
<ul>
  <li>category: uma string que representa a categoria da mensagem (por exemplo, "pedido", "consulta", "elogio", etc.).</li>
  <li>customerPhone: uma string que representa o número de telefone do cliente que enviou a mensagem.</li>
  <li>prompt: uma string que representa a mensagem enviada ao cliente.</li>
  <li>receivedMessage: uma string que representa a resposta enviada pelo cliente ao estabelecimento.</li>
  <li>receivedTimestamp: uma data que representa o momento em que a mensagem foi recebida pelo    estabelecimento.</li>
  <li>responseTimestamp: uma data que representa o momento em que a resposta foi enviada ao cliente.</li>
  <li>sentMessage: uma string que representa a mensagem enviada pelo estabelecimento ao cliente.</li>
  <li>storeId: uma string que representa o ID do estabelecimento que recebeu a mensagem.</li>
  <li>storeMenuSlug: uma string que representa o slug do menu do estabelecimento.</li>
  <li>storePhone: uma string que representa o número de telefone do estabelecimento.</li>
</ul>
<p>O modelo messages é criado a partir do esquema e é utilizado pelo aplicativo para armazenar as mensagens recebidas e enviadas pelo estabelecimento.</p>

<h2>conversation.js</h2>
<p>O arquivo conversation.js contém a definição do esquema de conversa para o banco de dados MongoDB e o modelo correspondente. O esquema é definido utilizando o pacote mongoose e contém as seguintes propriedades:</p>
<ul>
  <li>_id: uma string que representa o ID da conversa.</li>
  <li>customerPhone: uma string que representa o número de telefone do cliente que iniciou a conversa.</li>
  <li>receivedTimestamp: uma data que representa o momento em que a primeira mensagem da conversa foi recebida pelo estabelecimento.</li>
  <li>storeId: uma string que representa o ID do estabelecimento com o qual o cliente está conversando.</li>
  <li>storeMenuSlug: uma string que representa o slug do menu do estabelecimento.</li>
  <li>messages: um array de objetos de mensagem, que contém as mesmas propriedades do esquema de mensagem.</li>
</ul>
<p>O modelo conversations é criado a partir do esquema e é utilizado pelo aplicativo para agrupar as mensagens recebidas e enviadas pelo estabelecimento em conversas, de forma que cada conversa é representada por um documento na coleção conversations.</p>

<h2>Conversations.ipynb</h2>
<p>Esses dois blocos de código são programas em Python que lêem um arquivo JSON contendo informações sobre conversas de clientes com restaurantes, e depois filtram e agregam os dados para gerar duas visualizações diferentes:</p>
<ul>
  <li>O primeiro bloco de código gera uma tabela formatada e uma contagem do número de conversas por restaurante, durante um período de tempo definido pelo usuário. O usuário é solicitado a fornecer uma data inicial e final, e o código filtra o DataFrame para exibir apenas as conversas que ocorreram nesse período. Em seguida, o código agrupa as conversas por restaurante e conta quantas conversas ocorreram em cada um, e exibe a tabela formatada e a contagem total de conversas.</li>
  <li>O segundo bloco de código gera um gráfico de barras mostrando o número de conversas por restaurante, durante um período de tempo definido pelo usuário. O usuário é solicitado a fornecer uma data inicial e final, e o código filtra o DataFrame para exibir apenas as conversas que ocorreram nesse período. Em seguida, o código agrupa as conversas por restaurante e conta quantas conversas ocorreram em cada um. O gráfico de barras é gerado usando a biblioteca Matplotlib, e é exibido com rótulos apropriados para os eixos e um título que inclui as datas selecionadas pelo usuário.</li>
</ul>
<p> Ambos os programas usam a biblioteca Pandas para ler e manipular dados tabulares, e usam a biblioteca datetime para lidar com datas e horas. O primeiro programa usa o método groupby() para agrupar os dados por restaurante, e o segundo usa o método count() para contar as conversas em cada grupo. O primeiro programa usa a biblioteca Styler da Pandas para formatar a tabela, enquanto o segundo usa a biblioteca Matplotlib para gerar o gráfico de barras. </p>
