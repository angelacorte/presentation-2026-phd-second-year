+++
title = "Toward a Collective Robotic Operating System"
description = "ACSOS 2026 PhD Symposium presentation"
outputs = ["Reveal"]
+++

{{< slide class="title-slide" transition="fade" >}}

<div class="title-layout">
<div class="title-copy">

<p class="eyebrow">PhD Symposium @ ACSOS 2026</p>

# Towards Collective Robotic Operating Systems through Aggregate Computing

<p class="author"><strong>Angela Cortecchia</strong><br>
Supervisor: Prof. Danilo Pianini <br>Co-supervisor: Prof. Mirko Viroli</p>

<p class="title-mail"><a href="mailto:angela.cortecchia@unibo.it">angela.cortecchia@unibo.it</a></p>

<img class="title-logo" src="images/DIP INFORMATICA-SCIENZA E INGEGNERIA_DISI_EN.svg" alt="Department of Computer Science and Engineering, University of Bologna">

</div>
<div class="title-visual">
<img src="images/drones_avoiding_formation.png" alt="A robot swarm reorganizing around obstacles">
</div>
</div>

---

{{< slide class="challenge-slide" transition="fade" >}}

<p class="eyebrow">The engineering problem</p>

# A swarm keeps changing while it operates

{{% multicol class="split wide-gap" %}}
{{% col class="copy-col" %}}

A robotic collective must pursue a **system-level goal** with only local views and
**no centralized point of coordination**.

<div class="challenge-list">
<p>Robots are heterogeneous: they move, fail, join, and leave</p>
<p>Connectivity and sensing change at runtime</p>
<p>Unsafe transients can cause physical damage</p>
</div>

<p class="takeaway">The collective needs runtime support, not only a coordination algorithm.</p>

{{% /col %}}
{{% col class="visual-col" %}}

<img class="hero-image" src="images/drones_changing-formation.png" alt="Drones changing formation around obstacles">

{{% /col %}}
{{% /multicol %}}

---

{{< slide class="aggregate-slide" transition="fade" >}}

<p class="eyebrow">Programming abstraction</p>

# One program for the whole collective

{{% multicol class="split" %}}
{{% col class="copy-col" %}}

<p class="today"><strong>Usually, each robot is programmed individually</strong> — a common example is ROS.
With hundreds of robots, that does not scale.</p>

With **Aggregate Computing** the collective is programmed as a whole, and the same
program runs decentralized on every device, which repeatedly:

1. senses local information;
2. exchanges data with its neighbors;
3. runs the same aggregate program;
4. acts on its local result.

<p class="takeaway">Local executions compose into a global behavior.</p>

{{% /col %}}
{{% col class="visual-col collective-visual" %}}

<img src="images/collective.svg" alt="Local device interactions producing collective behavior">

{{% /col %}}
{{% /multicol %}}

---

{{< slide class="gap-slide" transition="fade" >}}

<p class="eyebrow">Research gap</p>

# What is missing?

<div class="comparison">
<div class="comparison-side">
<h3>Classic Aggregate Computing applications</h3>
<p>One collective program, deployed once</p>
<ul>
<li>A single behavior runs on each device</li>
<li>No preemption, no lifecycle management</li>
<li>Self-stabilization guarantees recovery <em>eventually</em></li>
</ul>
</div>
<div class="comparison-divider" aria-hidden="true"></div>
<div class="comparison-side collective-side">
<h3>What a swarm mission needs</h3>
<p>Several behaviors, changing while the swarm flies</p>
<ul>
<li>Concurrent applications on the same devices</li>
<li>An authorized operator that can stop or switch them</li>
<li>Constraints that hold <em>during</em> the transient</li>
</ul>
</div>
</div>

<p class="takeaway centered">The runtime must support dynamic, safe, and authorized changes to the collective behavior.</p>

---

{{< slide class="vision-slide" transition="fade" >}}

<p class="eyebrow">PhD research vision</p>

# From Building Blocks to a Collective Robotic Operating System

