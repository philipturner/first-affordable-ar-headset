# Creating the World's First Affordable AR Headset Experience

![Google Cardboard plus AR](/Google_Cardboard_plus_AR.webp)

With the [AR MultiPendulum](https://apps.apple.com/app/ar-multipendulum/id1583322801) app, I created the world's first AR headset experience that does not rely on expensive specialized hardware. Using Google Cardboard, a standard iPhone, and images acquired using the phone's camera, the app creates an AR headset experience by rendering the user's surroundings in VR. To do this, I combined energy-efficient techniques for real-time hand tracking and scene color reconstruction to create an immersive user experience.

## Introduction

Augmented reality (AR) is a technology that overlays virtual objects over the real world. For years, AR experiences have been available on smartphones through handheld AR apps. In 2016, Pokemon Go popularized AR, overlaying virtual characters on a map of the world. Beyond that, AR has only played a minor role in the average person's life, being used for a few occasional tasks such as measuring objects or [testing out furniture](https://www.architectmagazine.com/technology/ikea-launches-augmented-reality-application_o).

A year before the release of Pokemon Go, Microsoft released [Hololens](https://www.microsoft.com/en-us/hololens), a $3000 AR headset that presents holograms by reflecting light into the user's eyes. Unlike VR headsets, Hololens allows users to see their surroundings while viewing virtual content and interacting using their hands instead of a controller. After releasing Hololens, Microsoft published demos of a wide variety of use cases, and the demo of Minecraft [went viral](https://www.polygon.com/2015/6/17/8788943/hololens-minecraft-demo). Minecraft was familiar to many people, and AR's promise of interaction and immersion meshed perfectly with the game. For example, users could interact with a Minecraft world using intuitive hand gestures, allowing them to experience creating buildings in Minecraft in ways that were not possible before. Despite all of the attention it received, Microsoft never turned the demo into an app. After 2015, Microsoft shifted its focus on Hololens from consumer applications to the corporate enterprise environment, and its price remains at thousands of dollars to this day. 

In the industries that utilize it, Hololens brings game-changing opportunities to improve productivity and even save lives. In hospitals, Hololens helps [surgeons train](https://news.microsoft.com/en-gb/2018/02/08/surgeons-use-microsoft-hololens-to-see-inside-patients-before-they-operate-on-the) for high-risk surgeries. By interacting with detailed 3D models of the human body, surgeons can run through the steps of surgery and learn from mistakes in an environment that will not endanger a patient's life. If Hololens were cheaper, it might allow first responders to provide more forms of life-saving assistance to people at the site of an emergency.

In the mid-2020s, AR headset technology is expected to go mainstream through smart glasses that cost as much as a smartphone. Smart glasses have been in development for several years. However, their small size presents a massive hurdle that has never been overcome. Hololens can be [large and bulky](https://www.theverge.com/2019/2/24/18235460/microsoft-hololens-2-price-specs-mixed-reality-ar-vr-business-work-features-mwc-2019) because it is used in specialized environments, where form factor is not a concern. Unlike Hololens, smart glasses must fit a processor, light projectors, and a battery into the same footprint as a glasses frame while lasting for several hours under a typical workload. To conserve energy, smart glasses might offload most of their computations to a paired smartphone.

## Contents

- [Background](#background)
  - [MultiPendulum](#multipendulum)
  - [Augmented Reality](#augmented-reality)
  - [First Applications](#first-applications)
- [Method](#method)
  - [The Challenge of Hand Reconstruction](#the-challenge-of-hand-reconstruction)
  - [Shifting Away from LiDAR](#shifting-away-from-lidar)
  - [Creating AR MultiPendulum](#creating-ar-multipendulum)
  - [Preparing for Release](#preparing-for-release)
- [Discussion](#discussion)
- [Conclusion](#conclusion)

## Background

### MultiPendulum

In late 2019, I was fascinated by the double pendulum, a physics simulation with chaotic motion. This motion is unpredictable yet fluid and aesthetically pleasing. I wondered what it would be like to experience a simulation with three or more pendulums, more complex behavior, and no damping (a form of friction that causes the simulation to slow down and eventually halt).

Since my programming skills allowed me to bring a frictionless multi-pendulum simulation into reality, I challenged myself to create it. When researching the physics behind the simulation, I could not understand much of the math terminology and formulas. So, I went on an accelerated self-study course. I absorbed several years of math and physics course material in less than a month, using Khan Academy and a free electronic textbook. After this, I created an algorithm that simulates up to 100 pendulums without damping. A year later, right before starting work on AR MultiPendulum, I would publish the simulation [online](https://github.com/philipturner/multipendulum) for free.

After finishing my original multi-pendulum simulation, I began exploring 3D graphics. I downloaded a computer graphics textbook, read online software documentation, and followed a tutorial on OpenGL, a low-level framework for rendering 3D graphics. When experimenting with OpenGL in Xcode 10, I learned that my 9-year-old iMac could not run Xcode 11. Then, I spent a week learning [Swift](https://swift.org/about), Apple's modern programming language that replaced Objective-C, but Xcode 10 could not run the newest version of Swift. Frustrated, I bought a new Mac Mini to gain access to both Xcode 11 and Swift.

With the newest version of Xcode, I gained practical experience with creating iOS apps. I attempted to learn [Metal](https://developer.apple.com/metal), a low-level 3D graphics framework that replaced OpenGL. However, I could not understand Apple's guides and sample code. I had just invested weeks learning Swift, yet all of the sample code was in Objective-C. After translating most of Apple's Metal sample code from Objective-C to Swift, I still did not understand it. I gave up on learning Metal and tried [Unity](https://unity.com) and [Unreal Engine](https://www.unrealengine.com) (high-level frameworks that are much easier to learn and more beginner-friendly). However, I was not satisfied with the direction of any of my work in 3D graphics.

### Augmented Reality

At the iPhone 12 event in October 2020, Apple was rumored to be unveiling its AR smart glasses ([Smith, 2020](https://bgr.com/tech/apple-ar-glasses-specs-and-price-to-be-unveiled-during-iphone-12-event)). I had been eagerly awaiting Apple's smart glasses for years and suspected that Apple would release new tools to prepare software developers for working with smart glasses after their announcement, but this did not happen. I became unsatisfied with waiting for Apple to release an affordable AR headset.

With my knowledge as a software developer, I decided to create an AR headset experience myself. I repurposed the [Google Cardboard](https://www.cnet.com/reviews/google-cardboard-review) VR viewer (which turns a smartphone into a VR headset) and my iPhone to create an AR headset, providing an affordable alternative to Microsoft Hololens without waiting for Apple's AR smart glasses. By presenting a video of my surroundings in VR, I could overlay virtual objects and create an AR headset experience. Since neither Unity nor Unreal Engine provides enough flexibility to render a video in VR, my only choice was to learn Metal and make a custom game engine.

I started over with learning Metal and translated the Metal [sample code](https://developer.apple.com/metal/sample-code) from Objective-C to Swift twice. After finding an [online guide](https://metalkit.org/2017/07/29/using-arkit-with-metal) to using Metal for AR apps written in Swift, I created a simple app that presented a video stream from AR as a flat rectangle in VR. After experiencing this initial attempt at creating an AR headset, I was disappointed that I could not interact with virtual objects. I would have to build on this foundation before I could share it with others.

In November 2020, I bought an iPhone 12 Pro Max with a built-in LiDAR scanner—a game-changer for AR ([Wilson, 2020](https://www.techradar.com/news/what-is-a-lidar-scanner-the-iphone-12-pros-rumored-camera-upgrade-anyway)). Instead of just recording a video of my surroundings, my phone also recorded its 3D shape. This meant I could present the world as a 3D mesh instead of a flat rectangle in VR, making it look much more realistic and drastically improving the AR headset experience. 

Although I was making progress, there were significant problems with my AR headset experience. I could not interact with virtual objects through hand gestures (like Hololens or future smart glasses). In addition, presenting my surroundings in 3D removed all color, forcing me to outline the mesh as a wireframe to distinguish geometry.

### First Applications

By December 2020, I figured out how to render my surroundings as a 3D mesh in VR (called the "scene mesh"). I had also started working on a 3D hand reconstruction algorithm for interacting with virtual objects through complex hand gestures. In January 2021, I was assigned a lengthy, independent school project. I planned to create the first application for my work—a 3D modeling experience only possible on an AR headset. 

A week into the project, I realized that controlling virtual objects in an AR headset with two hands was impossible with my hand reconstruction algorithm (I would later switch to one hand in AR MultiPendulum and use a form of interaction that worked without LiDAR). In the end, I made a handheld AR app that could only be used on LiDAR-enabled devices. It was impressive, but my ultimate goal was to create several applications for my work. 

After the school project, I tackled the challenge of presenting the scene in color instead of as a wireframe mesh (scene color reconstruction). The raw 3D shape of the scene mesh had no color, not even grayscale. To make triangles visible, I previously had to outline their edges by rendering the mesh as a wireframe or color triangles based on their distance from the camera. My solution to this problem was the [first application](https://github.com/philipturner/scene-color-reconstruction) that tracks the color of a scene mesh in real-time.

In April 2021, I discussed my work with a technology marketing expert who advised me to focus on something more straightforward and user-friendly. To accomplish this, I went back to the multi-pendulum simulation I made a year ago. Rather than creating numerous apps, I needed to show people that an affordable AR headset experience is possible on a mobile device. So, I revised my original goal of creating a suite of independent apps and created one unified app built on my framework. The resulting app, AR MultiPendulum, provided a captivating example that demonstrated what my work brought to AR and could capture the attention of a larger audience.

## Method

### The Challenge of Hand Reconstruction

Although I could present my surroundings in VR and full color, an immersive AR experience requires interacting with virtual objects using hand motions. In iOS 14, Apple added a [hand detection algorithm](https://appleinsider.com/articles/20/06/24/apple-introduces-hand-body-pose-detection-to-vision-framework-for-developers) that scans images and recognizes the 2D position of every joint in a human hand. This algorithm can be repurposed to track the user's hand movements in an AR experience, allowing them to interact with virtual objects (like they would when wearing Hololens or smart glasses).

This algorithm was not designed for AR and consumed a massive amount of energy. Running it on every video frame (60 times per second) made an iPhone's processor extremely warm in minutes. iOS would minimize energy consumption by throttling the display's refresh rate from 60 to 30 times per second to prevent overheating. This broke the fluidity of the AR headset experience and increased the likelihood of the experience causing nausea. To prevent iOS from throttling the refresh rate, I ran the algorithm on every sixth video frame (10 times per second). Although doing so reduced the quality of hand tracking, I had arrived at a somewhat workable solution.

Since Apple's hand detection algorithm operates on a 2D image, it could not reconstruct a hand's 3D position or orientation. However, raw LiDAR data took the form of a depth image, which could be superimposed over the color image passed into the hand tracking algorithm. After receiving 2D positions of the joints in the user's hand, they could then be mapped to the depth image to create 3D positions. While this solution was promising, the hand's representation in the raw depth image did not always match the output of Apple's 2D hand detection algorithm, so joints often had incorrect depths. In addition, when one part of the hand blocked another part from the camera's view, depth was assigned incorrectly.

To account for the inaccuracy in joint depth, I made a heuristic that constrained the 3D joint positions to something that appeared like a human hand. In addition, I created a mechanism to increase the quality of hand reconstruction while reducing energy consumption. By measuring optical flow (how much an image changes over time), it could estimate the speed at which the hand was moving. If the hand was moving slowly, the mechanism skipped updates to the hand's position to conserve energy. It could sample as high as 20 times per second for short periods and fall to as low as 2.5 times per second when the hand was absent.

After creating a moderately successful 3D hand reconstruction algorithm, I tried using it to replicate the experience of using "The Force" from Star Wars. I could select and attract or repel virtual objects by pointing my hand toward an object and opening or closing my fingers. However, this form of interaction was challenging to use because the hand reconstruction was still not precise. This was a significant setback in my aspiration to replicate the experience of using Hololens or smart glasses. To provide an interactive experience on Hololens, Microsoft created [advanced algorithms](https://www.immersiv.io/blog/hands-on-hololens-2-review) that could track the user's hand in 3D with extreme accuracy. I had neither the time nor the expertise to create those algorithms from scratch. I decided to set aside the challenge of precise hand reconstruction and move on.

### Shifting Away from LiDAR

My failure to use hand reconstruction for precise 3D interactions made me shift my focus in a more realistic direction. For months, I had created software that only ran on LiDAR-enabled devices. If I had published an app in July 2021, it would only be available to people with the latest iOS devices. This would defeat my goal of making AR headset experiences accessible to the general public before the release of smart glasses.

In addition, I realized that my current AR headset software could also enhance handheld AR experiences. Most people with iPhones did not have Google Cardboard, so releasing an app that only provided an AR headset experience would narrow the number of individuals who could experience my work. Moving forward, I focused on designing my AR software to function without LiDAR-enabled features and provide handheld experiences that complemented headset experiences. However, scene color and hand reconstruction would still be available on devices with a built-in LiDAR scanner.

### AR MultiPendulum

After setting myself on the right path, I began rendering the multi-pendulum simulation in AR. To make the simulation's motion appear smooth when moving quickly, the simulation was rendered at several nearby positions called *keyframes*, recorded at slightly different times. When the number of keyframes was large, the GPU (graphics processing unit) was overloaded with geometry, resulting in *stuttering*, a phenomenon where the app freezes for a fraction of a second. To overcome this, I made an algorithm that combined geometry from adjacent keyframes and reduced the computational burden of rendering pendulums to prevent stuttering.

The algorithm took up to a millisecond to operate on the CPU (central processing unit). If the CPU was overloaded with other work, this algorithm's long execution time could cause stuttering. A CPU runs a small number of *threads* (workers that perform one computation at a time), while on a GPU, thousands of threads run simultaneously to provide a massive amount of processing power. To speed up the algorithm for combining geometry, I ran it on the GPU instead of the CPU.

Initially, each pendulum was assigned to one thread, resulting in a small number of threads and underutilizing the GPU's processing power. To increase the number of threads, each pendulum was assigned to a *thread group*, a small group of threads that can communicate with each other. By dividing large computations among multiple threads, a thread group processed a pendulum more quickly than an individual thread did.

A holographic interface was necessary to allow users to interact with the simulation and replicate an AR headset experience. To create that, I had to render text in 3D, which was difficult. Traditionally, text objects are rendered by referring to a bitmap (an image where pixels are either on or off). Using this approach in 3D pixelates the outlines of letters, creating jagged edges that cannot be cleaned up with standard antialiasing techniques.

To solve pixelated edges, letters' outlines must be slightly blurred. To achieve a visually appealing form of blurring, text must be rendered using a signed distance field instead of a bitmap. I referred to an [online tutorial](https://metalbyexample.com/rendering-text-in-metal-with-signed-distance-fields) to generate signed distance fields, but made them more accurate and generated them on the GPU instead of the CPU.

### Preparing for Release

Before August 2021, my app only worked on an iPhone 12 Pro Max. It required the full capabilities of the phone's A14 GPU, and I had to hard-code my iPhone's physical measurements into code that rendered the AR headset experience. To allow my app to work on other devices, I revised my code to calculate a device's physical measurements at runtime. In addition, I compensated for the lack of features on the GPUs found in older devices (i.e., variable rasterization rate and vertex amplification) by creating two versions of several shaders (GPU programs)—one for devices with or without a specific capability.

In addition to compatibility issues, I faced several bugs with rendering pendulums when running my app on older devices. To overcome this, I avoided using thread groups on old devices, which had the side effect of making some GPU code run more slowly. Although this is not ideal, it provided a solution for expanding compatibility with a broader range of devices.

While profiling my app, I found a bottleneck in the process of scene color reconstruction. Every time the scene mesh changed, all of its color data was copied, which took multiple frames to complete and caused stuttering. So, I rewrote GPU code for processing color in the surrounding scene. The new code managed color data more efficiently and avoided copying color data after every mesh update.

Next, I created a transparent holographic interface for controlling and customizing the multi-pendulum simulation. Having an interface in the AR display that a user can navigate through with hand motions was a critical component of my app. To tackle hand control, I arrived at a solution that uses the 2D positions generated by Apple's hand reconstruction algorithm and projects them as a 3D ray that intersects with the interface. While not elegant, the solution works. This unique experience replicates a vital part of an AR headset experience for people without Google Cardboard (most of the app's users).

## Discussion

On September 6, 2021, I released AR MultiPendulum on the [Apple App Store](https://apps.apple.com/app/ar-multipendulum/id1583322801). A week before that, I published the [source code](https://github.com/philipturner/ar-multipendulum) for my app to allow other software developers to start building apps using my work.

Presently, using my code is a tedious process because a developer must copy thousands of lines of code into their app. In addition, the copied source code will not update whenever my app updates. To solve these problems, I have to create a framework that developers can use to incorporate AR headset experiences into iOS apps. This framework, [ARHeadsetKit](https://github.com/philipturner/arheadsetkit), will be my next project.

My app currently only works on iPhones and iPads. It is not accessible to Android users. I hope to bring AR MultiPendulum to Android so that anyone with a smartphone can experience the software.

## Conclusion

The purpose of creating AR MultiPendulum was to raise awareness that AR headset experiences are now affordable to the general public through Google Cardboard. While my app does not deliver a fully authentic Hololens-esque AR experience, it allows people to interact with virtual objects in a simulated representation of their surroundings and better understand what AR is capable of. This experience is available to anyone with an iPhone 6S or later, with or without Google Cardboard (but I strongly encourage everyone to get Google Cardboard and try the fully immersive AR MultiPendulum experience).
