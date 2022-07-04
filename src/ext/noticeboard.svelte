{#if dialog}    
<div id="welcome-bg" bind:this="{noticeWindow}">
    <div id="welcome-content">
        <h2>Hey there!</h2>
        <p>I've rewritten (again) this page using Svelte. There is not much functionality change, but I hope this will speed things up a litte bit.</p>
        <p>Also did you know that Persona 5 is going to be on Nintendo Switch?</p>
        <iframe width="560" height="315" src="https://www.youtube.com/embed/4eKT3kseiAY" title="The Persona series is coming to Nintendo Switch" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media;" allowfullscreen></iframe>
        <hr>
        <p>View all version changelog by visit <a href="https://github.com/skyventuree/p5cc/blob/main/CHANGELOG.md">changelog</a>.</p>
        <p>Something happened? Have a suggestion? <a href="https://docs.google.com/forms/d/e/1FAIpQLSfuqntr1v4CW99VYnBIg-5yqX2Vony89CIaRuBrnBBeoI8n7A/viewform?usp=sf_link">Send it here!</a></p>
        <hr>
        <p>If you enjoy using this tool, please share it around on social media or to your friends. Thanks!</p>
        <!-- dismiss button -->
        <button on:click="{closeDialog}" class="full-btn">Okay!</button>
    </div>
</div>
{/if}

<script>
    import { version } from '../version.json';
    
    let noticeWindow, dialog = false;

    if (!document.cookie.includes('version')) document.cookie = `version=0;path=/`;

    const VCBOOL = /version=([^;]+)/.test(document.cookie) || false;
    const VCINFO = document.cookie.split(';').find(e => e.includes('version=')).split('=')[1];

    if (VCBOOL === false || VCINFO !== version) {
        console.warn('Version mismatch! Show update infomation.');
        document.cookie = `version=${version}; max-age=31536000`;
        dialog = true;
    }

    function closeDialog() {
        noticeWindow.style.display = "none";
    }
</script>

<style>
    #welcome-bg {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
        z-index: 5;
    }

    #welcome-content {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 70%;
        text-align: center;
        background-color: #FF0405;
        border: 10px solid black;
        padding: 10px;
        z-index: 10;
    }
    
    @media screen and (max-width:767px),
    screen and (max-device-width:767px) {
        #welcome-content {
            width: 90%;
        }
    }
</style>