<div class="vision-statement">
<p>Reusable set of mechanisms to manage collective behavior, towards an operating system-oriented architecture.</p>
</div>

<div class="os-map">
<div class="os-row">
<span class="os-cap">Resource management</span>
<span class="os-mean">Structures and resources grow where the collective needs them</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row">
<span class="os-cap">Monitoring</span>
<span class="os-mean">Collective state estimated from distributed, unreliable observations</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row">
<span class="os-cap">Adaptation</span>
<span class="os-mean">Tasks redistributed at runtime when a device is lost</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row">
<span class="os-cap">Consensus</span>
<span class="os-mean">Agreement between processes occupying different regions</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row">
<span class="os-cap">Safety</span>
<span class="os-mean">Physical constraints enforced while the collective is still moving</span>
<span class="os-state">investigated</span>
</div>
<div class="os-row open">
<span class="os-cap">Preemption &amp; lifecycle</span>
<span class="os-mean">Start, stop and switch collective processes without redeploying</span>
<span class="os-state">open</span>
</div>
<div class="os-row open">
<span class="os-cap">Permissions</span>
<span class="os-mean">Who is authorized to change the behavior of the collective</span>
<span class="os-state">open</span>
</div>
</div>

<p class="research-question">How can reusable runtime mechanisms keep collective behavior manageable while robots, goals, and networks change?</p>

---

{{< slide class="portfolio-slide" transition="fade" >}}

<div class="result-grid pair">
<figure>
<h2>Resource management</h2>
<img src="images/oneroot.gif" alt="FieldVMC structures growing and branching from local interactions">
<figcaption><strong>FieldVMC [1]</strong>
<span class="detail">Structures grow, branch and repair from a local flow of resources, with no global blueprint.</span>
<span class="detail alt">Resources are routed towards the most successful area of the network.</span>
</figcaption>
</figure>
<figure>
<h2>Adaptation</h2>
<img src="images/replanning.gif" alt="A swarm redistributing tasks after losing a robot">
<figcaption><strong>Runtime replanning [2]</strong>
<span class="detail">A mission is assigned to the swarm; when a robot is lost, its tasks are redistributed among the survivors.</span>
<span class="detail alt">The plan is repaired by the collective while it operates, without re-running a global planner.</span>
</figcaption>
</figure>
</div>

{{% footer %}}
[1] A. Cortecchia, G. Ciatto, R. Casadei, and D. Pianini, "FieldVMC: an asynchronous model and platform for self-organising morphogenesis of artificial structures". Complex Intell. Syst. 12(2) (2026)

[2] G. Aguzzi, M. Baiardi, A. Cortecchia, B. Miloradovic, A. Papadopoulos, D. Pianini, and M. Viroli, "A Field-Based Approach for Runtime Replanning in Swarm Robotics Missions". (ACSOS 2025)
{{% /footer %}}

---

{{< slide class="portfolio-slide" transition="fade" >}}

<div class="result-grid pair">
<figure>
<h2>Monitoring</h2>
<img src="images/dpf.gif" alt="Field-based distributed particle filtering tracking multiple targets">
<figcaption><strong>Field-based distributed particle filtering [3, 4]</strong>
<span class="detail">Several targets tracked from noisy observations, with observers that move and lose connectivity.</span>
<span class="detail alt">Where fusion happens, who leads, how far information travels: coordination is decoupled from the filtering logic, so it can be changed without redesigning the estimator.</span>
</figcaption>
</figure>
<figure>
<h2>Consensus</h2>
<img src="images/gossip.gif" alt="Self-stabilizing min-max gossip converging over a network">
<figcaption><strong>Self-stabilizing min&ndash;max gossip [5]</strong>
<span class="detail">The best value in the network wins, and the collective converges to it from any state.</span>
<span class="detail alt">Each message carries the path of nodes that acknowledged it: that is what lets stale contributions be pruned, which classical min&ndash;max gossip cannot do.</span>
</figcaption>
</figure>
</div>

