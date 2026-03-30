# 🧠 ALU de 8 bits

Implementação de uma Unidade Lógica e Aritmética (ALU) de 8 bits, desenvolvida utilizando lógica digital a partir de portas básicas, seguindo os requisitos da atividade proposta.

---

## 📌 Objetivo

O objetivo deste projeto foi desenvolver uma ALU simples de 8 bits, contemplando operações aritméticas, operações lógicas, registradores (AC e MQ) e seletor de operação. 

Conforme especificado no enunciado da atividade: *"Criar uma ALU simples com circuitos de operações, seletor e registradores."*

---

## ⚙️ Operações Implementadas

**➕ Aritméticas**
* Soma: `AC + N → AC`
* Subtração: `AC - N → AC`
* Multiplicação (sequencial) com resultado de 16 bits (`AC = 8 LSB`, `MQ = 8 MSB`)

**🔀 Lógicas**
* NAND
* XOR

**🔁 Deslocamentos (Shift lógico)**
* Shift Left
* Shift Right

---

## 🧱 Arquitetura do Projeto

A ALU foi construída de forma modular com os seguintes blocos principais:

* **1. Somador/Subtrator 8 bits:** Implementado com somadores de 1 bit em cascata. A subtração é feita via complemento de 2 (`B XOR SUB`, `CIN = SUB`).
* **2. REG_AC_8 (Acumulador):** Armazena resultados das operações. Controlado por `DATA`, `STORE` e `CLOCK`.
* **3. REG_MQ_8:** Utilizado na multiplicação para armazenar o multiplicador e parte do resultado.
* **4. Operadores Lógicos:** NAND e XOR implementados bit a bit (8 bits).
* **5. Shift Lógico:** Shift Left (multiplica por 2, insere 0 no LSB) e Shift Right (divide por 2, insere 0 no MSB).
* **6. Seletor (MUX):** Multiplexador de 8 bits controlado por `OP[2:0]`, seleciona qual operação será enviada ao registrador.

---

## ✖️ Multiplicador Sequencial

Esta foi a parte mais complexa da arquitetura. O algoritmo clássico de multiplicação binária sequencial foi utilizado:

> Para cada bit de MQ:
> Se MQ0 = 1 → AC = AC + A
> Shift Right em [AC | MQ]

**Componentes usados:**
* Somador 8 bits
* MUX (decisão AC ou AC+A)
* Join (16 bits)
* Shift Right 16 bits
* Split (16 bits)
* REG_AC_8 e REG_MQ_8

---

## 🧪 Testes Realizados

| Operação | Entrada | Resultado esperado | Resultado obtido |
| :--- | :--- | :--- | :---: |
| **Soma** | 3 + 5 | 8 | ✔️ |
| **Subtração** | 5 - 3 | 2 | ✔️ |
| **NAND** | 3 NAND 5 | correto | ✔️ |
| **XOR** | 3 XOR 5 | correto | ✔️ |
| **Shift Left** | 3 | 6 | ✔️ |
| **Shift Right** | 3 | 1 | ✔️ |
| **Multiplicação** | 3 × 3 | 9 | ✔️ |

---

## ⚠️ Limitação do Projeto

**❌ Divisão NÃO implementada**

Apesar de prevista no enunciado (*"Divisão: AC / N → AC (resto) e MQ (quociente)"*), não foi possível implementar a divisão e integrá-la na ALU dentro do tempo disponível.

**Motivos:**
* Alta complexidade do algoritmo sequencial de divisão.
* Necessidade de controle mais avançado (FSM mais robusta).
* Prioridade dada à finalização completa e funcional das demais operações.

---

## 🧩 Integração da ALU

A ALU final é composta por Registrador AC, Registrador MQ, Blocos de operação, Seletor (MUX), Entrada N e Controle por clock.

**Fluxo padrão:** `N + AC → operação → MUX → REG_AC`

**Fluxo na multiplicação:** `REG_AC + REG_MQ → MULT_8 → saída 16 bits`

---

## 🎥 Entrega

* ✔️ README explicativo
* ⏳ Vídeo explicativo: [LINK](https://docs.google.com/document/d/1VEWSaBhOKvqFFlK16f6JNKOvmstcJ4ioU4ucZt1Qi9U/edit?tab=t.0)

---

## 📚 Aprendizados

Este projeto permitiu consolidar conceitos fundamentais de:
* Arquitetura de computadores
* Circuitos sequenciais
* Registradores
* Controle por clock
* Multiplexação
* Operações binárias

Além disso, destacou a importância de separar lógica combinacional e sequencial, definir corretamente convenções de barramento e trabalhar com encapsulamento modular.

---

## 🚀 Conclusão

A ALU desenvolvida atende à maior parte dos requisitos da atividade, incluindo operações aritméticas, lógicas, shift lógico, multiplicação sequencial, registradores e seletor. Apesar da ausência da divisão, o sistema demonstra domínio sólido dos conceitos exigidos.
