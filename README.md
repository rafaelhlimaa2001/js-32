'use strict';

/* ==========================================================
   Introdução ao JavaScript – Desafios práticos
   Executar com:  node app.js   (ou colar no console do navegador)
   ========================================================== */

const titulo = (texto) => console.log(`\n===== ${texto} =====`);

/* ==========================================================
   BLOCO 1 – FUNDAMENTOS E VARIÁVEIS
   ========================================================== */
titulo('BLOCO 1 – Fundamentos e Variáveis');

// 1.1 let: valor pode ser alterado
let pontos = 50;
pontos = pontos + 10; // soma 10 na linha seguinte
console.log('Pontos:', pontos); // 60

// 1.2 const: não pode ser reatribuída
const MAX_PONTOS = 100;
try {
  MAX_PONTOS = 200; // erro!
} catch (erro) {
  console.log(`${erro.name}: ${erro.message}`);
  // Motivo: const cria uma ligação (binding) somente leitura.
  // Depois de inicializada, o identificador não pode apontar para outro valor.
}

// 1.3 Tipos primitivos e typeof
const nome = 'Rafael';      // string
const idade = 25;           // number
const ativo = true;         // boolean
let indefinida;             // undefined (declarada, sem valor)
const vazio = null;         // null (ausência intencional de valor)

console.log('typeof string   :', typeof nome);
console.log('typeof number   :', typeof idade);
console.log('typeof boolean  :', typeof ativo);
console.log('typeof undefined:', typeof indefinida);
console.log('typeof null     :', typeof vazio, '(peculiaridade histórica da linguagem: null é primitivo, mas typeof retorna "object")');

// 1.4 Template literals x concatenação
const fraseTemplate = `${nome} tem ${idade} anos e está com ${pontos} pontos.`;
const fraseConcatenada = nome + ' tem ' + idade + ' anos e está com ' + pontos + ' pontos.';
console.log('Template     :', fraseTemplate);
console.log('Concatenação :', fraseConcatenada);
console.log('Resultados iguais?', fraseTemplate === fraseConcatenada);

/* ==========================================================
   BLOCO 2 – FUNÇÕES
   ========================================================== */
titulo('BLOCO 2 – Funções');

// 2.1 Função declarada + hoisting (chamada ANTES da declaração)
console.log('Declarada (antes da declaração): 20 anos ->', ehMaiorDeIdade(20));

function ehMaiorDeIdade(idadePessoa) {
  return idadePessoa >= 18;
}

console.log('Declarada: 15 anos ->', ehMaiorDeIdade(15));

// 2.2 Função de expressão: NÃO sofre hoisting utilizável
try {
  console.log(ehMaiorDeIdadeExpressao(20)); // erro!
} catch (erro) {
  console.log(`${erro.name}: ${erro.message}`);
  // Motivo: a declaração const é "elevada", mas fica na Temporal Dead Zone
  // até a linha em que é inicializada; a função só existe depois dela.
}

const ehMaiorDeIdadeExpressao = function (idadePessoa) {
  return idadePessoa >= 18;
};

console.log('Expressão (depois da declaração): 20 anos ->', ehMaiorDeIdadeExpressao(20));

// 2.3 Função dobro nas três formas
function dobro(n) {                      // declarada
  return n * 2;
}

const dobroExpressao = function (n) {    // expressão
  return n * 2;
};

const dobroArrow = (n) => n * 2;         // arrow function (forma curta)

console.log('dobro (declarada)  :', dobro(4));
console.log('dobro (expressão)  :', dobroExpressao(4));
console.log('dobro (arrow)      :', dobroArrow(4));

// 2.4 Parâmetro com valor padrão
const dobroPadrao = (n = 1) => n * 2;
console.log('dobroPadrao(5)  :', dobroPadrao(5));  // 10
console.log('dobroPadrao()   :', dobroPadrao());   // 2 (usa n = 1)

/* ==========================================================
   BLOCO 3 – CONTROLE DE FLUXO
   ========================================================== */
titulo('BLOCO 3 – Controle de Fluxo');

// 3.1 if / else
function classificarNota(nota) {
  if (nota >= 6) {
    return 'Aprovado';
  } else {
    return 'Reprovado';
  }
}
console.log('Nota 7.5 ->', classificarNota(7.5));
console.log('Nota 6   ->', classificarNota(6));
console.log('Nota 4   ->', classificarNota(4));

// 3.2 switch com semáforo
const corSemaforo = 'amarelo';
switch (corSemaforo) {
  case 'vermelho':
    console.log('Pare');
    break;
  case 'amarelo':
    console.log('Atenção');
    break;
  case 'verde':
    console.log('Siga');
    break;
  default:
    console.log('Cor inválida');
}

// 3.3 Tabuada do 5 com for
console.log('\nTabuada do 5:');
for (let i = 1; i <= 10; i++) {
  console.log(`5 x ${i} = ${5 * i}`);
}

// 3.4 Contagem regressiva com while
console.log('\nContagem regressiva:');
let contagem = 5;
while (contagem >= 1) {
  console.log(contagem);
  contagem--;
}

// 3.5 Par ou ímpar de 1 a 20: com for e com while
console.log('\nPar ou ímpar (for):');
for (let n = 1; n <= 20; n++) {
  console.log(`${n} é ${n % 2 === 0 ? 'par' : 'ímpar'}`);
}

console.log('\nPar ou ímpar (while):');
let numero = 1;
while (numero <= 20) {
  console.log(`${numero} é ${numero % 2 === 0 ? 'par' : 'ímpar'}`);
  numero++;
}

// 3.6 diaDaSemana com switch
function diaDaSemana(numeroDia) {
  switch (numeroDia) {
    case 1: return 'Domingo';
    case 2: return 'Segunda-feira';
    case 3: return 'Terça-feira';
    case 4: return 'Quarta-feira';
    case 5: return 'Quinta-feira';
    case 6: return 'Sexta-feira';
    case 7: return 'Sábado';
    default: return 'Número inválido (use de 1 a 7)';
  }
}

console.log('\nDias da semana:');
[1, 4, 7, 0, 8].forEach((d) => console.log(`${d} -> ${diaDaSemana(d)}`));
