<template>
  <div>
    <p><span id="errorMsg"></span></p>
    <video id="webcam" autoplay="true" />
  </div>
</template>

<script lang="ts">
import {
    Vue,
    Component
} from 'vue-property-decorator'
import * as faceapi from 'face-api.js'
@Component
export default class WebCamFaceAPI extends Vue {
    private constraints = {
        audio: true,
        video: {
            width: 1280,
            height: 720
        }
    };

    async created() {
        try {
            const stream = await navigator.mediaDevices.getUserMedia(this.constraints)
            this.handleSuccess(stream)
        } catch (e) {
            // @ts-ignore
            document.querySelector('span#errorMsg').innerHTML = `navigator.getUserMedia error:${e.toString()}`
        }

    }
    // Success
    handleSuccess(stream: any) {
        // @ts-ignore
        document.getElementById('webcam').srcObject = stream
        const webcam = document.getElementById('webcam')
        // @ts-ignore

        webcam.addEventListener('play', async () => {
                // @ts-ignore
                const canvas = faceapi.createCanvasFromMedia(webcam)
                console.log('aqui')
                console.log(canvas)
                // @ts-ignore
                document.body.appendChild(canvas)
            })
    }
}  
</script>
