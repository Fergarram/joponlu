<script>
import { setContext, onMount } from 'svelte';
import { v4 as uuidv4 } from 'uuid';

let stackId = uuidv4();
let cardStack = [];

setContext('cardStack', {
    addCard: (id) => {
        cardStack = [...cardStack, id];
        return cardStack.length - 1;
    },
    getStack: () => {
        return cardStack;
    },
    moveCard: (id) => {
        const index = cardStack.indexOf(id);
        cardStack.splice(index, 1);
        cardStack = [...cardStack, id];
        window.dispatchEvent(new Event(`cardmoved:${stackId}`));
    },
    addListener: (listener) => {
        window.addEventListener(`cardmoved:${stackId}`, listener);
    },
    removeListener: (listener) => {
        window.removeEventListener(`cardmoved:${stackId}`, listener);
    }
});
</script>

<slot></slot>