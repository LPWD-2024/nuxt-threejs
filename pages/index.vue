<script setup>
import * as THREE from 'three'

// Target ref with same name in template part
const canvas = ref(null)

let scene = null
let camera = null
let cube = null
let renderer = null
let animationId = null

const initScene = () => {
  // Init camera & scene
  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)

  // Init cube
  const geometry = new THREE.BoxGeometry(1, 1, 1)
  const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 })
  cube = new THREE.Mesh(geometry, material)

  // Update cube position
  cube.position.x = 1
  cube.position.y = -1

  // Update cube rotation
  cube.rotation.x = 2

  scene.add(cube)

  // Move camera away
  camera.position.z = 5

  // Set render
  renderer = new THREE.WebGLRenderer({ canvas: canvas.value })
  renderer.setSize( window.innerWidth, window.innerHeight )
}

const animate = () => {
  console.log('animation is running')
  animationId = requestAnimationFrame(animate)
  cube.rotation.x += 0.1
  renderer.render(scene, camera)
}

const onClick = () => {
  console.log('document clicked')
}

onMounted(() => {
  initScene()
  animate()
  document.addEventListener('click', onClick)
})

onBeforeUnmount(() => {
  cancelAnimationFrame(animationId)
  document.removeEventListener('click', onClick)
})
</script>

<template>
  <div class="p-index">
    <NuxtLink to="/test">Test</NuxtLink>
    <canvas ref="canvas" />
  </div>
</template>

<style lang="scss">

</style>
