<script> 
    import './global.css';
    import Noticeboard from "./ext/noticeboard.svelte";
    import CanvasImage from "./ext/canvas.svelte"
    import { version } from './version.json';
    import logo from "./assets/icon.png";
</script>

<!-- main page -->
<div id="header">
    <div id="intro-icon">
        <img src="{logo}" alt="P5CC Logo">
    </div>
    <div id="intro-text">
        <h2>Persona 5 Calling Card Maker</h2>
        <p>For the sake of effortlessly making a calling card.<br>
            Sending your card to the darkest desire.</p>
    </div>
</div>
<hr>

<Noticeboard/>

<CanvasImage/>

<hr>

<!-- editor -->



<p id="version">v.<span>{version}</span> (<a href="https://github.com/skyventuree/p5cc/blob/main/CHANGELOG.md">See changelog</a>)</p>


<style>
    #header {
        display: grid;
        grid-template-columns: 40% 1fr;
        height: 100%;
    }

    #header > #intro-text {
        text-align: right;
        padding-right: 50px;
    }

    #header > #intro-icon > img {
        position: absolute;
        width: 20%;
        height: 0 auto;
        padding-left: 50px;
    }

    #version {
        font-size: 12px;
        text-align: center;
        padding-top: 10px;
    }
</style>
