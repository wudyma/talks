---
layout: cover
highlighter: shiki
css: unocss
colorSchema: auto
transition: fade
mdc: true
title: DeepRTE v1.2.0-zh
remoteAssets: true
date: 2026-02-01
export:
  dark: true
seoMeta:
  ogImage: auto
---

# DeepRTE {.emphasis-primary.text-4xl}

<div text-2xl class="text-on-surface-variant">基于注意力机制的辐射输运预训练神经算子</div>

<div mt15 />

<div flex="~ col gap-2">
  <div text-left text-2xl text-on-surface>马 征</div>
  <div text-left text-sm class="text-secondary">上海交通大学</div>
  <div text-left text-sm class="text-on-surface-variant">唐敏、竺烨锟，项目负责人：王涵、谌稳固</div>
</div>

<!-- SJTU Official Logo - Enhanced Glassmorphism with Theme Colors -->
<div class="absolute top-8 right-6 group">
  <div class="relative bg-gradient-to-br from-white/40 to-white/25 dark:from-neutral-900/30 dark:to-neutral-800/20 backdrop-blur-lg rounded-xl px-2 py-2 border border-sjtu-200/15 dark:border-sjtu-400/8 shadow-lg shadow-sjtu-500/8 dark:shadow-sjtu-400/5 hover:bg-white/50 dark:hover:bg-neutral-900/40 hover:border-sjtu-300/20 dark:hover:border-sjtu-400/12 transition-all duration-300">
    <img src="/images/sjtu-logo-zh.png" class="h-10 object-contain transition-all duration-300 emphasis-primary-logo" alt="Shanghai Jiao Tong University" />
  </div>
</div>

<style>
.emphasis-primary-logo {
  filter: brightness(0) saturate(100%) invert(36%) sepia(93%) saturate(4151%) hue-rotate(216deg) brightness(99%) contrast(92%);
}
.dark .emphasis-primary-logo {
  filter: brightness(0) saturate(100%) invert(58%) sepia(55%) saturate(2750%) hue-rotate(190deg) brightness(102%) contrast(95%);
}
</style>

<!-- Date positioned at bottom right with matching glassmorphism style -->
<div class="absolute bottom-8 right-6 group">
  <div class="relative bg-gradient-to-br from-white/40 to-white/25 dark:from-neutral-900/30 dark:to-neutral-800/20 backdrop-blur-lg rounded-lg px-3 py-1.5 border border-sjtu-200/15 dark:border-sjtu-400/8 shadow-lg shadow-sjtu-500/8 dark:shadow-sjtu-400/5 hover:bg-white/50 dark:hover:bg-neutral-900/40 hover:border-sjtu-300/20 dark:hover:border-sjtu-400/12 transition-all duration-300">
    <div text-xs class="text-on-surface-muted/80">2026年2月1日</div>
  </div>
</div>

---

# 背景

<div grid="~ cols-2 gap-6">
  <GlassCard
    title="惯性约束聚变"
    subtitle="清洁能源产生"
    variant="primary"
    icon="i-ph-atom-duotone"
    size="lg"
  >
    <div class="flex flex-col items-center gap-3">
      <img src="/icf.png" class="rounded-lg shadow-lg h-42 object-contain" />
      <div class="text-xs text-on-surface-variant text-center">
        辐射输运驱动聚变靶丸的内爆动力学
      </div>
    </div>
  </GlassCard>

  <GlassCard
    title="放射治疗"
    subtitle="精准癌症治疗"
    variant="secondary"
    icon="i-ph-heart-duotone"
    size="lg"
  >
    <div class="flex flex-col items-center gap-3">
      <img src="/rad-therapy.jpg" class="rounded-lg shadow-lg h-42 object-contain" />
      <div class="text-xs text-on-surface-variant text-center">
        精确的剂量计算以实现有效治疗
      </div>
    </div>
  </GlassCard>
</div>

<div mt-4>
  <GlassCard variant="tech" text-center size="md">
    <div class="text-lg mb-2">
      <span class="emphasis-tech font-semibold">核心挑战：</span>
      <span class="emphasis-primary font-semibold">辐射输运方程</span>的数值模拟
    </div>
    <div class="text-sm text-on-surface-variant">
      高维相空间 • 复杂碰撞算子 • 多尺度物理
    </div>
  </GlassCard>
</div>

---

# 辐射输运方程

<div class="mb-4">
  <GlassCard variant="primary" size="md" title="控制方程">
  <div class="text-center mb-4">
  <!-- <div class="text-lg font-semibold text-on-surface mb-2">控制方程</div> -->
  <div class="equation-block">

  $$
  \Omega \cdot \nabla I(r, \Omega) + \mu_t(r) I(r, \Omega) = \frac{\mu_s(r)}{S_{d-1}}\int_{\mathbb{S}^{d-1}} p(\Omega, \Omega^*) I(r, \Omega^*)\,\mathrm{d}\Omega^*
  $$

  </div>
  </div>
  <div class="flex justify-around items-center gap-6">
  <div flex="~ gap-2 items-center">
  <strong>

  $I(r,\Omega)$:

  </strong>

  相空间 $(r,\Omega)$ 处的辐射强度

  </div>
  <div flex="~ gap-2 items-center">
  <strong>

  $\mu_t(r)$:

  </strong>
  总截面
  </div>
  <div flex="~ gap-2 items-center">
  <strong>

  $\mu_s(r)$:

  </strong>
  散射截面
  </div>
  <div flex="~ gap-2 items-center"><strong>

  $p(\Omega,\Omega^*)$:

  </strong>
  散射核
  </div>
  </div>
  </GlassCard>
</div>

<GlassCard title="边界条件" variant="secondary" size="md">
<div class="text-center text-on-surface-variant">
<div class="equation-block" flex="~ gap-2 items-center justify-center">

