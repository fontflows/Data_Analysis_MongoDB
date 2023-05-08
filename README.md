<h1 align="center"> Análise de Dados de Pedidos por Whatsapp Usando MongoDB e Mongoose </h1>
<h2> Conexão com o banco de dados </h2>
<p>No trecho inicial do código 'app.js' importamos a biblioteca 'mongoose' e utilizamos o método 'connect' para nos conectarmos ao banco de dados "brendi" no endereço "localhost:;27017". Também utilizamos o objeto de opções ' { useNewUrlParser : true} para garantir que o driver do MongoDB utilize o novo analisador de URL.</p>
<p>Em seguida, adicionamos dois event listeners para escutar os eventos 'error' e 'open' do objeto 'mongoose.connection'. O evento 'error' é disparado caso ocorra algum erro durante a conexão com o banco de dados. Já o evento 'open' é disparado quando a conexão é estabelecida com sucesso.</p> 
