<script lang="ts">
	import SquareRoot from './../lib/icons/SquareRoot.svelte';
    import MultiplyIcon from "$lib/icons/Multiply.svelte";
    import SquareRootIcon from "$lib/icons/SquareRoot.svelte";
    import PercentIcon from "$lib/icons/Percent.svelte";
    import CEIcon from "$lib/icons/CE.svelte";
    import CIcon from "$lib/icons/C.svelte";
    import MinusIcon from "$lib/icons/Minus.svelte";
    import DivisonIcon from "$lib/icons/Divison.svelte";
    import DotIcon from "$lib/icons/Dot.svelte";
    import EqualsIcon from "$lib/icons/Equals.svelte";
    import AdditionIcon from "$lib/icons/Addition.svelte";

    function addToEquation(value:string){
        equation+=value;
    }

    function clear(){
        equation = "";
    }
    let squareRoot: string = '√ ';
    function calculateSquareRoot() {
    try {
      const result = Math.sqrt(eval(equation));
      equation = result.toString();
    } catch (error) {
    }
}
    function CE(){
        equation = equation.substring(0, equation.length-1)
    }
    function division(){
        equation = eval(equation)
    }
    function solve(){
        equation = eval(equation)
    }
    let equation: string ="";
</script>

<svelte:head>
    <title>آلة حاسبة</title>
</svelte:head>
<div
    class="bg-white h-fit w-fit rounded-3xl grid grid-cols-4 gap-2 p-6 font-semibold text-xl shadow-2xl"
>
    <div
        class="bg-blue-500 rounded-full text-white text-right col-span-4 h-12 flex items-center px-4 mb-2"
    >
        {equation}
    </div>
    <button on:click={() => addToEquation(' % 100 ')} class="bg-[#f2f6fc] hover:bg-[#f2f6fc]/50 ">
        <!-- % -->
        <PercentIcon />
    </button>
    <button on:click={() => calculateSquareRoot ()} class="bg-[#f2f6fc] hover:bg-[#f2f6fc]/50 ">
        <!-- Square root -->
        <SquareRootIcon />
    </button>

    <button on:click={CE} class="bg-[#f2f6fc] hover:bg-[f2f6fc]/50">
        <!-- CE -->
        <CEIcon />
    </button>

    <button on:click={clear} class="bg-[#232c5c] text-white hover:bg-[#232c5c]/50">
        <!-- C -->
        <CIcon />
    </button>

    <button on:click={() => addToEquation('7')}>7</button>
    <button on:click={() => addToEquation('8')}>8</button>
    <button on:click={() => addToEquation('9')}>9</button>
    <button on:click={() => addToEquation(' - ')} class="bg-[#f7425e] text-white hover:bg-[#f7425e]/50">
        <!-- Minus -->
        <MinusIcon />
    </button>

    <button on:click={() => addToEquation('4')}>4</button>
    <button on:click={() => addToEquation('5')}>5</button>
    <button on:click={() => addToEquation('6')}>6</button>

    <button on:click={() => addToEquation(' / ')} class="bg-[#2384fc] text-white hover:bg-[#2384fc]/50">
        <!-- Divison -->
        <DivisonIcon />
    </button>

    <button on:click={() => addToEquation('1')}>1</button>
    <button on:click={() => addToEquation('2')}>2</button>
    <button on:click={() => addToEquation('3')}>3</button>
    <button on:click={() => addToEquation(' x ')} class="bg-[#fcc707] text-white hover:bg-[#fcc707]/50">
        <MultiplyIcon />
    </button>
    <button on:click={() => addToEquation('. ')}>
        <DotIcon />
    </button>

    <button on:click={() => addToEquation('0')}>0

    </button>
    <button on:click={solve}>
        <EqualsIcon />
    </button>
    <button on:click={() => addToEquation(' + ')} class="bg-[#63dc74] text-white hover:bg-[#63dc74]/50">
        <AdditionIcon />
    </button>
</div>
