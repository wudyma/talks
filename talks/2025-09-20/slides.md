---
layout: cover
highlighter: shiki
css: unocss
colorSchema: dark
transition: fade-out
mdc: true
title: DeepRTE v1.0.2
remoteAssets: true
seoMeta:
  ogImage: auto
---

# DeepRTE {.emphasis-primary.text-4xl}

<div text-2xl class="text-on-surface-variant">Pre-trained Attention-based Neural Network for Radiative Transfer</div>

<div mt15 />

<div flex="~ col gap-2">
  <div text-left text-2xl text-on-surface>Zheng Ma</div>
  <div text-left text-sm class="text-secondary">Shanghai Jiao Tong University</div>
  <div text-left text-sm class="text-on-surface-variant">Joint work with Min Tang and Yekun Zhu</div>
</div>

<!-- SJTU Official Logo - Enhanced Glassmorphism with Theme Colors -->
<div class="absolute top-6 right-6 group">
  <div class="relative bg-gradient-to-br from-white/40 to-white/25 dark:from-neutral-900/30 dark:to-neutral-800/20 backdrop-blur-lg rounded-xl p-2.5 border border-sjtu-200/15 dark:border-sjtu-400/8 shadow-lg shadow-sjtu-500/8 dark:shadow-sjtu-400/5 hover:bg-white/50 dark:hover:bg-neutral-900/40 hover:border-sjtu-300/20 dark:hover:border-sjtu-400/12 hover:shadow-sjtu-500/12 dark:hover:shadow-sjtu-400/10 transition-all duration-300">
    <!-- Logo with official SJTU colors -->
    <div class="relative z-10">
      <!-- Logo for light theme - using SJTU theme colors -->
      <div class="h-8 w-auto dark:hidden opacity-90 group-hover:opacity-100 transition-opacity duration-300 relative overflow-hidden">
        <img
          src="/images/sjtu-logo-zh.png"
          alt="Shanghai Jiao Tong University"
          class="h-8 w-auto filter brightness-0 opacity-0"
        />
        <div class="absolute inset-0 bg-sjtu-600" style="mask: url('/2025/shsiam/images/sjtu-logo-zh.png') no-repeat center/contain; -webkit-mask: url('/2025/shsiam/images/sjtu-logo-zh.png') no-repeat center/contain;"></div>
      </div>
      <!-- Logo for dark theme - using lighter SJTU theme colors -->
      <div class="h-8 w-auto hidden dark:block opacity-85 group-hover:opacity-95 transition-all duration-300 relative overflow-hidden">
        <img
          src="/images/sjtu-logo-zh.png"
          alt="Shanghai Jiao Tong University"
          class="h-8 w-auto filter brightness-0 invert opacity-0"
        />
        <div class="absolute inset-0 bg-sjtu-400" style="mask: url('/2025/shsiam/images/sjtu-logo-zh.png') no-repeat center/contain; -webkit-mask: url('/2025/shsiam/images/sjtu-logo-zh.png') no-repeat center/contain;"></div>
      </div>
    </div>
  </div>
</div>

<!-- Date positioned at bottom right with matching glassmorphism style -->
<div class="absolute bottom-8 right-6 group">
  <div class="relative bg-gradient-to-br from-white/40 to-white/25 dark:from-neutral-900/30 dark:to-neutral-800/20 backdrop-blur-lg rounded-lg px-3 py-1.5 border border-sjtu-200/15 dark:border-sjtu-400/8 shadow-lg shadow-sjtu-500/8 dark:shadow-sjtu-400/5 hover:bg-white/50 dark:hover:bg-neutral-900/40 hover:border-sjtu-300/20 dark:hover:border-sjtu-400/12 transition-all duration-300">
    <div text-xs class="text-on-surface-muted/80">September 20, 2025</div>
  </div>
</div>

---
glow: left
---

# Introduction

<div class="mb-6 text-center">
  <div class="text-2xl text-on-surface">
    <span class="emphasis-primary font-bold">Radiative Transfer</span> governs energy transport
  </div>
</div>

<div grid="~ cols-2 gap-6" mt-6>
  <GlassCard
    title="Inertial Confinement Fusion"
    subtitle="Clean energy generation"
    variant="primary"
    icon="i-ph-atom-duotone"
    size="md"
  >
    <div class="flex flex-col items-center gap-3">
      <img src="/icf.png" class="rounded-lg shadow-lg h-32 object-contain" />
      <div class="text-xs text-on-surface-variant text-center">
        Radiation transport drives implosion dynamics in fusion targets
      </div>
    </div>
  </GlassCard>

  <GlassCard
    title="Radiation Therapy"
    subtitle="Precision cancer treatment"
    variant="secondary"
    icon="i-ph-heart-duotone"
    size="md"
  >
    <div class="flex flex-col items-center gap-3">
      <img src="/rad-therapy.jpg" class="rounded-lg shadow-lg h-32 object-contain" />
      <div class="text-xs text-on-surface-variant text-center">
        Accurate dose calculation for effective treatment
      </div>
    </div>
  </GlassCard>
</div>

<div mt-6>
  <GlassCard variant="tech" text-center size="md">
    <div class="text-lg mb-2">
      <span class="emphasis-tech font-semibold">Central Challenge:</span>
      Numerical simulation of the <span class="emphasis-primary font-semibold">radiative transfer equation</span>
    </div>
    <div class="text-sm text-on-surface-variant">
      High-dimensional phase space • Complex collision operators • Multi-scale physics
    </div>
  </GlassCard>
</div>

---
glow: right
---

# Radiative Transfer Equation

<div class="mb-4">
  <GlassCard variant="primary" size="lg" py2>
  <div class="text-center mb-4">
  <div class="text-lg font-semibold text-on-surface mb-2">The governing equation</div>
  <div class="equation-block">

  $$
  \Omega \cdot \nabla I(r, \Omega) + \mu_t(r) I(r, \Omega) = \frac{\mu_s(r)}{S_{d-1}}\int_{\mathbb{S}^{d-1}} p(\Omega, \Omega^*) I(r, \Omega^*)\,\mathrm{d}\Omega^*
  $$

  </div>
  </div>
  <div class="grid grid-cols-2 gap-6 text-sm">
  <div>
  <div flex="~ gap-2 items-center">
  <strong>

  $I(r,\Omega)$:

  </strong>

  radiation intensity at phase space $(r,\Omega)$

  </div>
  <div flex="~ gap-2 items-center">
  <strong>

  $\mu_t(r)$:

  </strong>
  total cross section
  </div>
  </div>
  <div>
  <div flex="~ gap-2 items-center">
  <strong>

  $\mu_s(r)$:

  </strong>
  scattering cross section
  </div>
  <div flex="~ gap-2 items-center"><strong>

  $p(\Omega,\Omega^*)$:

  </strong>
  phase function
  </div>
  </div>
  </div>
  </GlassCard>
</div>

<div class="mt-0">
  <GlassCard title="Boundary Conditions" variant="secondary" size="md">
  <div class="text-center text-on-surface-variant">
  <div class="equation-block" flex="~ gap-2 items-center justify-center">

  $I |_{\Gamma_{-}}(r,\Omega) = I_{-}(r,\Omega)$

  where

  $\Gamma_{\pm} := \{(r,\Omega) \mid r\in\partial D,\;\Omega\in\mathbb{S}^{d-1},\;\mp n(r)\cdot\Omega<0 \}$

  </div>
  </div>
  </GlassCard>
