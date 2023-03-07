# 1.2 // Objetos, Estado e Comportamento // Máquina D'água Configurável

Use este link do GitHub Classroom para ter sua cópia alterável deste repositório: <https://classroom.github.com/a/0Khbb0WO>

Implementar respeitando os fundamentos de Orientação a Objetos.

**Tópicos desta atividade:** abstrações, classes, objetos, construtores, validade, atributos, estado, comportamento, comandos e consultas, excepcionalidades e especificações.

---

A máquina d'água desta atividade é idêntica a apresentada na atividade [11](https://github.com/pooif/ava-11-objetos-estado-comportamento-maquina-dagua), porém: (1) permite configurar sua capacidade e (2) lança exceções para operações inválidas.

```java
MaquinaAguaConfiguravel maquinaCustom = new MaquinaAguaConfiguravel(10000, 30, 20);

System.out.println(maquinaCustom.capacidadeAgua == 10000); // mL
System.out.println(maquinaCustom.capacidadeCopos200 == 30);
System.out.println(maquinaCustom.capacidadeCopos300 == 20);

// As três linhas a seguinte não devem compilar pois estes atributos devem ser imutáveis:
maquinaCustom.capacidadeAgua = 100000;
maquinaCustom.capacidadeCopos200 = 300;
maquinaCustom.capacidadeCopos300 = 200;

// Checando armazenamento
System.out.println(maquinaCustom.agua() == 0); // mL
System.out.println(maquinaCustom.copos200() == 0);
System.out.println(maquinaCustom.copos300() == 0);

maquinaCustom.abastecerAgua();
maquinaCustom.abastecerCopo200();
maquinaCustom.abastecerCopo300();
System.out.println(maquinaCustom.agua() == 10000);
System.out.println(maquinaCustom.copos200() == 30);
System.out.println(maquinaCustom.copos300() == 20);

maquinaCustom.servirCopo200(); // -200
maquinaCustom.servirCopo200(); // -200
maquinaCustom.servirCopo200(); // -200
maquinaCustom.servirCopo200(); // -200
maquinaCustom.servirCopo200(); // -200

// System.out.println(maq.agua() == 9000); // patch:
System.out.println(maquinaCustom.copos200() == 25);
System.out.println(maquinaCustom.agua() == 9000);

MaquinaAguaConfiguravel maquininha = new MaquinaAguaConfiguravel(1000, 6, 3);

System.out.println(maquininha.capacidadeAgua == 1000); // mL
System.out.println(maquininha.capacidadeCopos200 == 6);
System.out.println(maquininha.capacidadeCopos300 == 3);
maquininha.abastecerAgua();
maquininha.abastecerCopo200();
maquininha.abastecerCopo300();
System.out.println(maquininha.agua() == 1000);
System.out.println(maquininha.copos200() == 6);
System.out.println(maquininha.copos300() == 3);

maquininha.servirCopo200(); // -200
maquininha.servirCopo200(); // -200
maquininha.servirCopo200(); // -200
maquininha.servirCopo200(); // -200
maquininha.servirCopo200(); // -200

System.out.println(maquininha.agua() == 0);
System.out.println(maquininha.copos200() == 1);
System.out.println(maquininha.copos300() == 3);

try {
  maquininha.servirCopo200(); // deve lançar exceção
  System.out.println(false); // esta linha não deve ser executada
} catch (IllegalStateException e) {
  System.err.println("true " + e.getMessage()); // Não há água
}

maquininha.abastecerAgua();
System.out.println(maquininha.agua() == 1000);
System.out.println(maquininha.copos200() == 1);
System.out.println(maquininha.copos300() == 3);

maquininha.servirCopo200(); // -200
System.out.println(maquininha.agua() == 800);
System.out.println(maquininha.copos200() == 0);

try {
  maquininha.servirCopo200(); // deve lançar exceção
  System.out.println(false); // esta linha não deve ser executada
} catch (IllegalStateException e) {
  System.err.println("true " + e.getMessage()); // Não há copos de 200mL
}


// Máquinas inválidas devem lançar exceção

try {
  MaquinaAguaConfiguravel maqinvalida = new MaquinaAguaConfiguravel(1000, 0, 3);
  System.out.println(false); // esta linha não deve ser executada
} catch (IllegalArgumentException e) {
  System.err.println("true " + e.getMessage()); // Copos de 200mL deve ser positivo
}

try {
  MaquinaAguaConfiguravel maqinvalida = new MaquinaAguaConfiguravel(1000, 10, 0);
  System.out.println(false); // esta linha não deve ser executada
} catch (IllegalArgumentException e) {
  System.err.println("true " + e.getMessage()); // Copos de 300mL deve ser positivo
}

try {
  MaquinaAguaConfiguravel maqinvalida = new MaquinaAguaConfiguravel(-1000, 10, 10);
  System.out.println(false); // esta linha não deve ser executada
} catch (IllegalArgumentException e) {
  System.err.println("true " + e.getMessage()); // Quantidade água deve ser positivo
}

// Máquina de 500 litros!
MaquinaAguaConfiguravel maquinao = new MaquinaAguaConfiguravel(500000, 3000, 2000);
maquinao.abastecerAgua();
maquinao.abastecerCopo300();

// Esvaziando a máquina
try { // servindo enquanto houver água até causa estado inválido
  while (true) maquinao.servirCopo300();
} catch (IllegalStateException e) {
  System.err.println("Não há água suficiente " + maquinao.agua());
}

System.out.println(maquinao.agua() == 200);
System.out.println(maquinao.copos300() == 334);
```


---
Obs.: os casos de teste não podem ser alterados, mas outros podem ser adicionados. Fique a vontade para adicionar códigos que imprimem ou separam os testes, por exemplo.
