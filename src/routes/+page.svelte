<script lang="ts">		
	
 import Minus from "$lib/icons/Minus.svelte";
 import Divide from "$lib/icons/Divide.svelte";
 import Multy from "$lib/icons/Multy.svelte";
 import Plus from "$lib/icons/Plus.svelte";
 import Backspace from "$lib/icons/Backspace.svelte";

 
 let equation: string="";

  function addToEquation(value: string){
    equation+=value;
  }

  function backspace(){
    switch(equation.substring(equation.length-3,equation.length)){
        case " * ":
            case " + ":
                case " - ":
                    case " / ":
                    equation=equation.substring(0,equation.length-3);
                    break;
                    default:
                    equation=equation.substring(0,equation.length-1);
    }
 
  }

 function clear(){
    equation=""; 
 }

 function solve(){
    try{
        let answer = eval(equation);
        if(answer==undefined) throw SyntaxError;
        equation=answer;

    } catch(error){
        let output = document.getElementById('output')
        output?.classList.add('bg-red-400');

        setTimeout(()=> {
            output?.classList.remove('bg-red-400');
        }, 700);
    } 
 }

 function onkeyDown(e: KeyboardEvent){
    let button =document.getElementById(e.key);
    button?.click();
    button?.focus();
    setTimeout(()=> {
           document.activeElement?.blur();
        }, 500);


 }


</script>

<svelte:head>
    <title> Calculator </title>
</svelte:head>

<svelte:window on:keydown|preventDefult={onkeyDown}/>

    <div
     class=" bg-white h-fit w-fit rounded-3xl grid grid-cols-4  gap-1 p-6 font-semibold text-xl shadow-2xl max-w-[16rem] ">

        <div 
        id="output"
        class= "bg-slate-400  rounded-xl col-span-4 h-12 flex items-center px-4 mb-2  text-white  text-lg  overflow-x-auto  transition-all" >
            {equation}

        </div>

        <button id="Delete" on:click={clear} class="bg-slate-50  "> AC </button>

        <button id="Backspace" on:click={()=> backspace()} class="bg-slate-50 "> 
            <Backspace/>
        </button>

        <button id="%" on:click={()=> addToEquation(' / 100')} class="bg-slate-50"> % </button>

        <button id="+" on:click={()=> addToEquation(' + ')} class=" bg-lime-100  text-gray-600">  
            <Plus/>
         </button>

        
        
        <button id="7" on:click={()=> addToEquation('7')}> 7 </button>
        <button id="8" on:click={()=> addToEquation('8')}> 8 </button>
        <button id="9" on:click={()=> addToEquation('9')}> 9 </button>
        <button id="-" on:click={()=> addToEquation(' - ')} class="bg-violet-100  text-gray-600 "> 
            <Minus/>
        </button>

        <button id="4" on:click={()=> addToEquation('4')}> 4 </button>
        <button id="5" on:click={()=> addToEquation('5')}> 5 </button>
        <button id="6" on:click={()=> addToEquation('6')}> 6 </button>
        <button id="/" on:click={()=> addToEquation(' / ')} class="bg-rose-100  text-gray-600">  
          <Divide/>  
        </button>

        <button id="1" on:click={()=> addToEquation('1')}> 1 </button>
        <button id="2" on:click={()=> addToEquation('2')}> 2 </button>
        <button id="3" on:click={()=> addToEquation('3')}> 3 </button>
        <button id="*" on:click={()=> addToEquation(' * ')} class=" bg-sky-100  text-gray-600"> 
            <Multy/>
        </button>

        <button id="." on:click={()=> addToEquation('.')}> . </button>
        <button id="0" on:click={()=> addToEquation('0')}> 0 </button>
        <button id="=" on:click={()=> solve()} class="bg-slate-50 col-span-2"> = </button>
        


       
    </div>

    

