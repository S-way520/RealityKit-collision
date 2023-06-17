# RealityKit-collision
SwiftUI and RealityKit 
# The first part
![IMG_0161](https://github.com/S-way520/RealityKit-collision/assets/95877651/16d35ecd-1f37-40ef-b6ff-88f9a79cb175)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
import RealityKit
struct ContentView: View {
    var body: some View {
        ARViewContainer()
            .edgesIgnoringSafeArea(.all)
    }
}
struct ARViewContainer: UIViewRepresentable {
    func makeUIView(context: Context) -> ARView {
        let arView = ARView(frame: .zero)
        let anchorEntity = AnchorEntity(plane: .horizontal)
        
        let SphereEntity = ModelEntity(mesh: MeshResource.generateSphere(radius: 0.2/5), materials: [SimpleMaterial(color: .blue, isMetallic: true)])
        SphereEntity.physicsBody = PhysicsBodyComponent(massProperties: .default, material: .default, mode: .dynamic)//物理Physics
        SphereEntity.generateCollisionShapes(recursive: true)
        SphereEntity.position = simd_float3(0.2/2,0.8,0)
        
        let planeEntity = ModelEntity(mesh: MeshResource.generatePlane(width: 0.5, depth: 0.5, cornerRadius: 0.5), materials: [SimpleMaterial(color: .blue, isMetallic: false)])//[OcclusionMaterial()])
        planeEntity.physicsBody = PhysicsBodyComponent(massProperties: .default, material: .default, mode: .static)//物理Physics
        planeEntity.generateCollisionShapes(recursive: true)
        
        anchorEntity.addChild(SphereEntity)
        anchorEntity.addChild(planeEntity)
        arView.scene.addAnchor(anchorEntity)
        return arView
    }
    func updateUIView(_ uiView: ARView, context: Context) {
    }
}
```
