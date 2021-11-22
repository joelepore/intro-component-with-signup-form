<script>
    import { createEventDispatcher } from "svelte";
    import ValidationOutput from "./ValidationOutput.svelte";

    export let data;

    const dispatcher = createEventDispatcher();

    const validateTypeLetters = (inputValue) => {
        return !(inputValue.match('[0-9]+') !== null);
    }

    const validateTypeEmail = (inputValue) => {
        return (inputValue.match(/^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/) !== null );
    }

    const validateTypePassword = (inputValue) => {
        let strong = new RegExp("^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[!@#\$%\^&\*])(?=.{8,})");
        let medium = new RegExp("^(((?=.*[a-z])(?=.*[A-Z]))|((?=.*[a-z])(?=.*[0-9]))|((?=.*[A-Z])(?=.*[0-9])))(?=.{6,})");
        let validation = 1;

        if(strong.test(inputValue)){
            validation = 3;
        } else if (medium.test(inputValue)){
            validation = 2;
        }

        return validation;
    }

    const validate = (e) => {
        let inputValue = e.srcElement.value;
        
        switch(data.validation.type) {
            case 'letters':
                validation = validateTypeLetters(inputValue);
                break;
                case 'email':
                    validation = validateTypeEmail(inputValue);
                    break;
                    case 'password':
                        validation = validateTypePassword(inputValue);
                        break;
        }

        dispatcher('validated', {
            ...data,
            validation
        });
    }

    let validation;
</script>

<div class="w-full">
    <input on:input="{validate}" class="w-full py-3 px-5 text-sm border border-gray-400 border-opacity-50 rounded-md" type={data.type} placeholder="{data.placeholder}">
    <ValidationOutput type={data.validation.type} bind:validation={validation}/>
</div>