$I |_{\Gamma_{-}}(r,\Omega) = I_{-}(r,\Omega)$

where

$\Gamma_{\pm} := \{(r,\Omega) \mid r\in\partial D,\;\Omega\in\mathbb{S}^{d-1},\;\mp n(r)\cdot\Omega<0 \}$

</div>
</div>
</GlassCard>

---

# 数值挑战

<div grid="~ gap-4 cols-3" mt-6>

<GlassCard
  title="高维"
  subtitle="维数灾难"
  variant="error"
  icon="i-ph-cube-duotone"
  size="lg"
  :list-items="[
    '6维相空间: $(x,y,z,\\Omega_x,\\Omega_y,\\Omega_z)$',
    '网格点数呈指数增长 $N^6$',
    '难以承受的内存和存储需求'
  ]"
  :enable-latex="true"
/>

<GlassCard
  title="复杂碰撞"
  subtitle="非线性相互作用"
  variant="warning"
  icon="i-ph-arrows-merge-duotone"
  size="lg"
  :list-items="[
    '在离散层面保持守恒律',
    '处理非线性玻尔兹曼型算子',
    '避免虚假射线效应和扩散'
  ]"
/>

<GlassCard
  title="多尺度物理"
  subtitle="区域耦合"
  variant="tech"
  icon="i-ph-scales-duotone"
  size="lg"
  :list-items="[
    '刚性参数: $\\varepsilon = \\ell/L \\ll 1$',
    '设计渐近保持格式',
    '耦合输运 ↔ 扩散转变'
  ]"
  :enable-latex="true"
/>

</div>

<div class="mt-4">
  <GlassCard variant="gradient-primary" text-center size="lg">
    <div class="font-semibold mb-1">
      <span class="emphasis-tech">为什么使用深度学习？</span>
    </div>
    <div class="opacity-90">
      神经网络有望克服维数灾难并学习复杂的多尺度行为
    </div>
  </GlassCard>
</div>

---

# 传统方法

<!-- <div class="mb-4 text-center">
  <div class="text-lg text-on-surface mb-2">现有方法难以应对计算障碍</div>
</div> -->

<div grid="~ cols-2 gap-6" mt-6>

<div>
  <GlassCard
    title="概率方法"
    subtitle="统计采样"
    variant="primary"
    icon="i-ph-dice-six-duotone"
    size="md"
  >
    <div class="space-y-3 text-base">
      <div>
        <div class="font-semibold mb-1">蒙特卡洛输运:</div>
        <div class="space-y-0.5 pl-2">
          <div>• MCNP, COG (LLNL), Mercury</div>
        </div>
      </div>
      <div>
        <div class="font-semibold mb-1">直接模拟:</div>
        <div class="space-y-0.5 pl-2">
          <div>• DSMC (Bird, Nanbu), Sparta (ORNL)</div>
        </div>
      </div>
    </div>
  </GlassCard>
</div>

<div>
  <GlassCard
    title="确定性方法"
    subtitle="基于网格的离散化"
    variant="secondary"
    icon="i-ph-grid-four-duotone"
    size="md"
  >
    <div class="space-y-3 text-base">
      <div>
        <div class="font-semibold mb-1">离散纵标法:</div>
        <div class="space-y-0.5 pl-2">
          <div>• Ardra (LLNL), NEWT (ORNL), DORT</div>
        </div>
      </div>
      <div>
        <div class="font-semibold mb-1">谱方法:</div>
        <div class="space-y-0.5 pl-2">
          <div>• 高阶精度，光滑重构</div>
        </div>
      </div>
    </div>
  </GlassCard>
</div>

</div>

<div class="mt-6 text-base">
  <ProsCons
    :pros="[
      '蒙特卡洛：易于并行',
      '确定性方法：精确守恒',
      '两者：理论成熟'
    ]"
    :cons="[
      '蒙特卡洛：收敛慢 $\\sqrt{N}$',
      '确定性方法：指数级增长',
      '两者：难以处理高维问题'
    ]"
  />
</div>

---
layout: center
---

<div flex="~ col gap-5 items-center">
  <div font-600 m--2 text-center>

  # 深度学习方法可能成为新途径

  </div>
  <div text-2xl op75 text-center>克服维数灾难</div>
</div>

---

# 用深度学习求解 PDEs

<div flex="~ col gap-2">

<div>
  <GlassCard
    title="架构：假设空间"
    variant="success"
    icon="i-ph-fediverse-logo-duotone"
    size="md"
    :list-items="[
      '近似解: PINNs, DeepRitz 等',
      '近似解算子: DeepONet, FNO 等',
      '近似 PDE (从方程到解): PDEFormer-1/2'
    ]"
  />
</div>

<div>
  <GlassCard
    title="约束：最小化问题的损失函数"
    variant="error"
    icon="i-carbon:constraint"
    size="md"
    :list-items="[
      '数据：纯监督或作为先验信息',
      '模型：需要物理信息 (PDE) (如 PINNs, DeepRitz, DeepGalerkin)',
      '其他：初值、边界、守恒、对称性等'
    ]"
  />
</div>

<div>
  <GlassCard
    title="优化"
    variant="warning"
    icon="i-streamline:graph-arrow-decrease"
    size="md"
    :list-items="[
      '在参数空间上最小化损失，通常使用 SGD, Adams, LBFGS 等',
    ]"
  />
</div>

</div>

---
glow: left
---

# DeepRTE

<!-- <div class="mb-4 text-center">
  <div class="text-lg text-on-surface mb-1">
    用于<span class="emphasis-primary font-bold">辐射输运方程</span>的<span class="emphasis-primary font-bold">深度</span>学习
  </div>
</div> -->

<div class="mt-10" />

<div grid="~ cols-[1fr_min-content_1fr] items-center gap-15" mt-5 w-full>