</div>

---

# Numerical Challenges

<div class="mb-6 text-center">
  <div class="text-xl text-on-surface mb-2">
    <span class="emphasis-primary font-bold">Three Major Barriers</span> in Radiative Transfer Simulation
  </div>
</div>

<div grid="~ gap-6 cols-3" mt-6>

<GlassCard
  title="High Dimensionality"
  subtitle="The curse of dimensions"
  variant="error"
  icon="i-ph-cube-duotone"
  size="md"
  :list-items="[
    '6D phase space: $(x,y,z,\\Omega_x,\\Omega_y,\\Omega_z)$',
    'Grid points scale exponentially as $N^6$',
    'Intractable memory and storage needs'
  ]"
  :enable-latex="true"
/>

<GlassCard
  title="Complex Collisions"
  subtitle="Nonlinear interactions"
  variant="warning"
  icon="i-ph-arrows-merge-duotone"
  size="md"
  :list-items="[
    'Preserve conservation laws at discrete level',
    'Handle nonlinear Boltzmann-type operators',
    'Avoid spurious ray effects and diffusion'
  ]"
/>

<GlassCard
  title="Multi-scale Physics"
  subtitle="Regime coupling"
  variant="tech"
  icon="i-ph-scales-duotone"
  size="md"
  :list-items="[
    'Stiffness parameter: $\\varepsilon = \\ell/L \\ll 1$',
    'Design asymptotic-preserving schemes',
    'Couple transport ↔ diffusion transitions'
  ]"
  :enable-latex="true"
/>

</div>

<div class="mt-6">
  <GlassCard variant="gradient-primary" text-center size="sm">
    <div class="text-base font-semibold mb-1">
      <span class="emphasis-tech">Why Deep Learning?</span>
    </div>
    <div class="text-sm opacity-90">
      Neural networks can potentially overcome dimensional scaling and learn complex multi-scale behavior
    </div>
  </GlassCard>
</div>

---

# Conventional Approaches

<div class="mb-4 text-center">
  <div class="text-lg text-on-surface mb-2">Existing methods struggle with the computational barriers</div>
  <div class="text-sm text-on-surface-variant">Two main categories with complementary strengths and limitations</div>
</div>

<div grid="~ cols-2 gap-6" mt-6>

<div>
  <GlassCard
    title="Probabilistic Methods"
    subtitle="Statistical sampling"
    variant="primary"
    icon="i-ph-dice-six-duotone"
    size="md"
  >
    <div class="space-y-3 text-xs">
      <div>
        <div class="font-semibold mb-1">Monte Carlo Transport:</div>
        <div class="space-y-0.5 pl-2 text-2xs">
          <div>• MCNP, COG (LLNL), Mercury</div>
        </div>
      </div>
      <div>
        <div class="font-semibold mb-1">Direct Simulation:</div>
        <div class="space-y-0.5 pl-2 text-2xs">
          <div>• DSMC (Bird, Nanbu), Sparta (ORNL)</div>
        </div>
      </div>
    </div>
  </GlassCard>
</div>

<div>
  <GlassCard
    title="Deterministic Methods"
    subtitle="Grid-based discretization"
    variant="secondary"
    icon="i-ph-grid-four-duotone"
    size="md"
  >
    <div class="space-y-3 text-xs">
      <div>
        <div class="font-semibold mb-1">Discrete Ordinates:</div>
        <div class="space-y-0.5 pl-2 text-2xs">
          <div>• Ardra (LLNL), NEWT (ORNL), DORT</div>
        </div>
      </div>
      <div>
        <div class="font-semibold mb-1">Spectral Methods:</div>
        <div class="space-y-0.5 pl-2 text-2xs">
          <div>• High-order accuracy, smooth reconstruction</div>
        </div>
      </div>
    </div>
  </GlassCard>
</div>

</div>

<div class="mt-6">
  <ProsCons
    :pros="[
      'Monte Carlo: Easy parallelization',
      'Deterministic: Exact conservation',
      'Both: Mature, established theory'
    ]"
    :cons="[
      'Monte Carlo: Slow √N convergence',
      'Deterministic: Exponential scaling',
      'Both: Struggle with high dimensions'
    ]"
  />
</div>

---
layout: center
---

<div flex="~ col gap-5 items-center">
  <div font-600 m--2 text-center>

  # Deep learning methods may become new approach

  </div>
  <div text-2xl op75 text-center>Overcome the curse of dimensionality</div>
</div>

---
glow: right
---

# Solve PDEs with Deep Learning

<div flex="~ col gap-3">

<div>
  <GlassCard
    title="Architecture: hypothesis space"
    variant="success"
    icon="i-ph-brain-duotone"
    size="md"
    :list-items="[
      'Approximate solution: PINNs, DeepRitz, etc.',
      'Approximate solution operator: DeepONet, FNO, etc.',
      'Approximate PDE (from equations to solutions): PDEFormer-1/2'
    ]"
  />
</div>

<div>
  <GlassCard
    title="Constraints: loss of minimization problem"
    variant="error"
    icon="i-carbon:constraint"
    size="md"
    :list-items="[
      'Data: pure supervised or as a priori information',
      'Model: physical information (PDE) needed (e.g., PINNs, DeepRitz, DeepGalerkin)',
      'Other: IC, BC, conservation, symmetry, etc.'
    ]"
  />
</div>

<div>
  <GlassCard
    title="Optimization"
    variant="warning"
    icon="i-streamline:graph-arrow-decrease"
    size="md"
    :list-items="[
      'Minimize loss over the parameter space, usually SGD, Adams, LBFGS, etc.',
    ]"
  />
</div>

</div>

---
glow: left
---

# DeepRTE

<div class="mb-4 text-center">
  <div class="text-lg text-on-surface mb-1">
    <span class="emphasis-primary font-bold">Deep</span> learning for <span class="emphasis-primary font-bold">R</span>adiative <span class="emphasis-primary font-bold">T</span>ransfer <span class="emphasis-primary font-bold">E</span>quation
  </div>
</div>

<div grid="~ cols-[1fr_min-content_1fr] items-center gap-15" mt-5 w-full>

<div>
  <GlassCard
    title="Neural Operator"
    subtitle="Learn mapping to solution"
    variant="primary"
    icon="i-ph-function-duotone"
    size="lg"
  >
  <div class="space-y-4">
  <div class="text-center equation-block text-sm">

  $$
  \mathcal{A}_\theta: (I_-; \mu_t, \mu_s, p) \mapsto I
  $$

  </div>
  <div class="text-sm space-y-2">
    <list
      variant="primary"
      :list-items="[
        'Attention-based transformer',
        'Resolution-invariant',
        'Parameter-to-solution mapping'
      ]"
    />
  </div>
  </div>
  </GlassCard>
</div>

<div i-ph:plus-duotone text-6xl op50 />

