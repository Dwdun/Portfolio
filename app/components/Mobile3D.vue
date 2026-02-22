<template>
  <div ref="container" class="w-full h-full cursor-grab active:cursor-grabbing"></div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, watch } from 'vue'
import * as THREE from 'three'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
import { useMouse } from '@vueuse/core'

const props = defineProps<{
  modelPath?: string,
  scale?: number
}>()

const emit = defineEmits<{
  (e: 'move', data: { x: number, y: number }): void
}>()

const container = ref<HTMLElement | null>(null)
let scene: THREE.Scene, camera: THREE.PerspectiveCamera, renderer: THREE.WebGLRenderer
let model: THREE.Group | null = null
let animationId: number

const { x, y } = useMouse()
const targetRotation = { x: 0, y: 0 }
const currentRotation = { x: 0, y: 0 }

const init3D = () => {
  if (!container.value) return

  // Scene
  scene = new THREE.Scene()
  
  // Camera
  camera = new THREE.PerspectiveCamera(45, container.value.clientWidth / container.value.clientHeight, 0.1, 100)
  camera.position.z = 5

  // Renderer
  renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true })
  renderer.setSize(container.value.clientWidth, container.value.clientHeight)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  container.value.appendChild(renderer.domElement)

  // Lighting
  const ambientLight = new THREE.AmbientLight(0xffffff, 2)
  scene.add(ambientLight)
  
  const directionalLight = new THREE.DirectionalLight(0xffffff, 3)
  directionalLight.position.set(5, 5, 5)
  scene.add(directionalLight)

  // Load Model
  const loader = new GLTFLoader()
  loader.load(props.modelPath || '/assets/3d/handphone_3d_model/scene.gltf', (gltf) => {
    model = gltf.scene
    
    // Center model
    const box = new THREE.Box3().setFromObject(model)
    const center = box.getCenter(new THREE.Vector3())
    model.position.x += (model.position.x - center.x)
    model.position.y += (model.position.y - center.y) - 0.5 // Shift it slightly down to avoid top cut off
    model.position.z += (model.position.z - center.z)

    const scale = props.scale || 1
    model.scale.set(scale, scale, scale)
    scene.add(model)
  })

  // Resize handler
  window.addEventListener('resize', onWindowResize)

  // Start loop
  animate()
}

const onWindowResize = () => {
  if (!container.value) return
  camera.aspect = container.value.clientWidth / container.value.clientHeight
  camera.updateProjectionMatrix()
  renderer.setSize(container.value.clientWidth, container.value.clientHeight)
}

const animate = () => {
  animationId = requestAnimationFrame(animate)

  if (model) {
    // Smooth interpolation (lerp)
    currentRotation.x += (targetRotation.x - currentRotation.x) * 0.05
    currentRotation.y += (targetRotation.y - currentRotation.y) * 0.05

    // Apply base rotation to show more of the screen continuously
    // The screen is usually on the +Z or -Z face depending on model. 
    // Usually, a slight Y rotation reveals the front. Let's add a base offset.
    const baseRotationY = -Math.PI * 0.1; // Rotate left slightly by default
    
    model.rotation.y = currentRotation.x + baseRotationY
    model.rotation.x = currentRotation.y
    
    // Add slow floating effect
    model.position.y = Math.sin(Date.now() * 0.002) * 0.1
  }

  renderer.render(scene, camera)
}

const handleMouseMove = () => {
  if (typeof window === 'undefined') return
  const normalizedX = (x.value / window.innerWidth) * 2 - 1
  const normalizedY = -(y.value / window.innerHeight) * 2 + 1
  
  targetRotation.x = normalizedX * Math.PI * 0.25 // max 45 degrees
  targetRotation.y = -normalizedY * Math.PI * 0.15 // max ~25 degrees

  // Emit normalized values for CSS metallic effect (-1 to 1 space)
  emit('move', { x: normalizedX, y: normalizedY })
}

watch([x, y], handleMouseMove)

onMounted(() => {
  init3D()
})

onBeforeUnmount(() => {
  cancelAnimationFrame(animationId)
  window.removeEventListener('resize', onWindowResize)
  if (renderer && container.value) {
    container.value.removeChild(renderer.domElement)
    renderer.dispose()
  }
})
</script>
