---
layout: post
title: "Living on the Edge"
date: 2026-10-05
excerpt: "Why AI sometimes needs to run on the device itself, and my current research on keeping a small edge computer from overheating while it runs AI models."
image: /assets/images/edgeai/edgeai1.jpg
image_alt: "Data center servers on one side and a rover with an onboard edge AI processor on the other"
author: "Rohan Khetan"
---

We all use AI like ChatGPT and Gemini, right? First, think about how these chatbots work. Visualize it:

You ask ChatGPT a math question. ChatGPT doesn’t run the large language model locally on your computer. Your computer most likely doesn’t have the computing power needed to efficiently run a model that large. Instead, your question is sent from your computer to servers in a remote data center. These servers have enough computing power to run the model, generate a response, and send it back to you.

This is an example of how computers communicate with each other to get responses and get things done. Now picture this:

Massive earthquakes in a remote location. Rubble everywhere, buildings damaged, people hurt. It’s too dangerous for humans to complete the rescue mission all by themselves.

![A drone in a collapsed building detecting a survivor using an onboard edge AI processor](/assets/images/edgeai/edgeai3.jpg)

You deploy a robot to navigate the area and rescue victims. Your robot currently takes in visual input and sends that input to a remote server, asking where to move next and whether or not a detected object is a victim to be rescued. There are two huge flaws:

> **1. It’s a remote location!**<br>
> You might not have a reliable internet connection or the ability to communicate with an external server.

> **2. Latency!**<br>
> Even if you had a connection to a server, sending inputs to an external server and waiting for the server to send a response back takes time and increases latency. In crucial disaster-response situations, the robot needs to know what to do very quickly, so latency needs to be minimized.

![Comparison of a drone waiting on a cloud AI server and crashing versus a drone processing on-device and avoiding a falling tree](/assets/images/edgeai/edgeai2.jpg)

Because of these flaws, engineers use edge computing, where computation happens on or near the device itself rather than relying on a distant server. In our example, the robot could have its own edge computer, eliminating the need to constantly communicate with an external server and reducing latency.

![Traditional AI in server farms losing signal, versus a rover with its own edge AI processor](/assets/images/edgeai/edgeai1.jpg)

The pipeline gets simplified from:

**Input → Robot → Remote Server → Robot → Output**

to:

**Input → Robot/Edge Computer → Output**

Like everything in life, there are tradeoffs between options. Although using an edge computer is quicker and reduces the need for an external server, an edge computer usually is not as powerful as a huge data center. It has limited space, computing power, memory, and energy. You can’t exactly put a giant data center inside a rescue robot.

Because of this, engineers often use smaller and more efficient AI models on edge devices. They can reduce model size, lower numerical precision, or make other optimizations that allow AI models to run with fewer resources.

But there is another problem.

When running computationally heavy AI models, GPUs and CPUs consume power and generate heat. As the device gets hotter, it can eventually thermal throttle, meaning it intentionally slows itself down to prevent overheating and protect the hardware.

Now we have another tradeoff: we want our edge AI system to run as fast as possible, but pushing the hardware harder generates more heat, which can eventually cause the system to slow itself down.

This is where my current research comes in.

I’m working with an NVIDIA Jetson Orin Nano, a small edge computer designed to run AI models locally. My research looks at whether we can recognize when an edge AI system is heading toward overheating and proactively adapt before it has to thermal throttle.

For example, if the system is starting to get too hot, could we temporarily switch to a smaller AI model? Could we use lower-precision calculations through quantization? Could we process fewer video frames per second? Then, once conditions improve, could we increase performance again?

The goal is not simply to keep the computer cool. It’s to figure out when and how much to adapt so that we can get as much sustained AI performance as possible from a small device without pushing it past its limits.

That’s what I’m currently experimenting with—and there are a lot of questions I still want to answer.

<span style="font-weight: 600;">Turns out, living life on the edge is a balancing act.</span>