<div>
  <GlassCard
    title="Pre-training"
    subtitle="Curated dataset tailored for RTE"
    variant="tech"
    icon="i-ph-database-duotone"
    size="lg"
  >
    <div class="space-y-4">
      <div class="text-center">
        <div class="grid grid-cols-3 gap-2 text-sm">
          <div class="bg-error-100/50 dark:bg-error-900/30 rounded p-3">
            Generate<br/>Data
          </div>
          <div class="bg-warning-100/50 dark:bg-warning-900/30 rounded p-3">
            Train<br/>Operator
          </div>
          <div class="bg-success-100/50 dark:bg-success-900/30 rounded p-3">
            Transfer<br/>Learning
          </div>
        </div>
      </div>
      <div class="text-sm space-y-2">
        <List
          variant="primary"
          :list-items="[
            'Delta function data',
            'End-to-end pre-training',
            'Zero-shot generalization'
          ]"
        />
      </div>
    </div>
  </GlassCard>
</div>

</div>

<div class="mt-5">
  <GlassCard variant="gradient-primary" text-center size="md" w-full>
    <div class="font-semibold text-lg">
      <span class="emphasis-tech">Key advantage:</span>
      Train once, solve many RTE problems
    </div>
  </GlassCard>
</div>

---
glow: right
---

# Why not DeepONet?
DeepONet has fundamental limitations for radiative transfer problems

<div grid="~ cols-2 gap-6" mt-6 items-stretch>

<div>
  <GlassCard
    title="DeepONet Limitations"
    variant="error"
    icon="i-ph-x-circle-duotone"
    size="lg"
    class="h-full"
  >
    <div class="space-y-4" mt-8>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">Fixed Discretization:</div>
        <div class="text-2xs text-on-surface-variant">
          Requires fixed grid points, limiting flexibility
        </div>
      </div>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">Parameter Scaling:</div>
        <div class="text-2xs text-on-surface-variant">
          Network size grows with input dimension
        </div>
      </div>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">Multi-Input Challenge:</div>
        <div class="text-2xs text-on-surface-variant">
          Difficulty with multiple input functions
        </div>
      </div>
    </div>
  </GlassCard>
</div>

<div>
  <GlassCard
    title="DeepONet Structure"
    variant="warning"
    icon="i-ph-tree-structure-duotone"
    size="lg"
    class="h-full"
  >
    <div class="text-center space-y-4">
      <img src="/deeponet.png" class="rounded shadow-sm mx-auto" alt="DeepONet"/>
      <div class="text-2xs text-on-surface-variant">
        Branch + Trunk architecture
      </div>
    </div>
  </GlassCard>
</div>

</div>

---
glow: left
---

# Why not FNO?
Fourier Neural Operator has structural limitations for radiative transfer

<div grid="~ cols-2 gap-6" mt-6 items-stretch>

<div>
  <GlassCard
    title="FNO Limitations"
    variant="error"
    icon="i-ph:x-circle-duotone"
    size="lg"
    class="h-full"
  >
    <div class="space-y-2">
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">Uniform Grid Requirement:</div>
        <div class="text-2xs text-on-surface-variant">
          Input functions must be on uniform grid, limiting geometric flexibility
        </div>
      </div>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">FFT Computational Cost:</div>
        <div class="text-2xs text-on-surface-variant">
          FFT operations become slow as function dimension increases
        </div>
      </div>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">Frequency Domain Assumption:</div>
        <div class="text-2xs text-on-surface-variant">
          Relies on spectral decay which may not hold for RTE
        </div>
      </div>
    </div>
  </GlassCard>
</div>

<div>
  <GlassCard
    title="FNO Structure"
    variant="warning"
    icon="i-ph:tree-structure-duotone"
    size="lg"
    class="h-full"
  >
    <div class="text-center space-y-4">
      <img src="/fno.png" class="rounded shadow-sm mx-auto" alt="FNO Architecture"/>
      <div class="text-2xs text-on-surface-variant">
        Fourier layer-based neural operator
      </div>
      <div class="bg-warning-100/50 dark:bg-warning-900/30 rounded p-1.5">
        <div class="text-2xs font-semibold text-warning-600 dark:text-warning-400">
          RTE Challenge: Irregular geometries & high dimensionality
        </div>
      </div>
    </div>
  </GlassCard>
</div>
</div>

---

# Our goal

End-to-end fashion

<GlassCard title="Learn the solution operator" variant="primary">
<div class="equation-block">

$$
\mathcal{A}: (I_-; \mu_t, \mu_s, p) \mapsto I
$$

</div>
</GlassCard>

<div grid="~ cols-[2fr_auto_1fr] items-center gap-20" mt-5>

<GlassCard
  title="Inputs"
  variant="warning"
  size="md"
>
<List
  variant="warning"
  enable-latex="true"
  :list-items="[
    '$I_{-}(r,\\Omega)$: incoming boundary function',
    '$\\mu_t(r)$: total cross section',
    '$\\mu_s(r)$: scattering cross section',
    '$' + 'p(\\Omega,\\Omega^*)$: scattering kernel function'
  ]"
/>
</GlassCard>

<div i-ph:arrow-right-duotone text-5xl op-50 />

<GlassCard title="Output" variant="success" size="md">
<div class="equation-block">

$$
I(r, \Omega)
$$

</div>
</GlassCard>

</div>

---

# Idea

Green's function:

<GlassCard title="Approximate the integral kernel of solution by neural network" variant="secondary" size="md">
<div class="equation-block">

$$
I(r, \Omega)\approx \int_{\Gamma_-} G^{\text{NN}}(r, r', \Omega, \Omega'; \mu_t, \mu_s, p) I_-(r',\Omega') \, \mathrm{d}r' \mathrm{d}\Omega'
$$

</div>

<div class="text-on-surface-variant space-y--2">
<div flex="~ gap-4 items-center">
<div i-ph:square-duotone text="academic/70 sm" />
<div>

Solution $I$ is <span class="text-academic">linear</span> in boundary $I_{-}$

</div>
</div>
<div flex="~ gap-4 items-center">
<div i-ph:square-duotone text="academic/70 sm" />
<div>

Green's function $G^{\text{NN}}$ is <span text-academic>non-linear</span> in $\mu_t$, $\mu_s$ and $p$

</div>
</div>
<div flex="~ gap-4 items-center">
<div i-ph:square-duotone text="academic/70 sm" />
<div>

Green's function $G^{\text{NN}}$'s dependency on $\mu_t$ and $\mu_s$ is <span text-academic>non-local</span>

</div>
</div>
</div>
</GlassCard>

<GlassCard variant="success" mt-4 text="center xl success">
Start by looking at the "analytical" structure of Green's function/solution operator
</GlassCard>

---

# Structure of solution operator

<div flex="~ col gap-2">
<GlassCard title="Steady RTE" variant="primary" size="md">
<div flex="~ gap-4 justify-center items-center">
<div equation-block px32>

$$
\begin{aligned}
\Omega \cdot \nabla I + \mu_t I & = \mu_s\mathcal{S}I, \\
I|_{\Gamma_{-}} & = I_{-},
\end{aligned}
\quad \text{where} \quad
\mathcal{S}I:=\frac{1}{S_{d-1}}\int_{\mathbb{S}^{d-1}} p(\Omega, \Omega^*) I(r, \Omega^*)\,\mathrm{d}\Omega^*
$$

</div>
</div>
</GlassCard>

<div i-ph:arrows-split-duotone op-50 text-5xl ml-102/>

<div grid="~ cols-[1fr_auto_1fr] items-center gap-8">

<GlassCard title="Attenuation" size="md" variant="success">
<div class="equation-block">

$$
\begin{aligned}
\Omega \cdot \nabla I + \mu_t I & = 0, \\
I|_{\Gamma_{-}} & = I_{-}.
\end{aligned}
$$

