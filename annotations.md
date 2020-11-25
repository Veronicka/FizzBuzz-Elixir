# ESTUDANDO ELIXIR

modo interativo -> iex

#### tipos de dados 
 - inteiro = 1, 2, 3
 - float = 1.2, 2.5, 5.4
 - boolean = true, false
 - string = morando, maçã
 - atom (constante) = :banana, :chocolate
 - operadores lógicos (and, or, &&, || )

#### Método identificador de tipos:
 - is_float(5.2)
 - is_boolean(true)
 - is_binary("banana")
 - is_atom(:carro) ...

 - ELIXIR SEMPRE USA ASPAS DUPLAS PARA STRING

#### Operadores:
 - 5 + 5 = 10
 - 5 - 2 = 3
 - 5 / 2 = 2.5
 - div(5, 2) = 2
 - rem(5, 2) = 1 (resto da divisão)

#### Interpolação de Strings:
 meu_carro: fox
 "Meu carro é um #{meu_carro}" 

#### Concatenação de Strings:
  "Meu nome é " <> "Café"

Todos os operadores e funções que pertencem ao módulo Kernel podem ser chamados sem instanciar nada. 

TUPLAS são utilizadas para retornos de operações e erros. Para criar uma TUPLA usa-se chaves ('{' coisas dentro '}')

LISTAS são criadas usando colchetes ('[' coisas dentro ']). Elas são implementadas usando lista encadeada

 Ex: list = [2, 3, 4]
       adicionando 1: list = [ 1 | list ]
       resultado: [1, 2, 3, 4]

  concatenando listas:
      [1, 2] ++ [3 , 4]
   
  subtraindo:
      [1, 2] -- [1]
  
  pegando o head (cabeça):
      hd list
  pegando o tail (cauda, restante):
      tl list

Não é possível acessar um elemento da lista tão facilmente como em python list[3]. Mas podemos usar atoms que apontam para elementos da lista:
  a = [primeiro: 1, segundo: 2, terceiro: 3]

  acessando:
    a[:primeiro]
    a[:terceiro]

### Maps, armazena dados
    person = %{age: "4", name: "Belinha"}  
        ou 
    person = %{"age" => "4", "name" => "Belinha"}

    person[:name]
    person[:age]

    person.name

#### atualizar valores no Maps
    person = %{person | age: "5"}

#### remover uma nova chave
    person = Map.delete(person, :age)

#### adicionar uma nova chave
    person = Map.put(person, :city, "Jacareí")

#### mergeando um map
    address = %{street: "Rua tal"}
    Map.merge(person, address)


### Módulo Enum

#### percorrendo uma lista e imprimindo no terminal
    Enum.each([1, 2, 3, 4, 5], fn x -> IO.puts(x) end)

#### somando mais um na list
    Enum.map([1, 2, 3, 4, 5], fn x -> x + 1 end)

#### Listas com Maps
    numbers = %{x: 1, y:2, z:3}
    map = Enum.map(numbers, fn {k, v} -> {k, -v} end)

#### Retornando listas para map
    Map.new(map)

### Pattern Matching
    igual (=) é um operador de match 

    [a, b, c] = [1, 2, 3]

    [head | tail] = [1, 2, 3, 4, 5]

    [a, b | tail] = [1, 2, 3, 4, 5]

    criando uma função anonima

    handle_file_read = fn
    {:ok, result} -> result
    {:error, msg} -> "Erro ao ler o arquivo. Mensagem: #{msg}"
    end

    ao chamar essa função com um arquivo existente, ela cairá na primeira condição, 
    caso o arquivo não exista, cairá na segunda (Obs: não precisa usar if) 

    handle_file_read.(File.read("valid.txt"))
    handle_file_read.(File.read("invalid.txt"))

### Pipe Operator
    Para diminuir a confução de chamar função dentro de funções  infinitamentes

    "invalid.txt" |> File.read() |> handle_file_read.()

    ele concatena os fluxos como primeiro argumento das funçoes, 
    logo ele não precisa ser passado

    "valid.txt" |> File.read() |> handle_file_read.() |> IO.inspect(label: "resultado")

