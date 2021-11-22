<script>
    import FormInput from "../components/FormInput.svelte";
    import anime from 'animejs/lib/anime.es';
    import { onMount } from "svelte";

    let validatedForms = {};

    const formInputs = [
        {
            type: 'text',
            placeholder: 'First Name',
            validation: {
                required: true,
                type: 'letters',
            }
        },
        {
            type: 'text',
            placeholder: 'Last Name',
            validation: {
                required: true,
                type: 'letters',
            }
        },
        {
            type: 'text',
            placeholder: 'Email Address',
            validation: {
                required: true,
                type: 'email',
            }
        },
        {
            type: 'password',
            placeholder: 'Password',
            validation: {
                required: true,
                type: 'password',
            }
        },
    ];

    const onValidated = (e) => {
        validatedForms[e.detail.placeholder] = e.detail.validation; 
    }

    const finalValidation = () => {
        let notValidatedForms = formInputs.length - validatedForms.length;
        let validation = true;
        if(notValidatedForms > 0) {
            validation = false;
        } else {
            formInputs.forEach((form) => {
                validation = validation && validatedForms[form.placeholder];
                
            });
        }
        return validation;
    };

    let buttonHoverIn = (button) => {
        anime({
            targets: button.srcElement,
            duration: 300,
            scale: 1.06
        });
    };

    let buttonHoverOut = (button) => {
        anime({
            targets: button.srcElement,
            duration: 300,
            scale: 1
        });
    };

    let submitForm = (e) => {
        e.preventDefault();
        if(finalValidation()){
            anime({
                targets: 'div > form div > input',
                delay: anime.stagger(200),
                duration: 900,
                translateX: '200%',
                easing: 'easeInElastic'
            })
        } else {
            let invalidFormInputs = [];
            formInputs.forEach((item) => {
                if(!validatedForms[item.placeholder]) {
                    invalidFormInputs.push(document.querySelector(`input[placeholder='${item.placeholder}']`));
                }
            })
            anime({
                targets: invalidFormInputs,
                translateX: 3,
                direction: 'alternate',
                duration: 150,
                easing: 'easeInOutSine',
                loop: 4 
            })
        }
    }

    onMount(() => {
        anime({
            targets: 'div > header > h1',
            duration: 800,
            translateX: ['-200%', '0'],
            translateY: ['-400%', '0'],
            rotate: [90, 0],
            easing: 'easeOutElastic(1, 1)',
            delay: 200
        });

        anime({
            targets: 'div > form',
            right: ['-200%', 0],
            duration: 800,
            easing: 'easeOutElastic(1, 1)',
            delay: 200 
        });
        anime({
            targets: 'div > header > button',
            translateY: ['500%', 0],
            opacity: [0, 1],
            duration: 600,
            easing: 'easeOutElastic(1, 8)',
            delay: 300
        });
        anime({
            targets: 'div > form div > input',
            translateX: ['200%', 0],
            rotate: [20, 0],
            duration: 700,
            delay: anime.stagger(200, {start: 300}), 
            easing: 'easeOutElastic(1,1)'
        });

        anime.timeline({
            duration: 500,
            easing: 'easeOutElastic',
        }).add({
            targets: 'div > header > p',
            easing: 'linear',
            opacity: [0, 1],
            delay: 200
        }).add({
            targets: 'div > header > p',
            translateX: 5 
        });
    });
</script>

<div class="bg-custom-red py-10 px-5 grid gap-x-8 relative overflow:hidden lg:grid-cols-2 lg:py-36">
    <header class="max-w-xl mx-auto text-white text-center z-20 lg:text-left lg:max-w-xl lg:justify-self-end lg:mx-0">
        <h1 class="py-5 font-bold text-3xl leading-none md:text-5xl lg:text-6xl">
            Learn to 
            <span class="relative font-mono inline-block bg-black bg-opacity-20">
                code
                <div id="code-overlay" class="absolute h-full top-0 right-0 bg-custom-red">
                </div>
            </span> 
            by watching others
        </h1>
        <p class="mb-5 px-2 font-light md:text-lg lg:text-2xl lg:px-0">
            See how experienced developers solve problems in real-time. Watching scripted tutorials is great, 
            but understanding how developers think is invaluable. 
        </p>
        <button on:mouseenter="{buttonHoverIn}" on:mouseleave="{buttonHoverOut}"  class="px-9 py-4 my-5 text-sm bg-custom-blue border-b-8 border-black border-opacity-20 box-border rounded-md lg:text-base">
            <strong class="text-lg sm:text-2xl">
                Try it free 7 days 
            </strong>
            then $20/mo. thereafter
        </button>
    </header>

    <form class="max-w-lg mx-auto p-5 bg-white text-sm flex flex-col gap-3 border-b-8 border-black border-opacity-[0.06] rounded-lg z-20 relative lg:text-base lg:mx-0" action="/">
        {#each formInputs as input}
        <FormInput on:validated={onValidated} data={input}/>
        {/each}
        <button id="form-button" on:click="{submitForm}" class="py-3 px-5 font-semibold text-gray-50 uppercase bg-custom-green rounded-md border-b-4 border-green-500">Claim your free trial</button>
        <small class="px-3 text-center text-custom-grayishBlue">
            By clicking the button, you are agreeing to our 
            <a class="text-custom-red font-bold" href="/">
                Terms and Services
            </a>
        </small>
    </form>

    <div id="bg-pattern" class="absolute w-full h-full z-0" style="background-image: url(/assets/images/bg-intro-desktop.png);"></div>
</div> 


<style>
    :root {
        --animationTime: 6s;
        --cursorWidth: 5px;
    }
    #code-overlay {
        animation: type var(--animationTime) steps(1) infinite; 
    } 

    #code-overlay::after {
        content: '';
        position: absolute;
        animation: cursor var(--animationTime) steps(1) infinite;
        animation: cursorBlink 0.7s infinite ease-in-out;
        width: var(--cursorWidth);
        height: 100%;
        background-color: black;
    }

    #bg-pattern {
        animation: fadeIn 1.5s forwards;
    }

    #form-button {
        transition: .1s;
    }
    #form-button:hover {
        transform: translateY(5%);
        border-bottom-width: 8px;
    }

    @keyframes fadeIn {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }

    @keyframes type {
        0% {
            width: 100%;
        }
        10% {
            width: 75%;
        }
        20% {
            width: 50%;
        }
        30% {
            width: 25%;
        }
        40% {
            width: 0%;
        } 
        100% {width: 0%}
    }
    @keyframes cursor{
        0% {
            right: calc(100% - 0.125em);
            left: 0;
        }
        10% {
            right: calc(75% + 0.35em);
        }
        20% {
            right: calc(50% + 0.47em);
        }
        30% {
            right: calc(25% + 0.35em);
        }
        40% {
            right: calc(-0.125em);
        } 
        100% {
            right: calc(-0.125em)
        }
    }

    @keyframes cursorBlink {
        0% {
            background-color: currentColor;
        }
        100%{
            background-color: transparent;
        }
    }
</style>