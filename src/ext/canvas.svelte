<script>
    import canvasBg from '../assets/canvas.png';
    let cCard, cText;

    function redrawText() {
        const delay = Number(document.querySelector('#delay-rate > input[type="number"]').value);
        const fontSize = Math.min(Math.abs(+fontSizeInput.value || 120));
        const fontFamily = fontFamilyInput.value || 'sans-serif';

        // another canvas so making multiline text is easier
        lineCanvas.width = canvasText.width;
        lineCanvas.height = fontSize * 2.2;

        cCard.clearRect(0, 0, canvasText.width, canvasText.height);

        const value = (textInput.value || 'TAKE YOUR HEART').trim();
        const splitValue = value.split('\n');

        // they are all offset, just a different name and purpose
        let lineHeight = 0,
            middleOffset = 0,
            heightOffset = 0;
        let topOffset = Number(document.querySelector('#text-top').value);
        let timer = 0;

        splitValue.forEach(line => {
            setTimeout(() => {
                box = new BoxText(line, {
                    fontSize,
                    fontFamily
                });

                if (isMiddle) {
                    topOffset = 0;
                    middleOffset = ((canvasText.height - fontSize * splitValue.length) / 2.5) - (fontSize / 5 * (splitValue.length));
                }

                heightOffset += Number(box.draw(lineCanvas) - 40);

                cCard.drawImage(lineCanvas, 0, lineHeight + middleOffset + topOffset);

                lineHeight = Math.floor(heightOffset) || lineHeight;
                console.log(value, lineHeight, middleOffset, heightOffset);
            }, timer);
            timer += delay;
        });
    }

</script>

<!-- canvas -->
<div id="card-preview">
    <img src="{canvasBg}" id="canvas-bg" alt="Background canvas">
    <canvas id="canvas-card" bind:this="{cCard}" width="1770" height="1300"></canvas>
    <canvas id="canvas-text" bind:this="{cText}" width="1770" height="1300"></canvas>
</div>

<button id="refresh" class="action-btn"><i class="fa fa-refresh"></i>Refresh</button>

<style>
    #card-preview { 
        width: 60wv;
        height: 70vh;
        padding: 20px;
    }

    #card-preview>canvas {
        position: absolute;
        left: 50%;
        transform: translate(-50%, 7vh);
        height: 58vh;
        object-fit: cover;
        border: 1px solid black;
    }

    #canvas-bg {
        position: absolute;
        left: 50%;
        transform: translateX(-49.5%);
        height: 72vh;
    }

    button#refresh {
        position: relative;
        left: 50%;
        transform: translate(-50%);
    }

    @media screen and (max-width:767px),
    screen and (max-device-width:767px) {
        #card-preview {
            height: 45vh;
        }

        #canvas-bg {
            /* I'm sorry mobile users. */
            display: none;
        }

        #card-preview>canvas {
            object-fit: contain;
            height: 45vh;
        }

        button#refresh {
            margin-top: 60px;
        }
    }
</style>