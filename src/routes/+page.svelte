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
    equation= eval(equation);
 }


</script>

<svelte:head>
    <title> Calculator </title>
</svelte:head>

    <div
     class=" bg-white h-fit w-fit rounded-3xl grid grid-cols-4  gap-1 p-6 font-semibold text-xl shadow-2xl max-w-[16rem] ">

        <div class= "bg-slate-400  rounded-xl col-span-4 h-12 flex items-center px-4 mb-2  text-white  text-lg  overflow-x-auto " >
            {equation}

        </div>

        <button on:click={clear} class="bg-slate-50  "> AC </button>

        <button on:click={()=> backspace()} class="bg-slate-50 "> 
            <Backspace/>
        </button>

        <button  on:click={()=> addToEquation(' / 100')} class="bg-slate-50"> % </button>

        <button on:click={()=> addToEquation(' + ')} class=" bg-lime-100  text-gray-600">  
            <Plus/>
         </button>

        
        
        <button on:click={()=> addToEquation('7')}> 7 </button>
        <button on:click={()=> addToEquation('8')}> 8 </button>
        <button on:click={()=> addToEquation('9')}> 9 </button>
        <button on:click={()=> addToEquation(' - ')} class="bg-violet-100  text-gray-600 "> 
            <Minus/>
        </button>

        <button on:click={()=> addToEquation('4')}> 4 </button>
        <button on:click={()=> addToEquation('5')}> 5 </button>
        <button on:click={()=> addToEquation('6')}> 6 </button>
        <button on:click={()=> addToEquation(' / ')} class="bg-rose-100  text-gray-600">  
          <Divide/>  
        </button>

        <button on:click={()=> addToEquation('1')}> 1 </button>
        <button on:click={()=> addToEquation('2')}> 2 </button>
        <button on:click={()=> addToEquation('3')}> 3 </button>
        <button  on:click={()=> addToEquation(' * ')} class=" bg-sky-100  text-gray-600"> 
            <Multy/>
        </button>

        <button on:click={()=> addToEquation('.')}> . </button>
        <button on:click={()=> addToEquation('0')}> 0 </button>
        <button on:click={()=> solve()} class="bg-slate-50 col-span-2"> = </button>
        


       
    </div>

    

