<script>
    import { onMount, getContext } from 'svelte';
    import { v4 as uuidv4 } from 'uuid';

    export let x = 0;
    export let y = 0;
    export let width;
    export let resizable = true;
    export let title;

    let card;
    let cardId = uuidv4();
    let isDragging = false;
    let isTyping = false;
    let pos1 = 0, pos2 = 0, pos3 = 0, pos4 = 0;
    const { addCard, moveCard, addListener, getStack } = getContext('cardStack');

    const setPointerEventsFor = (element, option) => {
        element.style.pointerEvents = option;
    };

    const dragMouseDown = (e) => {
        pos3 = e.clientX;
        pos4 = e.clientY;
        let isDraggable = e.target.getAttribute('draggable') !== null;
        moveCard(cardId);

        document.onmousemove = (e) => {

            if (isDraggable) {
                pos1 = pos3 - e.clientX;
                pos2 = pos4 - e.clientY;
                pos3 = e.clientX;
                pos4 = e.clientY;
                let rect = card.getBoundingClientRect();
                card.style.transform = `translate3d(${(rect.left - pos1)}px, ${(rect.top - pos2)}px, 0)`;
                isDragging = true;
                setPointerEventsFor(card, 'none');
            }

        }

        document.onmouseup = (e) => {
            isDragging = false;
            setPointerEventsFor(card, 'initial');
            document.onmousemove = null;
            document.onmouseup = null;
        }
    }

    onMount(() => {
        let cardIndex = addCard(cardId);

        addListener(() => {
            cardIndex = getStack().indexOf(cardId);
            card.style.zIndex = cardIndex;
        });
    });
</script>

<article
    key={cardId}
    bind:this={card}
    class="window"
    style="transform: translate3d({x}px, {y}px, 0);"
    on:mousedown={dragMouseDown}
>
    <div class="title-bar" draggable>
        <span draggable>{title}</span>
        <button aria-label="close"></button>
    </div>
    <div
        class:resizable
        class="content"
        style="width: {width}px;"
    >
        <slot></slot>
    </div>
</article>

<style lang="scss">
    .title-bar {
        position: relative;
        height: 28px;
        background-color: white;
        background-image: url(../assets/classic.png);
        background-repeat: repeat-x;
        font-size: 14px;
        padding-top: 9px;
        padding-left: 1px;
        color: black;
        text-transform: uppercase
        // font-weight: 700;
        // border-top-left-radius: 5px;
        // border-top-right-radius: 5px;
    }

    button[aria-label=close] {
        position: absolute;
        width: 16px;
        height: 16px;
        top: 0;
        right: 6px;
        outline: none;
        border: none;
        background-image: url(../assets/close.png);
        cursor: pointer;
    }

    .window {
        position: absolute;
        left: 0;
        top: 0;
        background: white;
        // border: 1px solid black;
        // border-radius: 5px;
    }

    .content {
        border: 5px solid #03FCFF;
    }

    .resizable {
        width: fit-content;
        min-width: 181px;
        resize: both;
		overflow: auto;
        -webkit-overflow-scrolling: touch;
    }
</style>