<div>
  <GlassCard
    title="神经算子"
    subtitle="学习到解的映射"
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
        '基于注意力的 Transformer',
        '分辨率无关',
        '参数到解的映射'
      ]"
    />
  </div>
  </div>
  </GlassCard>
</div>

<div i-ph:plus-duotone text-6xl op50 />

<div>
  <GlassCard
    title="预训练"
    subtitle="为 RTE 定制的数据集"
    variant="tech"
    icon="i-ph-database-duotone"
    size="lg"
  >
    <div class="space-y-4">
      <div class="text-center">
        <div class="grid grid-cols-3 gap-2 text-sm">
          <div class="bg-error-100/50 dark:bg-error-900/30 rounded-lg p-3">
            生成<br/>数据
          </div>
          <div class="bg-warning-100/50 dark:bg-warning-900/30 rounded-lg p-3">
            训练<br/>算子
          </div>
          <div class="bg-success-100/50 dark:bg-success-900/30 rounded-lg p-3">
            迁移<br/>学习
          </div>
        </div>
      </div>
      <div class="text-sm space-y-2">
        <List
          variant="primary"
          :list-items="[
            'Delta 函数数据',
            '端到端预训练',
            '零样本泛化'
          ]"
        />
      </div>
    </div>
  </GlassCard>
</div>

</div>

<div class="mt-6">
  <GlassCard variant="gradient-primary" text-center size="lg" w-full>
    <div class="font-semibold text-lg">
      <span class="emphasis-tech">关键优势：</span>
      一次训练，解决各类 RTE 问题
    </div>
  </GlassCard>
</div>

---
glow: right
---

# 为什么不用 DeepONet?
DeepONet 在辐射输运问题上存在根本局限

<div grid="~ cols-2 gap-6" mt-6 items-stretch>

<div>
  <GlassCard
    title="DeepONet 的局限性"
    variant="error"
    icon="i-ph-x-circle-duotone"
    size="lg"
    class="h-full"
  >
    <div class="space-y-4" mt-8>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">固定离散化：</div>
        <div class="text-2xs text-on-surface-variant">
          需要固定网格点，限制了灵活性
        </div>
      </div>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">参数缩放：</div>
        <div class="text-2xs text-on-surface-variant">
          网络规模随输入维度增长
        </div>
      </div>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">多输入挑战：</div>
        <div class="text-2xs text-on-surface-variant">
          难以处理多个输入函数
        </div>
      </div>
    </div>
  </GlassCard>
</div>

<div>
  <GlassCard
    title="DeepONet 结构"
    variant="warning"
    icon="i-ph-tree-structure-duotone"
    size="lg"
    class="h-full"
  >
    <div class="text-center">
      <img src="/deeponet.png" class="rounded-lg shadow-sm mx-auto" alt="DeepONet"/>
      <div class="text-2xs text-on-surface-variant py-3 mb--4">
        Branch + Trunk 架构
      </div>
    </div>
  </GlassCard>
</div>

</div>

---
glow: left
---

# 为什么不用 FNO?
傅里叶神经算子在辐射输运问题上存在结构局限

<div grid="~ cols-2 gap-6" mt-6 items-stretch>

<div>
  <GlassCard
    title="FNO 的局限性"
    variant="error"
    icon="i-ph:x-circle-duotone"
    size="lg"
    class="h-full"
  >
    <div class="space-y-2">
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">均匀网格要求：</div>
        <div class="text-2xs text-on-surface-variant">
          输入函数必须在均匀网格上，限制了几何灵活性
        </div>
      </div>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">FFT 计算成本：</div>
        <div class="text-2xs text-on-surface-variant">
          随着函数维度增加，FFT 运算变慢
        </div>
      </div>
      <div>
        <div class="font-semibold mb-0.5 text-error-600 dark:text-error-400">频域假设：</div>
        <div class="text-2xs text-on-surface-variant">
          依赖谱衰减，这对 RTE 可能不成立
        </div>
      </div>
    </div>
  </GlassCard>
</div>

<div>
  <GlassCard
    title="FNO 结构"
    variant="warning"
    icon="i-ph:tree-structure-duotone"
    size="lg"
    class="h-full"
  >
    <div class="text-center space-y-4">
      <img src="/fno.png" class="rounded-lg shadow-sm mx-auto" alt="FNO Architecture"/>
      <div class="text-2xs text-on-surface-variant py-3">
        基于傅里叶层的神经算子
      </div>
      <div class="bg-warning-100/50 dark:bg-warning-900/30 rounded-lg p-2">
        <div class="text-2xs font-semibold text-warning-600 dark:text-warning-400">
          RTE 挑战：不规则几何和高维性
        </div>
      </div>
    </div>
  </GlassCard>
</div>
</div>

---

# 我们的目标

端到端方式

<GlassCard title="学习解算子" variant="primary">
<div class="equation-block">

$$
\mathcal{A}: (I_-; \mu_t, \mu_s, p) \mapsto I
$$

</div>
</GlassCard>

<div grid="~ cols-[2fr_auto_1.3fr] items-center gap-15" mt-5>

<GlassCard
  title="输入"
  variant="warning"
  size="md"
>
<List
  variant="warning"
  enable-latex="true"
  :list-items="[
    '$I_{-}(r,\\Omega)$: 入射边界函数',
    '$\\mu_t(r)$: 总截面',
    '$\\mu_s(r)$: 散射截面',
    '$' + 'p(\\Omega,\\Omega^*)$: 散射核函数'
  ]"
/>
</GlassCard>

<div i-ph:arrow-right-duotone text-5xl op-50 />

<GlassCard title="输出" variant="success" size="md">
<div class="equation-block py-6 mt-9 mb-4 mx-4">

$$
I(r, \Omega)
$$

