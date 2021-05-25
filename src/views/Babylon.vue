<template>
<div>
    <canvas id="canvas">

    </canvas>
</div>
</template>

<script>
import * as BABYLON from 'babylonjs'
// import 'babylonjs-loaders'
export default {
    mounted () {
        this.init()
    },
    methods: {
        init () {
            const canvas = document.getElementById('canvas')
            console.log(BABYLON)
            const engine = new BABYLON.Engine(canvas, true)
            const scene = new BABYLON.Scene(engine)
            // BABYLON.SceneLoader.ImportMeshAsync('', 'https://assets.babylonjs.com/meshes/', 'box.babylon')
            const camera = new BABYLON.ArcRotateCamera('camera', -Math.PI / 2, Math.PI / 2.5, 3, BABYLON.Vector3.Zero(0, 0, 0), scene)
            camera.attachControl(canvas, true)
            console.log(camera)
            const light = new BABYLON.HemisphericLight('light', new BABYLON.Vector3(0, 1, 0))
            console.log(light.direction)
            const box = BABYLON.MeshBuilder.CreateBox('box', {})
            console.log(box.visibility)

            engine.runRenderLoop(() => {
                scene.render()
            })
            window.addEventListener('resize', () => {
                engine.resize()
            })
        }
    }
}
</script>
