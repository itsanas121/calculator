<script lang="ts">
    import SquareRoot from "./../lib/icons/SquareRoot.svelte";
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
    import { onMount } from "svelte";
    function addToEquation(value: string) {
        equation += value;
    }

    function clear() {
        equation = "";
    }
    let squareRoot: string = "√ ";
    function calculateSquareRoot() {
        try {
            const result = Math.sqrt(eval(equation));
            equation = result.toString();
        } catch (error) {}
    }
    function calculateExponential() {
        try {
            const result = Math.exp(eval(equation));
            equation = result.toString();
        } catch (error) {}
    }
    function CE() {
        switch (equation.substring(equation.length - 3, equation.length)) {
            case " + ":
            case " x ":
            case " - ":
            case " / ":
                equation = equation.substring(0, equation.length - 3);
                break;
            default:
                equation = equation.substring(0, equation.length - 1);
        }
    }

    function division() {
        equation = eval(equation);
    }
    function solve() {
        try {
            let answer = eval(equation);
            if (answer == undefined) throw SyntaxError;
            equation = answer;
        } catch (error) {
            let output = document.getElementById("output");
            output?.classList.add("bg-red-500", "shake-animation");
            setTimeout(() => {
                output?.classList.remove("bg-red-500", "shake-animation");
            }, 500);
        }
    }
    let equation: string = "";

    function onKeydown(e: KeyboardEvent) {
        let button = document.getElementById(e.key);
        button?.click();
        button?.focus();
        setTimeout(() => {
            // @ts-ignore
            document.activeElement?.blur();
        }, 100);
    }
    
    onMount(() => {
        let allButtons = document.getElementsByTagName('button');
        for (let i = 0; i < allButtons.length; i++) {
            allButtons[i].addEventListener('click', () => {
                new Audio('./click.mp3').play();
            });
        }
    });

    
</script>

<svelte:head>
    <title>آلة حاسبة</title>
</svelte:head>
<svelte:window on:keydown|preventDefault={onKeydown} />
<div
    class="bg-white h-fit w-fit rounded-3xl grid grid-cols-4 gap-2 p-6 font-semibold text-xl shadow-2xl max-w-[16rem]"
>
    <div
        id="output"
        class="bg-blue-500 rounded-xl text-white col-span-4 min-h-12 flex items-center px-4 mb-2 break-all"
    >
        {equation}
    </div>
    <button
        id="%"
        on:click={() => addToEquation(" % 100 ")}
        class="bg-[#f2f6fc] hover:bg-[#f2f6fc]/50"
    >
        <!-- % -->
        <PercentIcon />
    </button>
    <button
        id="sqrt"
        on:click={() => calculateSquareRoot()}
        class="bg-[#f2f6fc] hover:bg-[#f2f6fc]/50"
    >
        <!-- Square root -->
        <SquareRootIcon />
    </button>

    <button
        id="Backspace"
        on:click={CE}
        class="bg-[#f2f6fc] hover:bg-[f2f6fc]/50"
    >
        <!-- CE -->
        <CEIcon />
    </button>

    <button
        id="Delete"
        on:click={clear}
        class="bg-[#232c5c] text-white hover:bg-[#232c5c]/50"
    >
        <!-- C -->
        <CIcon />
    </button>

    <button id="7" on:click={() => addToEquation("7")}>7</button>
    <button id="8" on:click={() => addToEquation("8")}>8</button>
    <button id="9" on:click={() => addToEquation("9")}>9</button>
    <button
        id="-"
        on:click={() => addToEquation(" - ")}
        class="bg-[#f7425e] text-white hover:bg-[#f7425e]/50"
    >
        <!-- Minus -->
        <MinusIcon />
    </button>

    <button id="4" on:click={() => addToEquation("4")}>4</button>
    <button id="5" on:click={() => addToEquation("5")}>5</button>
    <button id="6" on:click={() => addToEquation("6")}>6</button>

    <button
        id="/"
        on:click={() => addToEquation(" / ")}
        class="bg-[#2384fc] text-white hover:bg-[#2384fc]/50"
    >
        <!-- Divison -->
        <DivisonIcon />
    </button>

    <button id="1" on:click={() => addToEquation("1")}>1</button>
    <button id="2" on:click={() => addToEquation("2")}>2</button>
    <button id="3" on:click={() => addToEquation("3")}>3</button>
    <button
        id="*"
        on:click={() => addToEquation(" * ")}
        class="bg-[#fcc707] text-white hover:bg-[#fcc707]/50"
    >
        <MultiplyIcon />
    </button>
    <button id="." on:click={() => addToEquation(". ")}>
        <DotIcon />
    </button>

    <button id="0" on:click={() => addToEquation("0")}>0 </button>
    <button on:click={() => addToEquation("**")}>^</button>

    <button
        id="-"
        on:click={() => addToEquation(" - ")}
        class="bg-[#63dc74] text-white hover:bg-[#63dc74]/50"
    >
        <AdditionIcon />
    </button>
    
    <button id="(" on:click={() => addToEquation("(")}>(</button>
    <button id=")" on:click={() => addToEquation(")")}>)</button>    
    <button class="w-full col-span-2" id="=" on:click={solve}>
        <EqualsIcon />
    </button>
</div>
