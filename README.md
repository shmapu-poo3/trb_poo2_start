# Resumo Completo - Programação Orientada a Objetos (POO) em Python

### Classes, herança, polimorfismo, encapsulamento... objetos... atributos... metodos...

## Conceitos Básicos

### **Classe**
É o "molde" que define como um objeto deve ser criado.
```python
class Pessoa:
    def __init__(self, nome):
        self.nome = nome
```

### **Construtor (`__init__`)**
É o método especial que é executado automaticamente quando um objeto é criado, também usado para declarar os atributos da classe (papel dele é obrigar algém a informar algo...).
```python
class Pessoa:
    def __init__(self, nome: str, idade: int=None):  # construtor(parametros nao variavel e o self representa um atributo da instancia (this))
        self.nome = nome      # inicializa atributo nome
        self.idade = idade    # inicializa atributo idade
        print("Pessoa criada!")  # executa automaticamente
```

### **Objeto/Instância**
É a criação concreta de uma classe. Objeto e instância são sinônimos.
```python
pessoa1 = Pessoa("João", 25)  # chama __init__ automaticamente, 
pessoa2 = Pessoa("Maria") # chama __init__ automaticamente
print(pessoa1.nome, pessoa1.idade)
print(pessoa2.nome, pessoa2.idade)
```

### **Atributo**
São as características/propriedades de um objeto.
```python
class Carro:
    def __init__(self, marca, cor):
        self.marca = marca    # atributo
        self.cor = cor        # atributo
```

### **Método**
São as ações/comportamentos que um objeto pode executar.
```python
class Carro:
    def __init__(self, marca):
        self.marca = marca
    
    def acelerar(self):  # método
        print("Acelerando...")
```

### **Diferença: Método Construtor vs Métodos Comuns**

#### Método Construtor (`__init__`)
- É chamado **automaticamente** quando você cria um objeto
- Serve para **inicializar** os atributos do objeto
- Você **não chama** ele diretamente
```python
pessoa = Pessoa("João")  # __init__ é chamado automaticamente aqui
```

#### Métodos Comuns
- Você precisa **chamar explicitamente**
- Executam **ações** do objeto
```python
pessoa.falar()      # você chama explicitamente
pessoa.caminhar()   # você chama explicitamente
```

---

## Os 4 Pilares da POO

### 1. **Encapsulamento**
Controlar o acesso aos dados para manter integridade. **Não é apenas deixar privado**, é sobre validação e controle de acesso.

```python
class ContaBancaria:
    def __init__(self, saldo_inicial=0):  # construtor
        self._saldo = saldo_inicial  # protegido
    
    def depositar(self, valor):
        if valor > 0:  # validação
            self._saldo += valor
    
    @property
    def saldo(self):
        return self._saldo
```

### 2. **Herança**
Uma classe filha herda características da classe pai. **Nem todos os atributos são herdados** - depende do modificador de acesso.

```python
class Animal:
    def __init__(self, nome):
        self.nome = nome          # público - herdado
        self._idade = 0          # protegido - herdado
        self.__id = 123          # privado - não diretamente acessível
    
    def dormir(self):
        print(f"{self.nome} dormindo...")

class Cachorro(Animal):  # herda de Animal
    def __init__(self, nome, raca):
        super().__init__(nome)  # chama construtor da classe pai
        self.raca = raca
    
    def latir(self):
        print("Au au!")
```

### 3. **Polimorfismo**
Mesmo método, comportamentos diferentes. **Não precisa ser classe abstrata** - pode ser herança comum, interfaces ...

```python
class Gato(Animal):
    def __init__(self, nome):
        super().__init__(nome) # chama o construtor de Animal
    
    def som(self):
        return "Miau"

class Cachorro(Animal):
    def __init__(self, nome):
        super().__init__(nome)
    
    def som(self):
        return "Au au"

# Mesmo método, resultados diferentes
for animal in [Gato("Mimi"), Cachorro("Rex")]:
    print(animal.som())  # cada um faz seu som específico
```

### 4. **Abstração**
Esconder complexidade, mostrar apenas o essencial. O usuário usa funcionalidades sem saber como funcionam internamente.

```python
class Calculadora:
    def __init__(self):
        self._historico = []  # complexidade interna
    
    def somar(self, a, b):
        resultado = a + b  # uso simples
        self._salvar_historico("soma", a, b, resultado)  # complexidade escondida
        return resultado
    
    def _salvar_historico(self, operacao, a, b, resultado):  # método interno
        self._historico.append(f"{operacao}: {a} + {b} = {resultado}")

# Uso simples - abstração em ação
calc = Calculadora()
resultado = calc.somar(5, 3)  # usuário não precisa saber do histórico
```

---

## Exemplo Completo Integrado

```python
# Classe (molde)
class Pessoa:
    def __init__(self, nome, idade):     # construtor - método especial
        self.nome = nome      # atributo público
        self._idade = idade   # atributo protegido
        print(f"Pessoa {nome} criada!")
    
    def apresentar(self):     # método comum
        return f"Olá, sou {self.nome}"
    
    @property
    def idade(self):         # encapsulamento
        return self._idade

# Objetos/Instâncias
pessoa1 = Pessoa("Ana", 25)    # chama __init__("Ana", 25) automaticamente
pessoa2 = Pessoa("Carlos", 30) # chama __init__("Carlos", 30) automaticamente

print(pessoa1.apresentar())  # "Olá, sou Ana" - chama método explicitamente
print(pessoa2.idade)         # 30 - acesso encapsulado
```

---

## Fluxo de Execução dos Métodos

```python
class Pessoa:
    def __init__(self, nome):      # MÉTODO construtor
        self.nome = nome
    
    def falar(self):               # MÉTODO comum
        print(f"{self.nome} está falando")
    
    def caminhar(self):            # MÉTODO comum
        print(f"{self.nome} está caminhando")

# ONDE os métodos são chamados:

# 1. Método construtor __init__ é chamado AQUI automaticamente:
pessoa = Pessoa("João")  # ← __init__ executa automaticamente nesta linha

# 2. Métodos comuns são chamados AQUI explicitamente:
pessoa.falar()      # ← falar() é chamado AQUI
pessoa.caminhar()   # ← caminhar() é chamado AQUI
```

---

## Resumo Final

**Classes** são moldes, **construtor (`__init__`) inicializa objetos automaticamente**, **objetos** são criações desses moldes, **atributos** são características, **métodos** são ações. 

Os **4 pilares** (encapsulamento, herança, polimorfismo, abstração) organizam e estruturam o código de forma mais eficiente e reutilizável.

**Ponto-chave**: `__init__` é um método, mas é o método **construtor** - executa automaticamente na criação do objeto para inicializar seus atributos. Os outros métodos você chama quando quiser executar ações específicas.
 
**Convencoes:** Nome de Classe sempre iniciar com letra Maiuscula - Nome de Metodo: sempre usar verbo (podem ser nomes compostos (com padrao camelCase)

