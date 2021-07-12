<script>
    let modal_is_active = "";
    let content_type;
    let image_src;
    let bitcoin_bpi;

    export async function command(action, value) {
        if (action == "open") {
            if (value == "type1") {
                const response = await fetch(
                    "https://dog.ceo/api/breeds/image/random"
                );
                let j = await response.json();
                image_src = j.message;
            } else if (value == "type2") {
                const response = await fetch(
                    "https://api.coindesk.com/v1/bpi/currentprice.json"
                );
                let j = await response.json();
                bitcoin_bpi = j.bpi;
            }
            // Show Now
            content_type = value;
            modal_is_active = "active";
        } else if (action == "close") {
            modal_is_active = "";
        } else if (action == "any command") {
        }
    }
</script>

<section class="modal {modal_is_active}">
    <div class="bg">
        <div class="window">
            <button class="close" on:click={() => command("close")}
                >CLOSE</button
            >
            <div class="content {content_type}">
                {#if content_type == "type1"}
                    <h2>DOG</h2>
                    <img src={image_src} alt="" />
                {:else if content_type == "type2"}
                    <h2>MONEY</h2>
                    <h3>BTC/USD</h3>
                    <p>{bitcoin_bpi.USD.rate}</p>
                    <div class="buttons">
                        <button on:click={() => command("close", "cancel")}
                            >CANCEL</button
                        >
                        <button on:click={() => command("close", "ok")}
                            >OK</button
                        >
                    </div>
                {/if}
            </div>
        </div>
    </div>
</section>

<style>
    section {
        position: fixed;
        left: 0;
        top: 0;
        display: none;
        width: 100%;
        height: 100%;
    }
    section.active {
        display: block;
    }
    .bg {
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.8);
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .window {
        width: 80vw;
        height: 80vh;
        background-color: rgba(150, 150, 150, 1);
        padding: 1em;
    }
    .window .close {
        position: absolute;
    }
    .window .content {
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
    .window .content.type1 img {
        max-width: 90%;
        max-height: 80%;
    }
</style>
