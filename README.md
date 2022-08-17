# solutions
###################################efeitos para filtros ###########################################################
myFilterMethod (node, filter) {
    node.name.includes(filter) ? this.blink(node.name) : console.log('object')
    return node.name.toLowerCase().includes(filter.toLowerCase())
  },
  blink (text) {
    const xpath = `//div[text()='${text}']`
    const matchingElement = document.evaluate(xpath, document, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue
    console.log('matchingElement', matchingElement)
    matchingElement.classList.add('animate__animated', 'animate__tada')
    setTimeout(() => {
      matchingElement.classList.remove('animate__tada')
    }, 1000)
  }
  .blinked {
  animation-duration: 2s;
  animation: blink 1s linear forwards;
}

@keyframes blink {
  0% {
    background-color: yellow;
  }
  50% {
    background-color: yellowgreen;
    transform: scale(1.5);
  }
  100% {
    background-color: transparent;
  }
}


Pequenos trechos úteis de código
//////////////////////////////////VALIDADOR CPF/CNPJ VUE///////////////////////////////////////////////SSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSSS
cpf (cpf) {
    cpf = cpf.replace(/\D/g, '')
    if (cpf.toString().length !== 11 || /^(\d)\1{10}$/.test(cpf)) {
      return false
    }
    let result = true;
    [9, 10].forEach(function (j) {
      let soma = 0, r
      cpf.split(/(?=)/).splice(0, j).forEach(function (e, i) {
        soma += parseInt(e) * ((j + 2) - (i + 1))
      })
      r = soma % 11
      r = (r < 2) ? 0 : 11 - r
      if (r !== cpf.substring(j, j + 1)) result = false
    })
    console.log(result)
    return result
  },
  validaCnpj (cnpj) {
    cnpj = cnpj.replace(/[^\d]+/g, '')
    console.log(cnpj.length)
    if (cnpj.length !== 14) { return false }

    // Elimina CNPJs invalidos conhecidos
    if (cnpj === '00000000000000' ||
      cnpj === '11111111111111' ||
      cnpj === '22222222222222' ||
      cnpj === '33333333333333' ||
      cnpj === '44444444444444' ||
      cnpj === '55555555555555' ||
      cnpj === '66666666666666' ||
      cnpj === '77777777777777' ||
      cnpj === '88888888888888' ||
      cnpj === '99999999999999') {
      return false
    }

    // Valida DVs
    let tamanho = cnpj.length - 2
    let numeros = cnpj.substring(0, tamanho)
    const digitos = cnpj.substring(tamanho)
    let soma = 0
    let pos = tamanho - 7
    for (let i = tamanho; i >= 1; i--) {
      soma += numeros.charAt(tamanho - i) * pos--
      if (pos < 2) { pos = 9 }
    }
    let resultado = soma % 11 < 2 ? 0 : 11 - soma % 11
    if (resultado !== digitos.charAt(0)) { return false }

    tamanho = tamanho + 1
    numeros = cnpj.substring(0, tamanho)
    soma = 0
    pos = tamanho - 7
    for (let i = tamanho; i >= 1; i--) {
      soma += numeros.charAt(tamanho - i) * pos--
      if (pos < 2) { pos = 9 }
    }
    resultado = soma % 11 < 2 ? 0 : 11 - soma % 11
    if (resultado !== digitos.charAt(1)) { return false }

    return true
  }



/////////////////////////////////////PUPPETEER////////////////////////////////////////////////

const puppeteer = require('puppeteer');
const readlineSync = require('readline-sync');


console.log('Bem vindo ao Bot conversor 🤖💰');



async function robo() {
  const browser = await puppeteer.launch({ headless: true });
  const page = await browser.newPage();
  const linguaBase = readlineSync.question('Informe uma lingua base: ') || 'português';
  const linguaFinal = readlineSync.question('Informe uma lingua desejada:') || 'inglês';

  const qualquerUrl = `https://www.google.com/search?q=tradutor+${linguaBase}+para+${linguaFinal}&sxsrf=ALeKk014ocPYlaGkEBv7yQ7esnJB-smI7w%3A1627486563237&ei=Y3kBYfbKDYrR1sQP24mY4AI&oq=tradutor&gs_lcp=Cgdnd3Mtd2l6EAMYATIHCCMQsAMQJzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQRxCwAzIHCAAQsAMQQ0oECEEYAFAAWABgxRloAXACeACAAYQBiAGEAZIBAzAuMZgBAKoBB2d3cy13aXrIAQrAAQE&sclient=gws-wiz`;
  await page.goto(qualquerUrl);
  // await page.screenshot({path: 'example.png'});



  const resultado = await page.evaluate(() => {
    document.getElementsByClassName('textarea').value = "Esse eh um valor de teste"
    return document.querySelector('.Y2IQFc').value;
  });

  console.log(`${resultado}`)
  await browser.close();
}

robo();



/*********************************************************PARES, IMPARES, CRESCENTES E DECRESCENTES*********************************************************************/
let totalItems = gets();
let items = [];

for (let i = 0; i < totalItems; i++) {
  items.push(parseInt(gets()));
}

const itensPares= items.filter((item)=>item%2==0)

let itensImpares= items.filter((item)=>item%2!=0)

var ordPar= itensPares.sort((current, next)=> current - next)
ordPar.forEach((element)=> console.log(element))
var ordImp= itensImpares.sort((current, next)=> next - current)
ordImp.forEach((element)=> console.log(element))

/*********************************************LISTA DE COMPRAS, CRESCENTES, DELEÇÃO DE ITENS DUPLICADOS******************************************************************************/

Desafio
Pedro trabalha sempre até tarde todos os dias, com isso tem pouco tempo tempo para as tarefas domésticas. Para economizar tempo ele faz a lista de compras do supermercado em um aplicativo e costuma anotar cada item na mesma hora que percebe a falta dele em casa.

O problema é que o aplicativo não exclui itens duplicados, como Pedro anota o mesmo item mais de uma vez e a lista acaba ficando extensa. Sua tarefa é melhorar o aplicativo de notas desenvolvendo um código que exclua os itens duplicados da lista de compras e que os ordene alfabeticamente.

Entrada
A primeira linha de entrada contém um inteiro N (N < 100) com a quantidade de casos de teste que vem a seguir, ou melhor, a quantidade de listas de compras para organizar. Cada lista de compra consiste de uma única linha que contém de 1 a 1000 itens ou palavras compostas apenas de letras minúsculas (de 1 a 20 letras), sem acentos e separadas por um espaço.

Saída
A saída contém N linhas, cada uma representando uma lista de compra, sem os itens repetidos e em ordem alfabética.

 
Exemplo de Entrada	Exemplo de Saída
2
carne laranja suco picles laranja picles
laranja pera laranja pera pera

carne laranja picles suco
laranja pera
// a função gets é implementada dentro do sistema para ler as entradas(inputs) dos dados
let totalItems = gets();

for (var i = 0; i < totalItems; i++) {
  let itens = gets();
  let itensOrdenados = itens.split(" ").sort();
 

  let itensUnicos = itensOrdenados.filter((element, count)=>{
     let first= itensOrdenados.indexOf(element)
    

    if(first===count){
        return element
    }
  });
  
    /*console.log(itensUnicos)
    console.log(i)
     var valor= itensUnicos[i]
     var index= itensUnicos.indexOf(valor)
      var ultimo= itensUnicos.lastIndexOf(valor) 
    
     if(index!=ultimo){
          console.log(i,valor, index, ultimo)
          itensUnicos.splice(ultimo, 1)
     }*/



  let resposta = [...itensUnicos].join(" ");
    console.log(resposta);
}
/***Valore Únicos usando SET of COLLECTIONS*******************

const myArray = [30, 30, 40, 5, 223, 2049, 3034, 5]

function valoresUnicos(arr){
	const mySet= new Set(arr)// setters are maps with an unic values
	return [...mySet]
}

console.log(valoresUnicos(myArray))
**************************************************************************/

/*********************************************************ORDENAMENTO CRESCENTE, CONTAGEM DE DADOS REPETIDOS****************************************************************/
let totalItems = gets()
let itens = []
let contaRepete = 0;
for(let index= 0; index < totalItems ; index ++){
  let novoDado = gets()
  itens.push(novoDado)
}

itens.sort((curr, next)=> curr - next)
let menor = itens[0]

let index=0 
while(index < itens.length){
  let primeiro= itens.indexOf(menor)
  let ultimo= itens.lastIndexOf(menor) 
  contaRepete = (ultimo+1) - primeiro
  console.log(menor + ' aparece ' + contaRepete + ' vez(es)')
  index= ultimo+1
  menor = itens[index]
}

//itens.forEach((item)=> console.log(item))


/*******************************************VOGAIS EXTRA-TERRESTRES- COMPARAÇÃO ENTRE UNIDADES DE 2 STRINGS E CONTAGEM*************************************************/
for(let indice = 0 ; indice < 3 ; indice ++){
  let vogais = gets()
  
  let frase = gets()
  
  let contaRepete = 0;
  
  for(let i= 0; i < vogais.length ; i ++){
    for(let j = 0 ; j < frase.length ; j++){
      if(vogais[i]===frase[j]){
        contaRepete = contaRepete + 1
      }
    }
  }
  
  console.log(contaRepete)
  
}
