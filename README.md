# solutions
Pequenos trechos úteis de código

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