</div>
</GlassCard>

<div i-ph:plus-duotone text-5xl />

<GlassCard title="Scattering" size="md" variant="warning">
<div class="equation-block">

$$
\begin{aligned}
\Omega \cdot \nabla I + \mu_t I & = \mu_s\mathcal{S}I, \\
I|_{\Gamma_{-}} & = 0.
\end{aligned}
$$

</div>
</GlassCard>
</div>
</div>

---

# Structure of solution operator

<div grid="~ cols-[max-content_min-content_auto] gap-4 items-center" w-full>
<GlassCard title="Attenuation" size="sm" variant="success">
<div class="equation-block">

$$
\Omega \cdot \nabla I + \mu_t I = 0, \; I|_{\Gamma_{-}} = I_{-}.
$$

</div>
</GlassCard>

<div i-ph:arrow-right-duotone op-50 text-4xl />

<GlassCard title="$\mathcal{J}$ operator" size="sm" variant="success" enable-latex="true">
<div class="equation-block">

$$
I(r,\Omega) = \mathcal{J}I_{-}:=e^{-{\color{pink}\tau(0,s_{-})}}I_{-}(r-s_{-}\Omega,\Omega).
$$

</div>
</GlassCard>

<GlassCard title="Scattering" size="sm" variant="warning" h-34>
<div class="equation-block">

$$
\Omega \cdot \nabla I + \mu_t I = \mu_s\mathcal{S}I, \; I|_{\Gamma_{-}} = 0.
$$

</div>
</GlassCard>

<div i-ph:arrow-right-duotone op-50 text-4xl />

<GlassCard title="$\mathcal{L}$ and $\mathcal{S}$ operators" size="sm" variant="warning" enable-latex="true">
<div class="equation-block">

$$
I(r,\Omega) = \mathcal{L}\mathcal{S}I:=\int_0^{s_{-}}e^{-{\color{pink}\tau(0,s)}}\mu_s(r-s\Omega)\mathcal{S}I(r-s\Omega,\Omega)\,\mathrm{d}s
$$

</div>
</GlassCard>
</div>

<GlassCard title="Integral fomulation of steady RTE" variant="error" size="sm" mt-4>
<div flex="~ gap-2 items-center justify-center">
<div equation-block text-base>

$$
I = \mathcal{L}\mathcal{S}I + \mathcal{J}I_{-}
$$

</div>
where the <span text-pink-3>optical depth</span> is defined as:
<div equation-block text-pink-3>

$$
\tau(s_1,s_2):=\int_{s_1}^{s_2}\mu_t(r-s\Omega)\,\mathrm{d}s
$$

</div>
</div>
</GlassCard>

---

# DeepRTE: architecture

Overview

<GlassCard
  title="The Green's function also satisfy"
  variant="primary"
  size="md"
>
<div equation-block text-base>

