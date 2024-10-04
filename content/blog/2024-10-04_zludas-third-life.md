+++
title = "ZLUDA's third life"
date = 2024-10-04
+++


ZLUDA is back. For the last few months, I've been trying to find a commercial organization that would guarantee the continued development of the project. I am happy to announce that I have found one that is not only willing to fund further development, but also has an excellent vision for the future of ZLUDA.
I share their long-term vision and I can't wait to talk more about it. We don’t want to disclose everything just yet, but for now, we know that we want to make ZLUDA better. If you think ZLUDA is a cool project, we have even cooler projects in the works. Development has begun, and as soon as we have something to share, we will.
What I can talk about now is the current state and the direction of ZLUDA itself.

### Where we are now:
The code has been rolled back to the pre-AMD state and I've been working furiously on improving the codebase. I’ve been writing the improved PTX parser I always wanted and laid the groundwork for the rebuild. Currently, some very simple synthetic GPU test programs can be run on an AMD GPU, but we are not yet at the point where ZLUDA can support a full application.
 
### Where we are going:
* ##### The year of rebuild  
  The ultimate goal is to bring "new" ZLUDA to a similar state as before the rollback in one year (Q3 2025). "Similar state" is very subjective here. I don't have precise criteria, but an application of similar complexity should work just as well. Not every pre-rollback application will be supported again due to new priorities (more below).
 
* ##### Focus on machine learning  
  In the past, ZLUDA focused mainly on professional creator workloads. This meant focusing on applications like Arnold Render, Blender, 3DF Zephyr, etc. We even had a working prototype of GameWorks. While all of these workloads are important extremely satisfying to have running, machine learning workloads are in much higher demand. We are targeting for llm.c, llama.cpp, PyTorch, TensorFlow and others.  
  Additionally, HIP support for anything image-related is disappointing. The time saved by skipping layers of workarounds can be spent more productively writing more tests and enabling more applications.
 
* ##### Raytracing is gone  
  This is related to the previous point. Not many people realized it, but ZLUDA had an OptiX implementation. While ZLUDA-OptiX only supported just a handful of OptiX demos and simple Arnold scenes, it required a lot of code and broke all the time. Considering how underpowered it was and how much maintenance it required, it is a feature that is unlikely to ever come back.
 
* ##### GPU support  
  The new ZLUDA will be built to support multiple GPU architectures. The mainline development will happen on AMD GPUs as that's what most of our users have. Still, I do realize there is lot of interest in other GPUs (e.g. Intel) and hopefully this will lead to more code contributions and new backends.  
Pre-rollback ZLUDA stayed on ROCm 5 mainly because I did not want to re-test all the version-specific workarounds. Since we are starting with a clean slate, AMD backend will target ROCm 6.1+.
 
* ##### More modest set of supported AMD GPUs  
  We will only support RDNA1 and newer non-server AMD GPUs. Supporting pre-RDNA1 and server GPU architectures was an additional support burden and never worked as well as RDNA1+ GPUs due to the wavefront 64 configuration they use.  
  Note that this applies to the _current_ architectures. AMD recently announced the merging of RDNA and CDNA into a single architecture (UDNA). I have high hopes for this new architecture and expect it to simplify porting CUDA → HIP and to bring ZLUDA to server GPUs.
 
* ##### Downgraded Windows support  
  Windows will still work and be supported, it will just be less user-friendly. `zluda.exe` will be gone. Windows developers have invented several imaginative ways to load CUDA into a process. `zluda.exe` has tried to support all of them, and even succeeded. Most of the time.  
  As a user, you have to fashion some other way to load ZLUDA into the target process. Usually copying the ZLUDA binaries to the application is sufficient. We will provide ready-to-download Windows binaries.
 
* ##### Code improvements  
  The current ZLUDA code is not the worst, but there is clearly room for improvement. During its second life, ZLUDA was written as a proof-of-concept solution for closed-source graphics applications (Arnold, 3DF Zephyr, etc.). This had two important consequences. First, since we were only concerned with one-time proof, it was enough to enable an application once and move on to the next without worrying about regressions. Second, some floating-point operations were handled with too little (or too much) precision - if you are rendering a scene, you can probably live with some pixels being imperceptibly different shades of red.  
  Now that the concept has been thoroughly proven, ZLUDA will maintain application-level testing and more rigorously test for floating-point correctness (and document differences where strict compatibility is not possible).
 
* ##### Let’s talk  
  If you think there's not enough ZLUDA in your life, there's now a ZLUDA Discord channel [here](https://discord.gg/sg6BNzXuc7). Feel free to drop by and say hello.
I will also try to post development updates from time to time. I hope that learning about all the creative ways developers are abusing CUDA APIs will be as exciting as it is for me to implement them.
 
Of course, ZLUDA will remain open source. This means that any features that are not part of the plan are fair game if someone steps up and submits a pull request. Personally, I think there is no better way to express your undying love for your Radeon VII than to add support for it in ZLUDA.
 