</div>
</GlassCard>

</div>

---

# 想法

格林函数：

<GlassCard title="用神经网络近似解的积分核" variant="secondary" size="md">
<div class="equation-block">

$$
I(r, \Omega)\approx \int_{\Gamma_-} G^{\text{NN}}(r, r', \Omega, \Omega'; \mu_t, \mu_s, p) I_-(r',\Omega') \, \mathrm{d}r' \mathrm{d}\Omega'
$$

</div>

<div class="text-on-surface-variant space-y--2">
<div flex="~ gap-4 items-center">
<div i-ph:square-duotone text="academic/70 sm" />
<div>

解 $I$ 关于边界 $I_{-}$ 是<span class="text-academic">线性</span>的

</div>
</div>
<div flex="~ gap-4 items-center">
<div i-ph:square-duotone text="academic/70 sm" />
<div>

格林函数 $G^{\text{NN}}$ 关于 $\mu_t$, $\mu_s$ 和 $p$ 是<span text-academic>非线性</span>的

</div>
</div>
<div flex="~ gap-4 items-center">
<div i-ph:square-duotone text="academic/70 sm" />
<div>

格林函数 $G^{\text{NN}}$ 对 $\mu_t$ 和 $\mu_s$ 的依赖是<span text-academic>非局部</span>的

</div>
</div>
</div>
</GlassCard>

<GlassCard variant="success" mt-4 text="center xl success">
从格林函数/解算子的“解析”结构入手
</GlassCard>

---

# 解算子的结构

<div flex="~ col gap-2">
<GlassCard title="稳态 RTE" variant="primary" size="md">
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

<GlassCard title="衰减" size="md" variant="success">
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

<GlassCard title="散射" size="md" variant="warning">
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

# 解算子的结构

<div class="mt-5" />

<div grid="~ cols-[max-content_min-content_auto] gap-4 items-center" w-full>
<GlassCard title="衰减" size="sm" variant="success">
<div class="equation-block">

$$
\Omega \cdot \nabla I + \mu_t I = 0, \; I|_{\Gamma_{-}} = I_{-}.
$$

</div>
</GlassCard>

<div i-ph:arrow-right-duotone op-50 text-4xl />

<GlassCard title="$\mathcal{J}$ 算子" size="sm" variant="success" enable-latex="true">
<div class="equation-block">

$$
I(r,\Omega) = \mathcal{J}I_{-}:=e^{-{\color{pink}\tau(0,s_{-})}}I_{-}(r-s_{-}\Omega,\Omega).
$$

</div>
</GlassCard>

<GlassCard title="散射" size="sm" variant="warning" h-34>
<div class="equation-block">

$$
\Omega \cdot \nabla I + \mu_t I = \mu_s\mathcal{S}I, \; I|_{\Gamma_{-}} = 0.
$$

</div>
</GlassCard>

<div i-ph:arrow-right-duotone op-50 text-4xl />

<GlassCard title="$\mathcal{L}$ 和 $\mathcal{S}$ 算子" size="sm" variant="warning" enable-latex="true">
<div class="equation-block">

$$
I(r,\Omega) = \mathcal{L}\mathcal{S}I:=\int_0^{s_{-}}e^{-{\color{pink}\tau(0,s)}}\mu_s(r-s\Omega)\mathcal{S}I(r-s\Omega,\Omega)\,\mathrm{d}s
$$

</div>
</GlassCard>
</div>

<GlassCard title="稳态 RTE 的积分形式" variant="error" size="sm" mt-4>
<div flex="~ gap-2 items-center justify-center">
<div equation-block text-base px-4>

$$
I = \mathcal{L}\mathcal{S}I + \mathcal{J}I_{-}
$$

</div>
其中 <span text-pink-3>光学深度</span> 定义为：
<div equation-block text-pink-3 py--2 px-4>

$$
\tau(s_1,s_2):=\int_{s_1}^{s_2}\mu_t(r-s\Omega)\,\mathrm{d}s
$$

</div>
</div>
</GlassCard>

---

# DeepRTE: 架构

概览

<GlassCard
  title="格林函数也满足"
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
  title="迭代作为神经网络的模块组合"
  subtitle="受源迭代法启发"
  size="md"
  mt-5
  >
<div flex="~ gap-4 items-center justify-center" text-base>
<div>

第 $\ell$ 个模块：

</div>
<div equation-block>

$$
G^{\ell+1} = \mathcal{L}\mathcal{S}G^{\ell} + G^0
$$

</div>
<div>其中</div>
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
    '$\\mathcal{J}$, $\\mathcal{L}$: 衰减模块（沿特征线的注意力）',
    '$\\mathcal{S}$: 散射模块'
  ]"
  enable-latex="true"
/>
</div>

</GlassCard>

---

# 衰减模块

$\mathcal{J}$ 和 $\mathcal{L}$

<div flex="~ col gap-4 items-center">
<GlassCard title="$\mathcal{J}$ 算子为例" size="md" variant="success" enable-latex="true">
<div class="equation-block">

