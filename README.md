# Métodos Avançados de Programação

## UNIESP Faculdades

### Professora

* Drª Alana Morais ([alanamm.prof@gmail.com](mailto:alanamm.prof@gmail.com))

### Aluno
Manoel Nazario Da Silva Junior


### Padrão Comportamental: 
State


## Padrão State

### Problema: 

Há uma extrema complexidade no código quando tentamos gerênciar comportamentos diferentes, dependendo de um número de estados diferentes.
Também manter o código torna-se difícil,
e mesmo em alguns casos,
podem apontar a uma inconsistência de estados atuais na forma de implementação dos diferentes estados no código
(por exemplo, com variáveis ​​para cada estado).


### Solução: 

Se implementa uma classe para cada estado diferente do objeto e o desenvolvimento de cada método para cada estado em particular.
O objeto da classe a que pertencem esses estados resolvem os diferentes comportamentos,
dependendo de sua condição, com as instâncias das classes de estado. Assim,
sempre está presente em um objeto o seu estado atual e se comunica com ele a resolvendo suas responsabilidades.


### Consequências: 

Confina comportamento específico de estados e
particiona o comportamento específico para estados

diferentes.
Torna explícitas as transições de estado.

Objetos State podem ser compartilhados, se não
possuirem variáveis de instância. Nesse caso eles
acabam implementando o padrão Flyweight sem
estado intrínseco.

### Exemplo: 

Agora vamos imaginar um cenário,
vamos imaginar uma conta corrente bem simples com opção de depositar e sacar dinheiro
e já imaginamos os estado que essa conta pode estar saldopositivo,
saldonegativo e bloqueado.

iremos primeiro criar uma interface para os estados

public interface IContaState
{
  void Saque(Double valor);
  void Deposito(Double valor);
}


public class saldoPositivo : IContaState
{
  private Conta _conta;
 
  public saldoPositivo(Conta PConta)
  {
      this._conta = PConta;
  }
 
  #region [IContaState Members]
  public void Saque(double valor)
  {
      this._conta.Saldo -= valor;
      Console.WriteLine("Retirado Rnbsp;{0},
      saldoatualRnbsp;{1}.",valor,this._conta.Saldo);
      if(this._conta.Saldo&lt;0)
      if(this._conta.Saldo&lt;-100.00)
      this._conta.MeuEstado=newbloqueado(this._conta);
      else
      this._conta.MeuEstado=newsaldoNegativo(this._conta);
    }
 
      publicvoidDeposito(doublevalor)
      {
        this._conta.Saldo+=valor;
      Console.WriteLine("FoidepositadoRnbsp;{0},
      saldoatualRnbsp;{1}",valor,this._conta.Saldo);
      if(this._conta.Saldo&lt;0)
      if(this._conta.Saldo&lt;-100.00)
      this._conta.MeuEstado=newbloqueado(this._conta);
      else
      this._conta.MeuEstado=newsaldoNegativo(this._conta);
    }
      #endregion
    }
 
      publicclasssaldoNegativo:IContaState
      {
        privateConta_conta;
 
      publicsaldoNegativo(ContaPConta)
      {
        this._conta=PConta;
    }
 
      #region[IContaStateMembers]
      publicvoidSaque(doublevalor)
      {
        this._conta.Saldo-=valor;
      Console.WriteLine("RetiradoRnbsp;{0},
      saldoatualRnbsp;{1}.",valor,this._conta.Saldo);
 
      if(this._conta.Saldo&lt;-100.00)
      this._conta.MeuEstado=newbloqueado(this._conta);
    }
 
      publicvoidDeposito(doublevalor)
      {
        this._conta.Saldo+=valor;
      Console.WriteLine("FoidepositadoRnbsp;{0},
      saldoatualRnbsp;{1}",valor,this._conta.Saldo);
      if(this._conta.Saldo&gt;=-100.00)
      if(this._conta.Saldo&lt;0)
      this._conta.MeuEstado=newsaldoNegativo(this._conta);
      else
      this._conta.MeuEstado=newsaldoPositivo(this._conta);
    }
      #endregion
    }
 
      publicclassbloqueado:IContaState
      {
        privateConta_conta;
 
      publicbloqueado(ContaPConta)
      {
        this._conta=PConta;
    }
 
      #region[IContaStateMembers]
      publicvoidSaque(doublevalor)
      {
        Console.WriteLine("Contabloqueada,saquecancelado,
        saldoatualRnbsp;{1}.",valor,this._conta.Saldo);
    }
 
      publicvoidDeposito(doublevalor)
      {
        this._conta.Saldo+=valor;
      Console.WriteLine("FoidepositadoRnbsp;{0},saldoatualRnbsp;{1}",valor,this._conta.Saldo);
      if(this._conta.Saldo&lt;0)
      {
        if(this._conta.Saldo&lt;-100.00)
      this._conta.MeuEstado=newbloqueado(this._conta);
    }
      else
      {
        this._conta.MeuEstado=newsaldoPositivo(this._conta);
  }
}
#endregion
}
