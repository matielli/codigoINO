Documentação do Código

# **__MARKDOWN__**

Instituição
Técnico em Desenvolvimento de Sistemas - SENAC NH

**Aluno**:
**Rafael Matielli**

__Professor__:
__Glauber Kiss de Souza__

**Disciplina**:
Analisar Orient. Técnicas



**Descrição Geral**


Este programa é desenvolvido para um microcontrolador Arduino. Ele realiza a soma de dois números de 4 bits, lidos de pinos de entrada digitais, e exibe o resultado nos pinos de saída digitais, incluindo o bit de transporte (carry).


__Variáveis Globais__


soma: Variável para armazenar o valor lido do pino 13, que indica se a soma deve ser realizada.

carryBit: Armazena o bit de transporte durante a soma.


nib1a, nib1b, nib1c, nib1d: Bits do primeiro número de 4 bits.


nib2a, nib2b, nib2c, nib2d: Bits do segundo número de 4 bits.


res1a, res1b, res1c, res1d: Resultados da soma de cada bit.


**Funções**


void setup()
Configura os modos dos pinos digitais:


Pinos 0 a 7 são configurados como entradas para ler os bits dos números a serem somados.

Pinos 8 a 12 são configurados como saídas para exibir o resultado da soma.

Pino 13 é configurado como entrada para ler a flag que ativa a soma.

cpp

Copiar código

void setup()

{

    pinMode(0, INPUT);
    
    pinMode(1, INPUT);
    
    pinMode(2, INPUT);
    
    pinMode(3, INPUT);
    
    pinMode(4, INPUT);
    
    pinMode(5, INPUT);
    
    pinMode(6, INPUT);
    
    pinMode(7, INPUT);
    
    pinMode(8, OUTPUT);
    
    pinMode(9, OUTPUT);
    
    pinMode(10, OUTPUT);
    
    pinMode(11, OUTPUT);
    
    pinMode(12, OUTPUT);
    
    pinMode(13, INPUT);
}


int somaBit(int b1a, int b2a, int cBit)

Realiza a soma de dois bits (b1a e b2a) e do bit de transporte (cBit). Retorna o resultado do bit somado (sem o transporte).




cpp

Copiar código

int somaBit(int b1a, int b2a, int cBit)

{

    int bitResult = 0;
    
    if ((b1a ^ b2a) ^ cBit)
    
    {
    
        bitResult = 1;
    }
    
    
    else
    
    {
    
        bitResult = 0;
    }
    
    
    return bitResult;
}


int somaCarryBit(int b1a, int b2a, int cBit)

Calcula o bit de transporte resultante da soma de dois bits (b1a e b2a) e do bit de transporte (cBit). Retorna o bit de transporte.



cpp

Copiar código

int somaCarryBit(int b1a, int b2a, int cBit)

{

    if ((b1a && b2a) || (b1a && cBit) || (b2a && cBit))
    
    {
    
        cBit = 1;
    }
    
    
    else
    
    {
    
        cBit = 0;
    }
    
    
    return cBit;

}




Executa continuamente as seguintes etapas:


Lê a flag de soma do pino 13.

Lê os bits dos dois números dos pinos 0 a 7.

Se a flag de soma estiver ativada (soma == 1), realiza a soma bit a bit dos dois números, levando em conta o transporte.

Escreve os resultados da soma e o bit de transporte nos pinos 8 a 12.

cpp

Copiar código

void loop()

{

    soma = digitalRead(13);
    
    nib1a = digitalRead(0);
    
    nib1b = digitalRead(1);
    
    nib1c = digitalRead(2);
    
    nib1d = digitalRead(3);
    
    nib2a = digitalRead(4);
    
    nib2b = digitalRead(5);
    
    nib2c = digitalRead(6);
    
    nib2d = digitalRead(7);
    
    if (soma == 1)
    
    {
    
        carryBit = 0;
        
        res1a = somaBit(nib1a, nib2a, carryBit);
        
        carryBit = somaCarryBit(nib1a, nib2a, carryBit);
        
        res1b = somaBit(nib1b, nib2b, carryBit);
        
        carryBit = somaCarryBit(nib1b, nib2b, carryBit);
        
        res1c = somaBit(nib1c, nib2c, carryBit);
        
        carryBit = somaCarryBit(nib1c, nib2c, carryBit);
        
        res1d = somaBit(nib1d, nib2d, carryBit);
        
        carryBit = somaCarryBit(nib1d, nib2d, carryBit);
    }
    
    
    digitalWrite(8, res1a);
    
    digitalWrite(9, res1b);
    
    digitalWrite(10, res1c);
    
    digitalWrite(11, res1d);
    
    digitalWrite(12, carryBit);
}


Instalação do Programa

Materiais Necessários

Placa Arduino (qualquer modelo compatível com pinos digitais).

Cabo USB para conectar o Arduino ao computador.

Software Arduino IDE instalado no computador.

Breadboard e fios de conexão.

Botões ou switches para simular entradas digitais (opcional).

Passos para Instalação

Configuração do Hardware:



Conecte os fios de entrada aos pinos 0 a 7 do Arduino.

Conecte os fios de saída aos pinos 8 a 12 do Arduino.

Conecte um botão ou switch ao pino 13 para ativar a soma.

Configuração do Software:



Abra o Arduino IDE no computador.

Conecte a placa Arduino ao computador usando o cabo USB.

Selecione a placa Arduino e a porta correta no menu "Ferramentas".

Carregamento do Código:



Copie o código fornecido para o editor de texto no Arduino IDE.

Clique em "Verificar" para compilar o código e verificar se há erros.

Clique em "Carregar" para enviar o código compilado para a placa Arduino.

Comandos para Executar o Programa

Compilação e Carregamento do Código:



Abra o Arduino IDE.

Cole o código no editor.

Clique no botão "Verificar" (ícone de check) para compilar.

Clique no botão "Carregar" (ícone de seta) para enviar o código para o Arduino.

Operação do Programa:



Após o código ser carregado, o Arduino começará a executar automaticamente.

Configure os pinos de entrada para os bits dos números que você deseja somar.

Acione o botão/switch conectado ao pino 13 para ativar a soma.

Observe os pinos de saída (8 a 12) para ver o resultado da soma.

**Resumo**

Este programa para Arduino lê dois números de 4 bits dos pinos de entrada, realiza a soma bit a bit considerando o bit de transporte, e exibe o resultado nos pinos de saída. A instalação é simples e envolve a configuração de pinos digitais e o carregamento do código 
via Arduino IDE.






