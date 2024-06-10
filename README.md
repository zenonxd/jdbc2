Para realizarmos recuperação de dados precisamos entender duas classes do jdbc.
Statement - Ela monta um comando sql para ser executado (recuperar dados). "INSER INTO", por exemplo.
ResultSet - Representa um objeto contendo o resultado da consulta em forma de tabela. Você pode acessar os dados por colunas e linhas.

![image](https://github.com/zenonxd/jdbc2/assets/64092861/a396bade-5454-40f9-9e13-4d0ef0b0926a)

O resultSet, tem operações pra você posicionar a consulta onde quiser, exemplo:
first() - posiciona na posição 1, se houver. Exemplo na imagem acima: (computers). Se retornar nada, o resultset não vai ter a posição 1.
beforeFirst() - move para a posição 0.
Next() - vai para o proximo. Se você faz o beforeFirst() e depois next(), ele vai pra posição 1. É muito util para percorrer o resultSet. Você faz uma estrutura while e você percorre tudo. O next pode retornar false se está no ultimo também. Se você está no 4 (books) e digita Next(), vai dar false.
Absolute(int) - posiciona o resultset para a posição informada por você.

//COMANDOS//
Iniciando um statement: ![image](https://github.com/zenonxd/jdbc2/assets/64092861/dc12dc23-780d-4987-85d1-0bb5d6b30006)

Executando uma consulta no banco de dados com o statement acima criado: ![image](https://github.com/zenonxd/jdbc2/assets/64092861/4a5591fa-bfdf-419b-ad8d-ab67ffd39ac4)

Conforme citado acima, usamos o resultSet para fazer uma leitura com o next(). ![image](https://github.com/zenonxd/jdbc2/assets/64092861/a59f4199-2fe6-476b-8907-c5cc08da7c12)

Dando o SOUT na consulta feita no while: ![image](https://github.com/zenonxd/jdbc2/assets/64092861/ea27cb72-97f9-475d-867d-30b5b7b3d6cc)

Utilizamos o rs.getInt acima pois o ID é composto por numero inteiro. Assim como o getString, pois o campo depois é uma string.

Depois, para finalizarmos o bloco try-catch, usamos o finally.

![image](https://github.com/zenonxd/jdbc2/assets/64092861/8d2f2649-35d5-4faf-aa00-c6bed8e0bff0)

^Isso causaria muitas exceptions e não é o ideal. Então, iremos na classe DB e iremos criar uma classe para fechar o statement. 
```
public static void closeStatement(Statement st) {
        if (st != null) {
            try {
                st.close();
            } catch (SQLException e) {
                throw new DbException(e.getMessage());
            }
        }
    }

    public static void closeResultSet(ResultSet rs) {
        if (rs != null) {
            try {
                rs.close();
            } catch (SQLException e) {
                throw new DbException(e.getMessage());
            }
        }
    }
Basicamente: se o statement for diferente de nulo, irá fechar. Isso tudo dentro um bloco try catch, com a SQLException. Faz a mesma coisa pro resultSet.
```
![image](https://github.com/zenonxd/jdbc2/assets/64092861/86187026-c5e2-47f9-8185-3bc9287f6b25)

E ficará assim.