$$
G^0(r,r',\Omega,\Omega';\mu_t)= \mathcal{J}\left(\delta_{\{r'\}}(r)\delta(\Omega-\Omega')\right)=e^{-{\color{pink}\tau(0,s_{-})}}\left(\delta_{\{r'\}}(r)\delta(\Omega-\Omega')\right)\approx \text{MLP}(r,r,\Omega,\Omega';\tau^{\text{NN}})
$$

</div>
</GlassCard>

<div i-ph:arrow-fat-lines-up-duotone text-4xl op-50 />

<GlassCard title="光学深度网络" size="md" variant="error" enable-latex="true">
<div class="equation-block">

$$
\tau^{\text{NN}}(r,\Omega)\approx\tau(0,s_{-})=\int_0^{s_{-}(r,\Omega)}\mu_t(r-s\Omega)\,\mathrm{d}s
$$

</div>
</GlassCard>
</div>

---

# 光学深度网络

<GlassCard title="沿特征线的注意力" variant="error">
<div flex="~ col gap-2">
<div equation-block>

$$
\tau^\text{NN} = \text{OpticalDepthNet}\left(r,\Omega; \{r^\text{mesh}_i\}, \{(\mu_t^{\text{mesh}})_i\}\right) = \text{MultiHead}(Q, K, V)
$$

</div>
<div text-xs flex="~ gap-2 items-center" ml-28>
<div>其中</div>
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

<GlassCard variant="secondary" title="相对位置编码" mt-4>
<div equation-block>

$$
{(r^\text{mesh}_{\text{local}})}_i = \left({(r^\text{mesh}_\text{local})}_i, {(\theta^\text{mesh}_\text{local})}_i\right)
= \left((r-r^{\text{mesh}}_i)\cdot\Omega, \frac{(r-r^{\text{mesh}}_i)}{
\| r-r^{\text{mesh}}_i\|}\cdot \Omega\right)
$$

</div>
</GlassCard>

---

# 光学深度网络

<!-- <div class="mt-8" /> -->

<div flex="~ col gap-4 items-center">
<div flex="~ gap-4 items-center">
<GlassCard variant="success" size="sm" class="p-4">
<div equation-block class="px-4">

$$
\tau(r,\Omega) \approx  \sum_{j}^{N\left(s_{-}(r,\Omega)\right)} w(r, \Omega;s_j)\mu_t(r-s_j \Omega),
$$

</div>
</GlassCard>
<div i-ph:arrow-fat-lines-left-duotone text-3xl op-50 />
<GlassCard variant="secondary" size="sm" class="p-4">
<div equation-block class="px-4">

$$
\mu_t(r-s_j \Omega)\approx  \sum_{i}^{N_\text{mesh}} \bm{1}_{\mathcal{C}_{r,\Omega}}(r_i^{\text{mesh}}) c(r-s_j\Omega, r^{\text{mesh}}_i){(\mu_t^\text{mesh})}_i,
$$

</div>
</GlassCard>
</div>

<div i-ph:arrows-merge-duotone text-4xl op-50 ml--22 />

<GlassCard variant="error" size="sm" class="p-5">
<div equation-block text-xs class="px-4">

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

# 光学深度网络

<GlassCard title="沿特征线的注意力" variant="primary">
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

# 衰减模块

总结

<GlassCard title="衰减模块示意图" variant="secondary" size="lg">
<div bg-white:95 rounded-xl p-4 mt-5>
  <img src="/figs/attenuation_module.png" />
</div>
</GlassCard>

---

# 散射模块

<GlassCard title="散射作为迭代" size="md" variant="primary">
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

# 散射块

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

# DeepRTE 架构

回顾

<div grid="~ cols-2 gap-6" mt-4>

<div>
  <GlassCard
    title="衰减模块"
    subtitle="输运编码"
    variant="primary"
    icon="i-ph-tree-structure-duotone"
    size="md"
    :list-items="[
      '将 $\\mu_t(r)$ 和 $\\mu_s(r)$ 编码为光学深度网络',
      '沿特征线的注意力',
    ]"
    :enable-latex="true"
  />
</div>

<div>
  <GlassCard
    title="散射模块"
    subtitle="散射编码"
    variant="secondary"
    icon="i-ph-tree-structure-duotone"
    size="md"
    :list-items="[
      '编码 $' + 'p(\\Omega,\\Omega^*)$',
      '捕捉各向异性散射'
    ]"
    :enable-latex="true"
  />
</div>
</div>

<div bg-white:95 rounded-xl p-2 mt-4 flex="~ justify-center">
  <img src="/figs/architecture.png" h-50 />
</div>

---

# 训练策略

使用类 Delta 函数训练

<GlassCard
  title="数据集"
  subtitle="为了具备零样本能力"
  variant="warning"
  icon="i-ph-database-duotone"
  size="lg"
>

<div flex="~ col gap-2" ml--2>

<List variant="secondary" :list-items="['我们构建由 Delta 函数组成的训练数据集']" />
<div text-on-surface>

$$
I^\sigma_{-}(r, \Omega; r', \Omega') =
\delta_{\{r'\}}(r)\delta(\Omega-\Omega'), \quad (r,\Omega) \in \Gamma_{-}.
$$

</div>
<List variant="secondary" :list-items="['实际上，我们使用 Delta 函数的平滑版本作为边界函数']" />
<div text-on-surface>

$$
\delta_{\{r'\}}^{\sigma}(r) = \frac{1}{\sigma \sqrt{\pi}} \exp\left( -\frac{(r-r')^2}{\sigma^2} \right), \quad
\delta^{\sigma}(\Omega-\Omega') = \frac{1}{\sigma \sqrt{\pi}} \exp\left( -\frac{(\Omega-\Omega')^2}{\sigma^2} \right),
$$

</div>
</div>
</GlassCard>

---

# 训练策略

<GlassCard title="定理" variant="success" icon="i-arcticons:math-riddles" size="lg">
<div class="text-on-surface">

设 $\mathcal{A}$ 和 $\mathcal{A}^{\text{NN}}_{\theta^*}$ 分别为 RTE 和<span class="text-orange">学习到的</span> DeepRTE 算子。对于任意 $I_-\in L^2(\Gamma_-)$ 以及其近似 $I_{-, h}^\sigma$。如果存在神经网络参数集 $\theta^*$ 使得：

</div>
<div class="equation-block">

$$
\|\mathcal{A}^{\text{NN}}_{\theta^*}I^\sigma_{-,h} - \mathcal{A}I^\sigma_{-,h}\|\leq \varepsilon, \quad \forall I^\sigma_{-,h} \in \text{Delta 函数{\color{orange}测试数据集}},
$$

