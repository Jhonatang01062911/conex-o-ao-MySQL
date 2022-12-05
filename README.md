# conex-o-ao-MySQL

Passos para a conexão ao MySQL
Vejamos os passos que devemos seguir para realizar a conexão a um banco de dados MySQL usando um script em Python.

Ter o MySQL Server instalado, configurado e em execução na máquina local. Preferencialmente, ter um banco de dados já criado para testar a conexão.
É necessário instalar o conector para MySQL do Python, que pode ser instalado usando o gerenciador de pacotes pip (no prompt / terminal) com o comando a seguir:
$ pip3 install mysql-connector-python
Com o método mysql.connector.connect() do conector MySQL Python iremos conectar o script Python ao banco de dados MySQL passando os parâmetros requeridos, que incluem o nome do host, nome do banco de dados, usuário e senha para a conexão..
Após efetivar a conexão usamos o objeto retornado pelo método connect() para criar um objeto cursor que permitirá realizar operações no banco de dados, como as declarações SQL para consultas, inserções, atualizações e exclusões de registros, entre outras.
Neste ponto podemos então executar as consultas SQL desejadas a partir do Python com o método cursor.execute().
Após terminar de realizar as consultas, fechamos o objeto cursor com o método cursor.close(), e também fechamos a conexão ao banco MySQL com o método connection.close() para liberar os recursos do sistema.
Não esquecer de capturar exceções caso algum erro possa ocorrer durante esse processo (veremos esse passo na próxima lição).
Código de conexão e teste (simplificado):
A seguir, temos um código simplificado para o teste de conexão do Python a um banco MySQL. Não vamos aqui usar blocos try /catch nem aplicar técnicas de segurança mais robustas, pois o objetivo hoje é simplesmente mostrar como usar o módulo mysql-connector-python para criar uma conexão, criar um cursor e executar uma declaração SQL no banco selecionado.

import mysql.connector
con = mysql.connector.connect(host='localhost',database='db_MeusLivros',user='root',password='123**')
if con.is_connected():
    db_info = con.get_server_info()
    print("Conectado ao servidor MySQL versão ",db_info)
    cursor = con.cursor()
    cursor.execute("select database();")
    linha = cursor.fetchone()
    print("Conectado ao banco de dados ",linha)
if con.is_connected():
    cursor.close()
    con.close()
    print("Conexão ao MySQL foi encerrada")
Resultado:

======== RESTART: C:\Users\Boson\Downloads\Conectar-MySQL-IDLE.py ========
Conectado ao servidor MySQL versão 5.7.13-log
Conectado ao banco de dados ('db_meuslivros',)
Conexão ao MySQL foi encerrada
>>> 
Conexão iniciada e finalizada com sucesso ao banco de dados MySQL. Executamos também a declaração SQL do MySQL SELECT DATABASE(), a qual retorna o nome do banco de dados selecionado no momento.
