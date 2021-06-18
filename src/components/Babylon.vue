<template>
    <div id="canvas-container">
        <el-row>
            <el-button @click="addMesh">add mesh</el-button>
        </el-row>
        <canvas id="canvas"></canvas>
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
            this.engine = engine
            this.scene = scene
            this.camera = camera
            this.light = light
            this.primitives = []
            this.primitives.push(box)
            engine.runRenderLoop(() => {
                scene.render()
            })
            window.addEventListener('resize', () => {
                engine.resize()
            })
            window.addEventListener('mousewheel', () => {
                console.log(camera.position)
                console.log(camera.fov)
                console.log(camera.upVector)
                console.log(camera.minZ)
                console.log(camera.maxZ)
            })
        },
        addMesh () {
            // mesh
            const cmesh = new BABYLON.Mesh('custom', this.scene)
            const positions = [-5, 2, -3, -7, -2, -3, -3, -2, -3, 5, 2, 3, 7, -2, 3, 3, -2, 3]
            const indices = [0, 1, 2, 3, 4, 5]
            const vertexData = new BABYLON.VertexData()
            vertexData.positions = positions
            vertexData.indices = indices
            vertexData.applyToMesh(cmesh)
            // material
            const vmaterial = new BABYLON.StandardMaterial('vmaterial', this.scene)
            vmaterial.ambientColor = new BABYLON.Color3(1, 0, 0)
            // material to mesh
            cmesh.material = vmaterial
            this.primitives[0].isVisible = false
            cmesh.showBoundingBox = true
        }
    }
}
</script>
<style scoped>
#canvas-container {
    width: 100%;
    height: 100%;
}
#canvas {
    width: 100%;
    height: 100%;
}
</style>