</div>

那么我们有：

<div class="equation-block">

$$
\begin{aligned}
  \|\mathcal{A}^{\text{NN}}_{\theta^*} I_- - \mathcal{A} I_-\|_{L^2(D\times\mathbb{S}^{d-1})}\leq C\left\{ \sigma^k \|I_-\|_{H^k(\Gamma_-)} + \left(\frac{h}{\sigma}\right)^m \|I_-\|_{H^m(\Gamma_-)} + \varepsilon\right\}.
\end{aligned}
$$

</div>
</GlassCard>

---

# 训练策略

<div grid="~ cols-[max-content_auto] gap-4">

<GlassCard
  title="RTE 特征"
  variant="warning"
  icon="i-ph-database-duotone"
  size="md"
>
<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>

| **特征与形状** | **描述** |
| ---------------- | ----------- |
| phase_coords: $[N_{\text{coords}}, 2d]$ | 相空间坐标 $(r,\Omega)$ |
| boundary_coords: $[N_{\text{bc}}, 2d]$ | 边界坐标 $(r',\Omega')$ |
| position_coords: $[N_{\text{mesh}}, 2d]$ | 网格点 $(r^{\text{mesh}})$ |
| velocity_coords: $[N_{\text{quad}}, 2d]$ | 角度求积点 $\Omega^*$ |
| boundary: $[N_{\text{bc}}]$ | 边界 $I(r',\Omega')$ |
| mu: $[N_{\text{mesh}}, 2]$ | 截面 $\mu_t$ 和 $\mu_s$ |
| scattering_kernel: $[N_{\text{quad}}]$ | 散射核 $p(\Omega,\Omega^*)$ |

</div>
</GlassCard>

<GlassCard
  title="训练设置"
  variant="success"
  icon="i-ph-gear-duotone"
  size="md"
>

<div flex="~ col gap-2" ml--2 mt-3>

<List variant="success" :list-items="['Adam 优化器', '余弦退火学习率调度']" />
<List variant="success" :list-items="['MSE 损失']" />

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

# 实验设置

<div mt-2 />

令
$$
\Omega=(c,s,\zeta), \quad c =
{\left(1-\zeta^{2}\right)}^{\frac{1}{2}} \cos\theta, \quad s =
{\left(1-\zeta^{2}\right)}^{\frac{1}{2}} \sin\theta, \quad \text{for }|\zeta| \leq 1.
$$

<GlassCard
  title="降维 2-D RTE"
  variant="primary"
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
  title="Henyey-Greenstein (H-G) 散射核"
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

# 实验设置

<GlassCard
  title="训练边界条件"
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
  title="截面"
  variant="secondary"
  size="sm"
>
<div equation-block>

$$
\begin{aligned}
\mu_t(x,y) &=
\begin{cases}
U_t, \quad \text{其中 } U_t \sim \mathcal{U}(5,7) & \text{若 } (x,y) \in D_\mu \\
10 & \text{若 } (x,y) \notin D_\mu
\end{cases} \\
\mu_s(x,y) &=
\begin{cases}
U_s, \quad \text{其中 } U_s \sim \mathcal{U}(2,4) & \text{若 } (x,y) \in D_\mu \\
5 & \text{若 } (x,y) \notin D_\mu
\end{cases}
\end{aligned}
$$

</div>
</GlassCard>

<GlassCard
  title="散射核"
  variant="success"
  size="sm"
>
<div equation-block>
<div py-3 text-base>

$$
g \sim
\begin{cases}
\mathcal{U}(0,0.2),  & \quad \text{近各向同性} \\
\mathcal{U}(0.4,0.6), & \quad \text{中等各向异性} \\
\mathcal{U}(0.7,0.9), & \quad \text{强各向异性} \\
\end{cases}
$$

</div>
</div>
</GlassCard>
</div>

---

# 数据集参数

<div bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden mt--2>

| 类别 | 参数 | 符号 | 值/范围 |
| -------- | ---------- | ------ | ----------- |
| 空间域 | 域<br> 子域 | $D$ <br>  $D_\mu$  | ${[0,1]}^2$ <br> ${[0.4,0.6]}^2$ |
| 截面 | 总 <br> 散射 | $\mu_t$ <br> $\mu_s$ | $\mathcal{U}(5,7)$ in $D_\mu$ and $10$ in $D\backslash D_\mu$ <br>  $\mathcal{U}(2,4)$ in $D_\mu$ and $5$ in $D\backslash D_\mu$ |
| 离散化 | 网格点数 <br> 角度求积点数 | $N_{\text{mesh}}$ <br> $N_\text{quad}$  | $40$ <br> $24$ |
| 边界条件 | 波束空间中心坐标 <br><div mt-2 /> 波束角度求积点 <br><div mt-3 /> 波束空间标准差 <br> 波束角度标准差 | $y_l', y_r', x_b', x_t'$ <br> $c_l', c_r', c_b', c_t'$ <br> $s_l', s_r', s_b', s_t'$ <br> $\sigma_{r}$ <br> $\sigma_{\Omega}$ | 从网格点采样 <br><div mt-2 /> 从求积点采样 <br><div mt-3 /> $\sqrt{2}\,\mathcal{U}(0.005, 0.02)$ <br> $\sqrt{2}\,\mathcal{U}(0.005, 0.01)$ |
| 散射 | 不对称参数 | $g$ | $\mathcal{U}(0,0.2)$ <br> $\mathcal{U}(0.4,0.6)$ <br> $\mathcal{U}(0.7,0.9)$ |

</div>

---
class: pt-4
---

# 超参数

<div grid="~ cols-2 gap-6" mt--2>