$$
G(r,r',\Omega,\Omega') = \mathcal{L}\mathcal{S}G(r,r',\Omega,\Omega') + \mathcal{J}\left(\delta_{\{r'\}}(r)\delta(\Omega-\Omega')\right)
$$

</div>
</GlassCard>

<GlassCard
  variant="secondary"
  title="Iterate as the block composition of a neural network"
  subtitle="Inspired by source iteration method"
  size="md"
  mt-5
  >
<div flex="~ gap-4 items-center justify-center" text-base>
<div>

$\ell$-th block:

</div>
<div equation-block>

$$
G^{\ell+1} = \mathcal{L}\mathcal{S}G^{\ell} + G^0
$$

</div>
<div>with</div>
<div equation-block>

$$
G^0 = \mathcal{J}\left(\delta_{\{r'\}}(r)\delta(\Omega-\Omega')\right).
$$

</div>
</div>

<div text-base mt-4>
<List
  variant="secondary"
  :list-items="[
    '$\\mathcal{J}$, $\\mathcal{L}$: attenuation module (attention along characteristic)',
    '$\\mathcal{S}$: scattering module'
  ]"
  enable-latex="true"
/>
</div>

</GlassCard>

---

# Attenuation module

$\mathcal{J}$ and $\mathcal{L}$

<div flex="~ col gap-4 items-center">
<GlassCard title="$\mathcal{J}$ operator for example" size="md" variant="success" enable-latex="true">
<div class="equation-block">

$$
G^0(r,r',\Omega,\Omega';\mu_t)= \mathcal{J}\left(\delta_{\{r'\}}(r)\delta(\Omega-\Omega')\right)=e^{-{\color{pink}\tau(0,s_{-})}}\left(\delta_{\{r'\}}(r)\delta(\Omega-\Omega')\right)\approx \text{MLP}(r,r,\Omega,\Omega';\tau^{\text{NN}})
$$

</div>
</GlassCard>

<div i-ph:arrow-fat-lines-up-duotone text-4xl op-50 />

<GlassCard title="Optical depth network" size="md" variant="error" enable-latex="true">
<div class="equation-block">

$$
\tau^{\text{NN}}(r,\Omega)\approx\tau(0,s_{-})=\int_0^{s_{-}(r,\Omega)}\mu_t(r-s\Omega)\,\mathrm{d}s
$$

</div>
</GlassCard>
</div>

---

# Optical depth network

<GlassCard title="Attention along the characteristic" variant="error">
<div flex="~ col gap-2">
<div equation-block>

$$
\tau^\text{NN} = \text{OpticalDepthNet}\left(r,\Omega; \{r^\text{mesh}_i\}, \{(\mu_t^{\text{mesh}})_i\}\right) = \text{MultiHead}(Q, K, V)
$$

</div>
<div text-xs flex="~ gap-2 items-center" ml-28>
<div>where</div>
<div>

$$
Q = (r, \Omega)\in \mathbb{R}^{1\times 2d}, \quad
K =
\begin{pmatrix}
  \vdots \\
  {(r^\text{mesh}_{\text{local}})}_i \\
  \vdots
\end{pmatrix}\in\mathbb{R}^{N_\text{mesh} \times 2},
\quad
V =
\begin{pmatrix}
  \vdots \\
  {(\mu_t^{\text{mesh}})}_i \\
  \vdots
\end{pmatrix}\in\mathbb{R}^{N_\text{mesh}\times 1}.
$$

</div>
</div>
</div>
</GlassCard>

<GlassCard variant="secondary" title="Relative position encoding" mt-4>
<div equation-block>

$$
{(r^\text{mesh}_{\text{local}})}_i = \left({(r^\text{mesh}_\text{local})}_i, {(\theta^\text{mesh}_\text{local})}_i\right)
= \left((r-r^{\text{mesh}}_i)\cdot\Omega, \frac{(r-r^{\text{mesh}}_i)}{
\| r-r^{\text{mesh}}_i\|}\cdot \Omega\right)
$$

</div>
</GlassCard>

---

# Optical depth network

<div flex="~ col gap-4 items-center">
<div flex="~ gap-4 items-center">
<GlassCard variant="success" size="sm">
<div equation-block>

$$
\tau(r,\Omega) \approx  \sum_{j}^{N\left(s_{-}(r,\Omega)\right)} w(r, \Omega;s_j)\mu_t(r-s_j \Omega),
$$

</div>
</GlassCard>
<div i-ph:arrow-fat-lines-left-duotone text-3xl op-50 />
<GlassCard variant="secondary" size="sm">
<div equation-block>

$$
\mu_t(r-s_j \Omega)\approx  \sum_{i}^{N_\text{mesh}} \bm{1}_{\mathcal{C}_{r,\Omega}}(r_i^{\text{mesh}}) c(r-s_j\Omega, r^{\text{mesh}}_i){(\mu_t^\text{mesh})}_i,
$$

</div>
</GlassCard>
</div>

<div i-ph:arrows-merge-duotone text-4xl op-50 ml--22 />

<GlassCard variant="error" size="sm">
<div equation-block text-xs>

$$
\begin{aligned}
\tau(r,\Omega) & \approx \sum_j^{N\left(s_{-}(r,\Omega)\right)} w(r,\Omega;s_j)\sum_{i}^{N_\text{mesh}} \bm{1}_\mathcal{C}(r_i^{\text{mesh}})c\left(s_j; (r^\text{mesh}_\text{local})_i, (\theta^\text{mesh}_\text{local})_i\right)(\mu_t^\text{mesh})_i \\
& =\sum_{i}^{N_\text{mesh}} \bm{1}_\mathcal{C}(r^{\text{mesh}}_i)\left(\sum_{j}^{N\left(s_{-}(r,\Omega)\right)} w(r,\Omega;s_j)c\left(s_j; (r^\text{mesh}_\text{local})_i, (\theta^\text{mesh}_\text{local})_i\right)\right)(\mu_t^\text{mesh})_i \\
& =\sum_{i}^{N_\text{mesh}} \underbrace{\bm{1}_\mathcal{C}(r^{\text{mesh}}_i)W(r,\Omega; (r^\text{mesh}_\text{local})_i, (\theta^\text{mesh}_\text{local})_i)}_{\text{attention weights}}\underbrace{(\mu_t^\text{mesh})_i}_{\text{values}},
\end{aligned}
$$

</div>
</GlassCard>
</div>

---

# Optical depth network

<GlassCard title="Attention along characteristic" variant="primary">
<div equation-block>

$$
W\left(r,\Omega; {\left(r^\text{mesh}_\text{local}\right)}_i, {\left(\theta^\text{mesh}_\text{local}\right)}_i\right) \approx \sum_{m}^{d_k} \underbrace{q_m(r,\Omega)}_{\text{query}:\;QW^Q_h}\underbrace{k_m({(r^\text{mesh}_\text{local})}_i, {(\theta^\text{mesh}_\text{local})}_i)}_{\text{keys}:\;KW^K_h},
$$

</div>
<div flex="~ justify-center" mt-5>
  <img src="/figs/mask.png" h-55 dark:invert />
</div>
</GlassCard>

---

# Attenuation

Summary

<GlassCard title="Diagram of attenuation module" variant="secondary" size="lg">
<div bg-white:95 rounded-xl p-4 mt-5>
  <img src="/figs/attenuation_module.png" />
</div>
</GlassCard>

---

# Scattering module

<GlassCard title="Scattering as iteration" size="md" variant="primary">
<div equation-block pb-0>

$$
\begin{aligned}
  & G^{0} = G^{\text{NN}}(r,\Omega,r^{\prime},\Omega^{\prime}), \\
  & G^{\ell}  = \text{ScatteringBlock}_s(G^{\ell-1}) + G^{0}, \quad \ell = 1,\dots,N_{\ell},
\end{aligned}
$$

</div>
<div bg-white:95 rounded-xl p-2 mt-4 flex="~ justify-center">
  <img src="/figs/scattering_module.png" h-55 />
</div>

</GlassCard>

---

# Scattering block

<GlassCard variant="primary" size="md">
<div equation-block>

$$
\text{ScatteringBlock}_\ell(G) = \text{LayerNorm}\Big(\sigma\Big(W^{\ell} S^{\top} G + b^{\ell}\Big)\Big).
$$

</div>

<div flex="~ gap-4 items-center justify-center" text-base>

$$
\mathcal{S} G^\ell(r-s' \Omega, \Omega) \approx \sum_{i=1}^{d_{\text{quad}}} w_i p(\Omega, \Omega_i^*) G^{\ell}(r-s' \Omega, \Omega_i^*),
$$

$$
\mathcal{L}\mathcal{S} G^{\ell}(r, \Omega) \approx \sum_{j=1}^{d_{\text{model}}} \tilde{w}_j^{r, \Omega} \mu_s e^{-\tau(0,s'_j)} \mathcal{S} G^\ell(r-s'_j \Omega, \Omega).
$$

</div>
<div bg-white:95 rounded-xl p-2 mt-4 flex="~ justify-center">
  <img src="/figs/scattering_block.png" h-40 />
</div>

</GlassCard>

---

# DeepRTE Architecture

Recap

<div grid="~ cols-2 gap-6" mt-6>

<div>
  <GlassCard
    title="Attenuation Module"
    subtitle="Transport encoding"
    variant="primary"
    icon="i-ph-tree-structure-duotone"
    size="md"
    :list-items="[
      'Encodes $\\mu_t(r)$ and $\\mu_s(r)$ as optical depth network',
      'Attention along characteristic',
    ]"
    :enable-latex="true"
  />
</div>

<div>
  <GlassCard
    title="Scattering Module"
    subtitle="Scattering encoding"
    variant="secondary"
    icon="i-ph-map-pin-duotone"
    size="md"
    :list-items="[
      'Encodes $' + 'p(\\Omega,\\Omega^*)$',
      'Capture anisotropic scattering'
    ]"
    :enable-latex="true"
  />
</div>
</div>

<div bg-white:95 rounded-xl p-2 mt-4 flex="~ justify-center">
  <img src="/figs/architecture.png" h-50 />
</div>

---

# Training Strategy

Trained with delta-like function

<GlassCard
  title="Dataset"
  subtitle="In order to have zero-shot ability"
  variant="warning"
  icon="i-ph-database-duotone"
  size="lg"
>

<div flex="~ col gap-2" ml--2>

<List variant="secondary" :list-items="['we construct the training dataset consists of delta functions']" />
<div text-on-surface>

$$
I^{\delta}_{-}(r, \Omega; r', \Omega') =
\delta_{\{r'\}}(r)\delta(\Omega-\Omega'), \quad (r,\Omega) \in \Gamma_{-}.
$$

</div>
<List variant="secondary" :list-items="['In practice, we use smoothed version of delta functions as the boundary functions']" />
<div text-on-surface>

$$
\delta_{\{r'\}}^{\sigma}(r) = \frac{1}{\sigma \sqrt{\pi}} \exp\left( -\frac{(r-r')^2}{\sigma^2} \right), \quad
\delta^{\sigma}(\Omega-\Omega') = \frac{1}{\sigma \sqrt{\pi}} \exp\left( -\frac{(\Omega-\Omega')^2}{\sigma^2} \right),
$$

</div>
</div>
</GlassCard>

---

# Training Strategy

<div grid="~ cols-[max-content_auto] gap-4">

<GlassCard
  title="RTE Features"
  variant="warning"
  icon="i-ph-database-duotone"
  size="md"
>
<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>

| **Features & Shape** | **Description** |
| ---------------- | ----------- |
| phase_coords: $[N_{\text{coords}}, 2d]$ | Phase coordinates $(r,\Omega)$ |
| boundary_coords: $[N_{\text{bc}}, 2d]$ | Boundary coordinates $(r',\Omega')$ |
| position_coords: $[N_{\text{mesh}}, 2d]$ | Mesh points $(r^{\text{mesh}})$ |
| velocity_coords: $[N_{\text{quad}}, 2d]$ | Angular quadrature points $\Omega^*$ |
| boundary: $[N_{\text{bc}}]$ | Boundary $I(r',\Omega')$ |
| mu: $[N_{\text{mesh}}, 2]$ | Cross sections $\mu_t$ and $\mu_s$ |
| scattering_kernel: $[N_{\text{quad}}]$ | Scattering kernel $p(\Omega,\Omega^*)$ |

</div>
</GlassCard>

<GlassCard
  title="Training setup"
  variant="success"
  icon="i-ph-target-duotone"
  size="md"
>

<div flex="~ col gap-2" ml--2 mt-3>

<List variant="success" :list-items="['Adam optimizer', 'Cosine annealing learning rate schedule']" />
<List variant="success" :list-items="['MSE loss']" />

<div text-on-surface ml-2>
<div equation-block>

$$
\mathcal{L}(\theta) = \frac{1}{N}\sum_{n=1}^N \ell(I^\text{NN}_{\theta,n}, I_n),
$$

</div>

<div equation-block mt-3>

$$
\ell(I^\text{NN}_{\theta}, I)= \frac{1}{N_\text{col}}\sum_{i=1}^{N_{\text{col}}} \left| I^{\text{NN}}_{\theta}(r_i,\Omega_i) - I(r_i, \Omega_i) \right|^2
$$

</div>
</div>
</div>
</GlassCard>
</div>

---

# Experimental Setup

<div mt-2 />

Let
$$
\Omega=(c,s,\zeta), \quad c =
{\left(1-\zeta^{2}\right)}^{\frac{1}{2}} \cos\theta, \quad s =
{\left(1-\zeta^{2}\right)}^{\frac{1}{2}} \sin\theta, \quad \text{for }|\zeta| \leq 1.
$$

<GlassCard
  title="Reduced 2-D RTE"
  variant="primary"
  icon="i-ph-test-tube-duotone"
  size="md"
>
<div equation-block>

$$
\left(c\partial_x \tilde{I}(x,y,\zeta,\theta)+s\partial_y
\tilde{I}(x,y,\zeta,\theta)\right)+\mu_t \tilde{I}(x,y,\zeta,\theta)=\frac{\mu_s}{2\pi}\int_{0}^{1}
\int_0^{2\pi} \tilde{p}(\zeta, \theta, \zeta^*,\theta^*) \tilde{I}(x,y,\zeta^*,\theta^*) \mathrm{d}\theta^*\mathrm{d}{\zeta^*},
$$

</div>
</GlassCard>

<GlassCard
  title="Henyey-Greenstein (H-G) scattering kernel"
  variant="secondary"
  size="sm"
  mt-4
>
<div equation-block>

$$
p(\Omega,\Omega^*) = p(\Omega\cdot\Omega^*) = \frac{1-g^2}{\Bigl(1+g^2-2g\,(cc^*+ss^*+\zeta\zeta^*)\Bigr)^{\frac{3}{2}}}.
$$

</div>
</GlassCard>

---

# Experimental Setup

<GlassCard
  title="Boundary conditions for training"
  variant="primary"
  size="sm"
  mt-4
>
<div equation-block>

$$
\left \{
\begin{aligned}
  & I_-(x=0,y,c>0,s;x_l^{\prime}=0,
  y_l^{\prime},c_l^{\prime},s_l^{\prime})
  =\delta_{\{y_l^{\prime}\}}^{\sigma_{r}}(y)\delta^{\sigma_{\Omega}}(c - c_l')\delta^{\sigma_{\Omega}}(s - s_l'),
  \\
  & I_-(x=1,y,c<0,s;x_r^{\prime}=1,
  y_r^{\prime},c_r^{\prime},s_r^{\prime})
  =\delta_{\{y_r^{\prime}\}}^{\sigma_{r}}(y)\delta^{\sigma_{\Omega}}(c - c_r')\delta^{\sigma_{\Omega}}(s - s_r'),
  \\
  & I_-(x,y=0,c,s>0;x_b^{\prime},y_b^{\prime}=0, c_b^{\prime},
  s_b^{\prime})
  =\delta_{\{x_b^{\prime}\}}^{\sigma_{r}}(x)\delta^{\sigma_{\Omega}}(c - c_b')\delta^{\sigma_{\Omega}}(s - s_b'),
  \\
  & I_-(x,y=1,c,s<0;x_t^{\prime},y_t^{\prime}=1,c_t^{\prime},
  s_t^{\prime})
  =\delta_{\{x_t^{\prime}\}}^{\sigma_{r}}(x)\delta^{\sigma_{\Omega}}(c - c_t')\delta^{\sigma_{\Omega}}(s - s_t'),
\end{aligned}
\right.
$$

</div>
</GlassCard>

<div grid="~ cols-2 gap-4 items-stretch" mt-4>
<GlassCard
  title="Cross sections"
  variant="secondary"
  size="sm"
>
<div equation-block>

$$
\begin{aligned}
\mu_t(x,y) &=
\begin{cases}
U_t, \quad \text{where } U_t \sim \mathcal{U}(5,7) & \text{if } (x,y) \in D_\mu \\
10 & \text{if } (x,y) \notin D_\mu
\end{cases} \\
\mu_s(x,y) &=
\begin{cases}
U_s, \quad \text{where } U_s \sim \mathcal{U}(2,4) & \text{if } (x,y) \in D_\mu \\
5 & \text{if } (x,y) \notin D_\mu
\end{cases}
\end{aligned}
$$

</div>
</GlassCard>

<GlassCard
  title="Scattering kernel"
  variant="success"
  size="sm"
>
<div equation-block>
<div py-3 text-base>

$$
g \sim
\begin{cases}
\mathcal{U}(0,0.2),  & \quad \text{near isotropy} \\
\mathcal{U}(0.4,0.6), & \quad \text{moderate anisotropy} \\
\mathcal{U}(0.7,0.9), & \quad \text{strong anisotropy} \\
\end{cases}
$$

</div>
</div>
</GlassCard>
</div>

---

# Dataset parameters

<div bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden mt--2>

| Category | Parameters | Symbol | Value/Range |
| -------- | ---------- | ------ | ----------- |
| Spatial domain | Domain<br> Subdomain | $D$ <br>  $D_\mu$  | ${[0,1]}^2$ <br> ${[0.4,0.6]}^2$ |
| Cross section | Total <br> Scattering | $\mu_t$ <br> $\mu_s$ | $\mathcal{U}(5,7)$ in $D_\mu$ and $10$ in $D\backslash D_\mu$ <br>  $\mathcal{U}(2,4)$ in $D_\mu$ and $5$ in $D\backslash D_\mu$ |
| Discretization | # of mesh points <br> # of angular quadrature points | $N_{\text{mesh}}$ <br> $N_\text{quad}$  | $40$ <br> $24$ |
| Boundary conditions | Beam spatial center coordinates <br><div mt-2 /> Beam angular quadrature points <br><div mt-3 /> Beam spatial std dev <br> Beam angular std dev | $y_l', y_r', x_b', x_t'$ <br> $c_l', c_r', c_b', c_t'$ <br> $s_l', s_r', s_b', s_t'$ <br> $\sigma_{r}$ <br> $\sigma_{\Omega}$ | Sampled from mesh points <br><div mt-2 /> Sampled from quadrature points <br><div mt-3 /> $\sqrt{2}\,\mathcal{U}(0.005, 0.02)$ <br> $\sqrt{2}\,\mathcal{U}(0.005, 0.01)$ |
| Scattering | Asymmetry parameter | $g$ | $\mathcal{U}(0,0.2)$ <br> $\mathcal{U}(0.4,0.6)$ <br> $\mathcal{U}(0.7,0.9)$ |

</div>

---
class: pt-4
---

# Hyperparameters

<div grid="~ cols-2 gap-6" mt--2>

<GlassCard
  title="Neural Network"
  variant="warning"
  icon="i-ph-database-duotone"
  size="md"
>
<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden mt-10>

| **Module Name** | **Hyperparameters** | **Value** |
| ---------------- | ------------------ | --------- |
| Attenuation | $\texttt{num\_layer}$: $N_{\text{mlp}}$ <br> $\texttt{hidden\_dim}$: $d_{\text{mlp}}$ <br> $\texttt{output\_dim}$: $d_{\text{model}}$ <br> $\texttt{num\_head}$: $N_{\text{head}}$ <br> $\texttt{key\_dim}$: $d_k$ <br> $\texttt{value\_dim}$: $d_v$ <br> $\texttt{output\_dim}$: $d_{\tau}$ | $4$ <br> $128$ <br> $16$ <br> $2$ <br> $32$ <br> $32$ <br> $2$ |
| Scattering | $\texttt{num\_block}$: $N_{\ell}$ <br> $\texttt{latent\_dim}$: $d_{\text{model}}$ | $2$ <br> $16$ |

</div>
</GlassCard>

<GlassCard
  title="Training"
  variant="success"
  icon="i-ph-target-duotone"
  size="md"
>

<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>

| **Hyperparameters** | **Value** |
| --------------------| --------- |
| Optimizer | Adam |
| Learning rate schedule | Cosine annealing |
| Initial learning rate | $1\times 10^{-3}$ |
| Batch size | $8$ |
| Epochs | $5000$ |
| # of training data | $800$ |
| # of validation data | $200$ |
| # of collocation points | $128$ |

</div>
</GlassCard>
</div>

---

# Results: Accuracy

Same distribution as training dataset

<GlassCard
  title="Accuracy validation"
  subtitle="Delta-like functions"
  variant="success"
  icon="i-ph-target-duotone"
  size="lg"
  mt-10
>
<div bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text text-on-surface overflow-hidden text-lg>

| **Model** | **# of parameters** | **Scattering regime** | **$g$ range** | **MSE($\times 10^{-10}$)** | **RMSPE($\%$)** |
| -------------------- | --------- | --------- | -------- | -------- | --------- |
| DeepRTE | $37954$ | Near isotropy <br> Moderate anisotropy <br> Strong anisotropy | $(0, 0.2)$ <br> $(0.4,0.6)$ <br> $(0.7,0.9)$ | $5.630$ <br> $5.453$ <br> $7.223$ | $2.827$ <br> $2.759$ <br> $3.181$ |

</div>
</GlassCard>

---

# Results

<div rounded-xl flex="~ justify-center" mt--1>
<img src="/figs/accuracy.png" h-110 rounded-lg bg-white p-2 />
</div>

---

# Generalization Capabilities

<div class="mb-2 text-center">
  <div class="text-xl text-on-surface mb-2">
    <span class="emphasis-primary font-bold">Zero-shot Generalization</span> Beyond Training Distribution
  </div>
</div>

<div grid="~ cols-2 gap-6" mt-4>

<GlassCard
  title="Out-of-Distribution Tests"
  subtitle="Challenging scenarios"
  variant="tech"
  icon="i-ph-arrows-out-duotone"
  size="md"
  :list-items="[
    'Different boundary conditions',
    'Different cross-sections and scattering kernels'
  ]"
/>

<GlassCard
  title="Transfer Learning"
  subtitle="Zero-shot adaptation"
  variant="secondary"
  icon="i-ph-swap-duotone"
  size="md"
  :list-items="[
    'Pre-trained on delta boundary',
    'High accuracy (< 5% error)'
  ]"
