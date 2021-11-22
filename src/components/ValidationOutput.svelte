<script>
    export let type, validation;

    let message = '';
    let passwordMessage = '';
    let passwordMessageColor = '';

    if(type == 'letters') {
        message = 'This field must contain only letters.';
    } else if (type == 'email') {
        message = 'This email is not valid.';
    }

    $: {

        if (validation > 2) {
            passwordMessage = 'Strong';
            passwordMessageColor = 'custom-green';
        }else if (validation > 1){
            passwordMessage = 'Medium';
            passwordMessageColor= 'yellow-500';
        }else {
            passwordMessage = 'Weak';
            passwordMessageColor= 'red-500';
        } 

        let classes = [
            'bg-red-500',
            'bg-yellow-500',
            'text-red-500',
            'text-yellow-500',
            'text-custom-green'
        ]
    }
</script>

{#if validation == false || typeof(validation) == 'number'}
<div class="text-red-600 font-light">
    {#if type !== 'password'}
    <p class="py-2 text-sm">{message}</p>
    {:else}
    <div class="py-2 grid grid-cols-3">
        <div class="h-1 w-full bg-{passwordMessageColor} rounded-full flex col-span-2 self-center">
        </div>
        <p class="text-sm col-span-1 justify-self-end self-center text-{passwordMessageColor}">{passwordMessage}</p>
    </div>
    {/if}
</div>
{/if}