<GlassCard
  title="神经网络"
  variant="warning"
  icon="i-ph-fediverse-logo-duotone"
  size="md"
>
<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden mt-16>

| **模块名称** | **超参数** | **值** |
| ---------------- | ------------------ | --------- |
| 衰减 | $\texttt{num\_layer}$: $N_{\text{mlp}}$ <br> $\texttt{hidden\_dim}$: $d_{\text{mlp}}$ <br> $\texttt{output\_dim}$: $d_{\text{model}}$ <br> $\texttt{num\_head}$: $N_{\text{head}}$ <br> $\texttt{key\_dim}$: $d_k$ <br> $\texttt{value\_dim}$: $d_v$ <br> $\texttt{output\_dim}$: $d_{\tau}$ | $4$ <br> $128$ <br> $16$ <br> $2$ <br> $32$ <br> $32$ <br> $2$ |
| 散射 | $\texttt{num\_block}$: $N_{\ell}$ <br> $\texttt{latent\_dim}$: $d_{\text{model}}$ | $2$ <br> $16$ |

</div>
</GlassCard>

<GlassCard
  title="训练"
  variant="success"
  icon="i-streamline:graph-arrow-decrease"
  size="md"
>

<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>

| **超参数** | **值** |
| --------------------| --------- |
| 优化器 | Adam |
| 学习率调度 | Cosine annealing |
| 初始学习率 | $1\times 10^{-3}$ |
| 批次大小 | $8$ |
| Epochs | $5000$ |
| 训练数据数量 | $800$ |
| 验证数据数量 | $200$ |
| 配点数量 | $128$ |

</div>
</GlassCard>
</div>

---

# 结果：精度

与训练数据集同分布

<GlassCard
  title="精度验证"
  subtitle="类 Delta 函数"
  variant="success"
  icon="i-ph-check-duotone"
  size="lg"
  mt-10
>
<div bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text text-on-surface overflow-hidden text-lg>

| **模型** | **参数量** | **散射区域** | **$g$ 范围** | **MSE($\times 10^{-10}$)** | **RMSPE($\%$)** |
| -------------------- | --------- | --------- | -------- | -------- | --------- |
| DeepRTE | $37954$ | 近各向同性 <br> 中等各向异性 <br> 强各向异性 | $(0, 0.2)$ <br> $(0.4,0.6)$ <br> $(0.7,0.9)$ | $5.630$ <br> $5.453$ <br> $7.223$ | $2.827$ <br> $2.759$ <br> $3.181$ |

</div>
</GlassCard>

---

# 结果

<div rounded-xl flex="~ justify-center" mt--1>
<img src="/figs/accuracy.png" h-110 rounded-lg bg-white p-2 />
</div>

---

# 泛化能力

<div class="mb-2 text-center">
  <div class="text-xl text-on-surface mb-2">
    超越训练分布的<span class="emphasis-primary font-bold">零样本泛化</span>
  </div>
</div>

<div grid="~ cols-2 gap-6" mt-4>

<GlassCard
  title="分布外测试"
  subtitle="挑战性场景"
  variant="tech"
  icon="i-ph-arrows-out-duotone"
  size="md"
  :list-items="[
    '不同的边界条件',
    '不同的截面和散射核'
  ]"
/>

<GlassCard
  title="迁移学习"
  subtitle="零样本适应"
  variant="secondary"
  icon="i-ph-swap-duotone"
  size="md"
  :list-items="[
    '在 Delta 边界上预训练',
    '高精度 (< 5% 误差)'
  ]"
/>

</div>

<div class="mt-4">
<GlassCard
  title="3 个案例"
  variant="gradient-secondary"
  icon="i-ph:balance-duotone"
  size="md"
>
<div flex="~ col items-center gap-2">
<div equation-block>
<div class="grid grid-cols-3 gap-3 text-sm text-center">
  <div>
    <div class="font-semibold mb-1">案例 I</div>
    <div>常数边界条件</div>
  </div>
  <div>
    <div class="font-semibold mb-1">案例 II</div>
    <div>三角函数边界条件</div>
  </div>
  <div>
    <div class="font-semibold mb-1">案例 III</div>
    <div>速度依赖边界条件</div>
  </div>
</div>
</div>
<div i-ph:x-duotone text-3xl op-50 />
<div equation-block text-sm py-0 px-3>

$$
g \sim (0, 0.2), (0.4, 0.6), (0.7, 0.9)
$$

</div>
</div>
</GlassCard>
</div>

---

# 案例 I:

无需进一步训练

<GlassCard title="常数边界条件" variant="primary" size="sm">
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

# 案例 II:

无需进一步训练

<GlassCard title="三角函数边界条件" variant="secondary" size="sm">
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
其中
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

# 案例 III:

无需进一步训练

<GlassCard title="速度依赖边界条件" variant="success" size="sm">
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
其中
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

# 结果：总结

<div grid="~ cols-[1fr_1.2fr] gap-4" mt--2>

<GlassCard
  title="零样本性能"
  variant="warning"
  icon="i-ph-arrows-out-duotone"
  size="sm"
>
<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden mt-10>

|       | **测试数据集** | **MSE** | **RMSPE($\%$)** |
| ---------------- | ------------------ | --------- | ------ |
| 案例 I | $g\in(0,0.2)$ <br> $g\in(0.4,0.6)$ <br> $g\in(0.7,0.9)$ | $4.390 \times 10^{-6}$ <br> $5.184 \times 10^{-6}$ <br> $1.474 \times 10^{-5}$ | $1.833$ <br> $1.994$ <br> $3.193$ |
| 案例 II| $g\in(0,0.2)$ <br> $g\in(0.4,0.6)$ <br> $g\in(0.7,0.9)$ | $4.931 \times 10^{-4}$ <br> $5.798 \times 10^{-4}$ <br> $2.870 \times 10^{-3}$ | $1.653$ <br> $1.827$ <br> 3.572$ |
| 案例 III | $g\in(0,0.2)$ <br> $g\in(0.4,0.6)$ <br> $g\in(0.7,0.9)$ | $1.065 \times 10^{-3}$ <br> $1.127 \times 10^{-3}$ <br> $1.853 \times 10^{-3}$ | $2.383$ <br> $2.452$ <br> 3.069$ |