/>

</div>

<div class="mt-4">
<GlassCard
  title="3 Cases"
  variant="gradient-secondary"
  icon="i-ph:balance-duotone"
  size="md"
>
<div flex="~ col items-center gap-2">
<div equation-block>
<div class="grid grid-cols-3 gap-3 text-sm text-center">
  <div>
    <div class="font-semibold mb-1">Case I</div>
    <div>Constant boundary conditions</div>
  </div>
  <div>
    <div class="font-semibold mb-1">Case II</div>
    <div>Trigonometric boundary condition</div>
  </div>
  <div>
    <div class="font-semibold mb-1">Case III</div>
    <div>Velocity dependent boundary condition</div>
  </div>
</div>
</div>
<div i-ph:x-duotone text-3xl op-50 />
<div equation-block text-sm p0>

$$
g \sim (0, 0.2), (0.4, 0.6), (0.7, 0.9)
$$

</div>
</div>
</GlassCard>
</div>

---

# Case I:

Without further training

<GlassCard title="Constant boundary conditions" variant="primary" size="sm">
<div equation-block>

$$
\left \{
  \begin{aligned}
    & I_-(x=0,y,c>0,s) =1,  \\
    & I_-(x=1,y,c<0,s) = 0, \\
    & I_-(x,y=0,c,s>0) =0,  \\
    & I_-(x,y=1,c,s<0) =0,
  \end{aligned}
  \right.
$$

</div>
</GlassCard>

<div rounded-xl flex="~ justify-center" h-50 mt-2 bg-white>
<img src="/figs/case-1.png"/>
</div>

---

# Case II:

Without further training

<GlassCard title="Trigonometric boundary conditions" variant="secondary" size="sm">
<div flex="~ gap-6 items-center justify-center" text-on-surface>
<div equation-block>

$$
\left \{
  \begin{aligned}
    & I_-(x=0,y,c>0,s) =a_L\sin{k_L y}+5,   \\
    & I_-(x=1,y,c<0, s) = a_R\sin{k_R y}+5, \\
    & I_-(x,y=0,c,s>0) =a_B\sin{k_B x}+5,   \\
    & I_-(x,y=1,c,s<0) =a_T\sin{k_T x}+5,
  \end{aligned}
  \right.
$$

</div>
with
<div equation-block>

$$
a_L, a_R, a_B, a_T \sim \mathcal{U}(-5,5), \quad
k_L, k_R, k_B, k_T \sim\mathcal{U}(-10, 10).
$$

</div>
</div>
</GlassCard>

<div rounded-xl flex="~ justify-center" h-50 mt-2 bg-white>
<img src="/figs/case-2.png"/>
</div>

---

# Case III:

Without further training

<GlassCard title="Velocity dependent boundary conditions" variant="success" size="sm">
<div flex="~ gap-6 items-center justify-center" text-on-surface>
<div equation-block>

$$
\left \{
  \begin{aligned}
    & I_-(x=0,y,c>0,s) =(a_{Lr}\sin{k_{Lr} y}+5)(a_{Lv}\sin{k_{Lv} c}+1)(a_{Lv}\sin{k_{Lv} s}+1), \\
    & I_-(x=1,y,c<0,s) = (a_{Rr}\sin{k_{Rr} y}+5)(a_{Rv}\sin{k_{Rv} c}+1)(a_{Rv}\sin{k_{Rv} s}+1),
    \\
    & I_-(x,y=0,c,s>0) =(a_{Br}\sin{k_{Br} x}+5)(a_{Bv}\sin{k_{Bv} c}+1)(a_{Bv}\sin{k_{Bv} s}+1),
    \\
    & I_-(x,y=1,c,s<0) =(a_{Tr}\sin{k_{Tr} x}+5)(a_{Tv}\sin{k_{Tv} c}+1)(a_{Tv}\sin{k_{Tv} s}+1),
  \end{aligned}
  \right.
$$

</div>
with
<div equation-block>

$$
\begin{aligned}
a_{Lr}, a_{Rr}, a_{Br}, a_{Tr} &\sim \mathcal{U}(-5,5), \\
a_{Lv}, a_{Rv}, a_{Bv}, a_{Tv} &\sim \mathcal{U}(-1,1), \\
k_{Lr}, k_{Rr}, k_{Br}, k_{Tr} &\sim\mathcal{U}(-10, 10),\\
k_{Lv}, k_{Rv}, k_{Bv}, k_{Tv} &\sim\mathcal{U}(-6, 6).
\end{aligned}
$$

</div>
</div>
</GlassCard>

<div rounded-xl flex="~ justify-center" h-50 mt-2 bg-white>
<img src="/figs/case-3.png"/>
</div>

---

# Results: Summary

<div grid="~ cols-[1fr_1.2fr] gap-4" mt--2>

<GlassCard
  title="Zero-shot performance"
  variant="warning"
  icon="i-ph-database-duotone"
  size="sm"
>
<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden mt-10>

|       | **Test Dataset** | **MSE** | **RMSPE($\%$)** |
| ---------------- | ------------------ | --------- | ------ |
| Case I | $g\in(0,0.2)$ <br> $g\in(0.4,0.6)$ <br> $g\in(0.7,0.9)$ | $4.390 \times 10^{-6}$ <br> $5.184 \times 10^{-6}$ <br> $1.474 \times 10^{-5}$ | $1.833$ <br> $1.994$ <br> $3.193$ |
| Case II| $g\in(0,0.2)$ <br> $g\in(0.4,0.6)$ <br> $g\in(0.7,0.9)$ | $4.931 \times 10^{-4}$ <br> $5.798 \times 10^{-4}$ <br> $2.870 \times 10^{-3}$ | $1.653$ <br> $1.827$ <br> 3.572$ |
| Case III | $g\in(0,0.2)$ <br> $g\in(0.4,0.6)$ <br> $g\in(0.7,0.9)$ | $1.065 \times 10^{-3}$ <br> $1.127 \times 10^{-3}$ <br> $1.853 \times 10^{-3}$ | $2.383$ <br> $2.452$ <br> 3.069$ |

</div>
</GlassCard>

<GlassCard
  title="Mesh dependency"
  variant="success"
  icon="i-ph-target-duotone"
  size="sm"
>

<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>

| **Test Dataset** | **Mesh Resolution** | **MSE** | **RMSPE($\%$)** |
| ---------------- | ------------------ | --------- | ------ |
| Validation | $40\times 40$<br>$20\times 20$<br>$10\times 10$ | $5.453\times 10^{-10}$<br>$8.235\times 10^{-9}$<br>$9.476\times 10^{-8}$ | $2.759$<br>$10.006$<br>$34.346$ |
| Case I | $40\times 40$<br>$20\times 20$<br>$10\times 10$ | $4.390 \times 10^{-6}$ <br> $1.876 \times 10^{-5}$ <br> $1.243 \times 10^{-4}$ | $1.833$ <br> $3.758$ <br> $9.276$ |
| Case II| $40\times 40$<br>$20\times 20$<br>$10\times 10$ | $4.931 \times 10^{-4}$ <br> $1.792 \times 10^{-2}$ <br> $3.687 \times 10^{-2}$ | $1.653$ <br> $9.952$ <br> $13.798$ |
| Case III | $40\times 40$<br>$20\times 20$<br>$10\times 10$ | $1.065 \times 10^{-3}$ <br> $1.175 \times 10^{-2}$ <br> $4.511 \times 10^{-2}$ | $2.383$ <br> $8.132$ <br> $15.477$ |

</div>
</GlassCard>
</div>

---

# Comparision with MIO

<GlassCard
  title="Comparision with MIO"
  variant="warning"
  icon="i-ph-target-duotone"
  size="lg"
>

<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>
<img src="/figs/vs-mio.png" />
</div>

<div strong text-center mt-4 text-xl equation-block>
<span text-2xl text-accent font-semibold>Fewer</span> parameters but <span text-2xl text-accent font-semibolt>Better</span> generalization
</div>
</GlassCard>

---

# Conclusion

<div class="mb-4 text-center">
  <div class="text-xl text-on-surface mb-2">
    <span class="emphasis-primary font-bold">Current Limitations</span> and Research Directions
  </div>
</div>

<div grid="~ cols-2 gap-6" mt-4>

<GlassCard
  title="Current Limitations"
  subtitle="Areas for improvement"
  variant="error"
  icon="i-ph-warning-duotone"
  size="md"
  :list-items="[
    '2D problems only',
    'Steady-state solutions',
    'Substantial pre-training data',
    'Memory constraints'
  ]"
/>

<GlassCard
  title="Future Directions"
  subtitle="Research opportunities"
  variant="success"
  icon="i-ph-rocket-launch-duotone"
  size="md"
  :list-items="[
    '3D extension',
    'Time-dependent problems',
    'Multi-physics coupling',
    'Uncertainty quantification'
  ]"
/>

</div>

<div class="mt-4">
  <GlassCard
    title="Broader Impact"
    variant="gradient-secondary"
    icon="i-ph-globe-duotone"
    size="sm"
  >
    <div class="text-center text-xs">
      <div class="mb-1">
        <strong>Applications:</strong> ICF design, medical imaging, astrophysics
      </div>
      <div>
        <strong>Impact:</strong> Real-time simulation and optimization
      </div>
    </div>
  </GlassCard>
</div>

---
layout: center
class: "text-center pb-5"
---

# Thank You!

<div class="mt-8 space-y-6">
  <div class="text-xl text-on-surface-variant">
    Questions & Discussion
  </div>

  <div class="grid grid-cols-3 gap-8 mt-12">
    <GlassCard
      title="Paper"
      variant="gradient-primary"
      icon="i-ph-file-text-duotone"
      size="sm"
      text-center
    >
      <div class="text-sm">
        DeepRTE: Pre-trained Attention-based Neural Network for Radiative Transfer
      </div>
    </GlassCard>
    <GlassCard
      title="Code"
      variant="gradient-secondary"
      icon="i-ph-code-duotone"
      size="sm"
      text-center
    >
      <div class="text-sm">
        Available on GitHub<br/>
        <Repo name="mazhengcn/deeprte" />
      </div>
    </GlassCard>
    <GlassCard
      title="Contact"
      variant="tech"
      icon="i-ph-envelope-duotone"
      size="sm"
      text-center
    >
      <div class="text-sm">
        Zheng Ma<br/>
        Shanghai Jiao Tong University
      </div>
    </GlassCard>
  </div>
</div>

Slides can be found [here](https://zheng-talks.netlify.app/2025/hksiam) -->