{{% footer %}}
[3] A. Cortecchia, D. Domini, G. Ciatto, R. Casadei, D. Pianini and M. Viroli, "Flexible Distributed Particle Filtering for the Internet of Things via Aggregate Computing," (DCOSS-IoT 2026)

[4] A. Cortecchia, D. Domini, G. Ciatto, R. Casadei, and M. Viroli, "Multi-Target Tracking via Field-Based Distributed Particle Filtering" (ACSOS 2026)

[5] A. Cortecchia, D. Pianini, and M. Viroli, "Self-Stabilizing Min-Max Gossip for Aggregate Computing" (COORDINATION 2026)
{{% /footer %}}

---

{{< slide class="filter-slide" transition="fade" >}}

# A safety filter between collective strategy and actuation

<div class="layer-explainer">
<p><strong>Aggregate program</strong> &middot; computes the wanted behavior</p>
<p class="filtered"><strong>Safety filter</strong> &middot; refines it into a feasible command</p>
</div>

<div class="filter-layout">
<figure class="filter-diagram">
<img src="images/different-targets-plot.gif" alt="Robots reaching different targets while avoiding obstacles">
<figcaption><strong>Different goals while collaborating</strong></figcaption>
</figure>
<figure class="filter-demo">
<img src="images/follow-leader-plot.gif" alt="Robot clusters merging and following a common leader">
<figcaption><strong>One shared goal: follow the leader</strong></figcaption>
</figure>
</div>

{{% footer %}}
[6] A. Cortecchia, A. Papadopoulos, and D. Pianini "Toward Safe Aggregate Computing: A Distributed Control-Theoretic Safety Filter for Robot Swarms" (ACSOS-C 2026)
{{% /footer %}}

---

{{< slide class="open-slide" transition="fade" >}}

# Open challenges

<div class="comparison open-comparison">
<div class="comparison-side">
<h3>Preemption &amp; lifecycle</h3>
<p>Change what the collective runs, without redeploying it</p>
<ul>
<li><strong>Start, stop and switch</strong> collective behaviors while the swarm operates</li>
<li>Run <strong>several collective programs concurrently</strong> on the same devices</li>
<li>Today a program's lifecycle is <em>tied to the lifecycle of the devices</em></li>
<li>Aggregate processes are a first step: how a process <strong>expands and contracts in space</strong> is still open</li>
</ul>
</div>
<div class="comparison-divider" aria-hidden="true"></div>
<div class="comparison-side">
<h3>Users &amp; permissions</h3>
<p>Decide who may change the collective, and where</p>
<ul>
<li>Only <strong>authorized operators</strong> can alter the behavior of the swarm</li>
<li>Programs <strong>confined to a geographic area</strong>, while the devices keep moving</li>
<li>Requires a <em>user model</em> and permissions over collective behavior</li>
</ul>
</div>
</div>

<p class="takeaway centered warning">Mission-critical swarms need a lifecycle and an authority model, not only a coordination algorithm.</p>

---

{{< slide class="closing-slide" transition="fade" >}}

# Future work

<div class="closing-layout">
<div class="wrap-up single">

<div class="wrap-col next-col">
<ul class="closing-list">
<li class="tied">Combine spatial organization and safety: <strong>complex shapes that grow and move</strong> without unsafe transients;</li>
<li>Add the two missing building blocks: <strong>preemption and lifecycle</strong>, and <strong>permissions</strong> over collective behavior;</li>
<li>Integrate the mechanisms into a <strong>CROS prototype</strong> in Collektive.</li>
</ul>
</div>

</div>
<figure class="next-figure">
<img src="images/star-fieldvmc.png" alt="A star-shaped structure grown by FieldVMC in the Alchemist simulator">
<figcaption><strong>Shapes already grow</strong><span>next: moving them safely</span></figcaption>
</figure>
</div>

<p class="final-line">Make the swarm programmable as one system, while keeping its adaptation explicit and safe.</p>

<div class="closing-mark footer">
<img src="images/qr.png" alt="QR code linking to my personal portfolio">
<p>Personal portfolio</p>
</div>