</div>
</GlassCard>

<GlassCard
  title="网格依赖性"
  variant="success"
  icon="i-ph-checkerboard-duotone"
  size="sm"
>

<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>

| **测试数据集** | **网格分辨率** | **MSE** | **RMSPE($\%$)** |
| ---------------- | ------------------ | --------- | ------ |
| 验证集 | $40\times 40$<br>$20\times 20$<br>$10\times 10$ | $5.453\times 10^{-10}$<br>$8.235\times 10^{-9}$<br>$9.476\times 10^{-8}$ | $2.759$<br>$10.006$<br>$34.346$ |
| 案例 I | $40\times 40$<br>$20\times 20$<br>$10\times 10$ | $4.390 \times 10^{-6}$ <br> $1.876 \times 10^{-5}$ <br> $1.243 \times 10^{-4}$ | $1.833$ <br> $3.758$ <br> $9.276$ |
| 案例 II| $40\times 40$<br>$20\times 20$<br>$10\times 10$ | $4.931 \times 10^{-4}$ <br> $1.792 \times 10^{-2}$ <br> $3.687 \times 10^{-2}$ | $1.653$ <br> $9.952$ <br> $13.798$ |
| 案例 III | $40\times 40$<br>$20\times 20$<br>$10\times 10$ | $1.065 \times 10^{-3}$ <br> $1.175 \times 10^{-2}$ <br> $4.511 \times 10^{-2}$ | $2.383$ <br> $8.132$ <br> $15.477$ |

</div>
</GlassCard>
</div>

---

# 效率

<div class="mt-10" />

<GlassCard
  title="与经典方法的比较"
  variant="warning"
  icon="i-ph-caret-double-right-duotone"
  size="lg"
>

<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>
<img src="/figs/efficiency.png" />
</div>

<div strong text-center mt-4 text-xl equation-block>
即使在多 <span text-2xl text-accent font-semibolt>GPUs</span> 上也比经典方法快 <span text-2xl text-accent font-semibold>10倍</span>
</div>
</GlassCard>

---

# 与 MIO 的比较

<GlassCard
  title="与 MIO 的比较"
  variant="warning"
  icon="i-ph-caret-double-right-duotone"
  size="lg"
>

<div  bg-white:20 dark:bg-black:10 rounded-lg border="t l r white/10" text-sm text-on-surface overflow-hidden>
<img src="/figs/vs-mio.png" />
</div>

<div strong text-center mt-4 text-xl equation-block>
参数<span text-2xl text-accent font-semibold>更少</span>但泛化<span text-2xl text-accent font-semibolt>更好</span>
</div>
</GlassCard>

---

# 结论

<!-- <div class="mb-4 text-center">
  <div class="text-xl text-on-surface mb-2">
    <span class="emphasis-primary font-bold">当前局限</span>与研究方向
  </div>
</div> -->

<div grid="~ cols-2 gap-6" mt-4>

<GlassCard
  title="当前局限"
  subtitle="待改进领域"
  variant="error"
  icon="i-ph-warning-duotone"
  size="lg"
  :list-items="[
    '无能量(频率)依赖',
    '稳态解',
    '大量预训练数据',
    '内存限制'
  ]"
/>

<GlassCard
  title="未来方向"
  subtitle="研究机遇"
  variant="success"
  icon="i-ph-rocket-launch-duotone"
  size="lg"
  :list-items="[
    '3D 扩展',
    '时间依赖问题',
    '多物理场耦合',
    '不确定性量化'
  ]"
/>

</div>

<div class="mt-4">
  <GlassCard
    title="广泛影响"
    variant="gradient-secondary"
    icon="i-ph-globe-duotone"
    size="lg"
  >
    <div class="text-center">
      <div class="mb-1">
        <strong>应用：</strong> ICF 设计、医学成像、天体物理
      </div>
      <div>
        <strong>影响：</strong> 实时模拟与优化
      </div>
    </div>
  </GlassCard>
</div>

---
layout: center
class: "text-center pb-5"
---

# 谢谢！

<div class="mt-8 space-y-6">
  <div class="text-xl text-on-surface-variant">
    提问与讨论
  </div>

  <div class="grid grid-cols-3 gap-4 mt-12">
    <GlassCard
      title="论文"
      variant="gradient-primary"
      icon="i-ph-file-text-duotone"
      size="md"
      text-center
    >
      <div class="text-sm">
      DeepRTE: Pre-trained attention-based neural network for radiative transfer, <span class="font-italic text-pink">Comput. Methods Appl. Mech. Eng.</span>, 2026
      </div>
    </GlassCard>
    <GlassCard
      title="代码"
      variant="gradient-secondary"
      icon="i-ph-code-duotone"
      size="md"
      text-center
    >
      <div class="text-sm mt-6">
        GitHub 上可用<br/>
        <Repo name="mazhengcn/deeprte" />
      </div>
    </GlassCard>
    <GlassCard
      title="联系方式"
      variant="tech"
      icon="i-ph-envelope-duotone"
      size="md"
      text-center
    >
      <div class="text-sm mt-6">
        马征<br/>
        上海交通大学
      </div>
    </GlassCard>
  </div>
</div>

<div class="mt-10 text-lg">
  可以访问 <a href="https://zheng-home.netlify.app/talks">https://zheng-home-netlify.app/talks</a> 获取幻灯片
</div>
