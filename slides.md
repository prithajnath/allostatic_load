---
theme: seriph
background: /bg.jpg
title: Quantifying Chronic Stress
info: |
  ## Quantifying Chronic Stress
  A reproducible method for measuring allostatic load with wearable sensors.
  MS Thesis Defense — Prithaj Nath, University of Vermont, 2026.
class: text-center
drawings:
  persist: false
transition: slide-left
comark: true
duration: 38min
fonts:
  sans: "Cormorant Garamond"
  mono: "Space Mono"
  provider: google
---

# Quantifying Chronic Stress

A Reproducible Method for Measuring Allostatic Load with Wearable Sensors

<div class="mt-4 text-sm" style="color: rgba(255,220,180,0.75)">
Prithaj Nath · University of Vermont · MS Defense · June 22, 2026
</div>

<div @click="$slidev.nav.next" class="mt-10 py-1" hover:bg="white op-10">
  Press Space to begin <carbon:arrow-right />
</div>


---

# Index

<div class="grid grid-cols-1 gap-2 text-left max-w-lg mx-auto mt-6">
  <div class="flex items-baseline gap-4"><span class="text-xs opacity-50">01</span><span class="text-2xl tracking-widest">INTRODUCTION</span></div>
  <div class="flex items-baseline gap-4"><span class="text-xs opacity-50">02</span><span class="text-2xl tracking-widest">BACKGROUND</span></div>
  <div class="flex items-baseline gap-4"><span class="text-xs opacity-50">03</span><span class="text-2xl tracking-widest">METHODS</span></div>
  <div class="flex items-baseline gap-4"><span class="text-xs opacity-50">04</span><span class="text-2xl tracking-widest">RESULTS</span></div>
  <div class="flex items-baseline gap-4"><span class="text-xs opacity-50">05</span><span class="text-2xl tracking-widest">DISCUSSION</span></div>
</div>

---
layout: center
class: text-center
---

# 01 — Introduction

---
clicks: 2
---

# About Me

<div class="grid grid-cols-2 gap-10 mt-6 items-center">
  <div class="flex justify-center">
    <div class="relative w-full h-52 flex items-center justify-center">
      <img :src="'/profile_pic.jpeg'" :class="$clicks >= 1 ? 'opacity-0' : 'opacity-100'" class="absolute w-44 h-44 rounded-full object-cover shadow-lg transition-opacity duration-700" />
      <div :class="$clicks >= 1 ? 'opacity-100' : 'opacity-0'" class="absolute inset-0 flex items-center justify-center gap-4 transition-opacity duration-700">
        <video class="h-48 w-36 rounded-xl object-cover shadow-lg" autoplay loop muted playsinline>
          <source :src="'/bike_snow.mp4'" type="video/mp4" />
        </video>
        <video class="h-48 w-36 rounded-xl object-cover shadow-lg" autoplay loop muted playsinline>
          <source :src="'/bike_va.mp4'" type="video/mp4" />
        </video>
      </div>
    </div>
  </div>
  <div class="flex flex-col gap-4 text-sm">
    <div>
      <div class="text-lg font-bold">Prithaj Nath</div>
      <div class="opacity-60 text-xs tracking-widest mt-1">M.S. COMPUTER SCIENCE · UNIVERSITY OF VERMONT</div>
    </div>
    <div class="flex flex-col gap-3">
      <div class="opacity-80">Before grad school, I spent a couple of years as a data engineer at startups in Burlington and New York — building pipelines, wrangling messy data, and learning what it means to ship things under pressure.</div>
      <div :class="$clicks >= 1 ? 'opacity-80' : 'opacity-0'" class="transition-opacity duration-700">I like to ride my bike, no matter the season. I've biked across VT, NY, NJ, PA, WI, IL and MN. Just a couple more states to go. It's a great way to explore new places.</div>
      <div :class="$clicks >= 2 ? 'opacity-80' : 'opacity-0'" class="transition-opacity duration-700">I spent the COVID pandemic in India. I lost someone in my family during that time, and it made health feel suddenly urgent and personal in a way it never had before. I started reading everything I could about longevity, got serious about exercise, and started tracking everything with wearables. That obsession with understanding what's happening inside the body is ultimately what brought me to this project.</div>
    </div>
  </div>
</div>

---
layout: center
class: text-center
---

# 02 — Background

Setting the stage and motivating the research question

---

# What Is Stress, Exactly?

Despite its ubiquity in daily life, stress has no universally agreed-upon scientific definition — and that definitional gap turns out to matter enormously for measurement.

<v-click>

**Hans Selye (1936) — the physiological pole**

Identified the *General Adaptation Syndrome* (GAS): a stereotyped, triphasic physiological response the body mounts against persistent stressors. Selye's insight was that heterogeneous stressors — cold, infection, trauma — could converge on the same downstream health outcomes via shared biological machinery: the HPA axis and the autonomic nervous system.

</v-click>

<v-click>

**Lazarus & Folkman (1984) — the appraisal pole**

Shifted focus from the stressor itself to the individual's *cognitive interpretation* of it. Stress, in this view, is not a physiological event but a relational appraisal: whether the person reads a situation as exceeding their coping resources.

</v-click>

---
clicks: 5
---

# The Stress Response: Two Axes

<div class="flex flex-col items-center mt-1" style="font-size: 0.72em; line-height: 1.4">
  <div :class="$clicks >= 1 ? 'border-yellow-300 bg-yellow-900 text-yellow-100' : 'border-slate-700 bg-slate-800 text-slate-500'" class="border-2 rounded px-8 py-2 font-bold tracking-widest transition-all duration-500">STRESSOR</div>
  <div :class="$clicks >= 2 ? 'text-slate-400' : 'text-slate-800'" class="text-xl leading-none my-1 transition-all duration-500">↓</div>
  <div :class="$clicks >= 2 ? 'border-yellow-400 bg-yellow-950 text-yellow-100' : 'border-slate-700 bg-slate-900 text-slate-600'" class="border-2 rounded px-8 py-2 transition-all duration-500">
    <span class="font-bold tracking-wide">Cognitive Appraisal</span>
    <span class="text-xs opacity-60 ml-3">Lazarus &amp; Folkman</span>
  </div>
  <div :class="$clicks >= 3 ? 'text-slate-400' : 'text-slate-800'" class="text-xl leading-none my-1 transition-all duration-500">↓</div>
  <div class="flex gap-20">
    <div class="flex flex-col items-center gap-1">
      <div :class="$clicks >= 3 ? 'text-blue-300' : 'text-slate-700'" class="font-bold text-xs tracking-widest mb-1 transition-all duration-300">SAM AXIS — fast</div>
      <div :class="$clicks >= 3 ? 'border-blue-600 text-slate-200' : 'border-slate-700 text-slate-700'" class="border rounded px-4 py-1 bg-slate-900 text-xs text-center transition-all duration-300">Hypothalamus</div>
      <div :class="$clicks >= 3 ? 'text-slate-500' : 'text-slate-800'" class="text-center transition-all duration-300">↓</div>
      <div :class="$clicks >= 3 ? 'border-blue-600 text-slate-200' : 'border-slate-700 text-slate-700'" class="border rounded px-4 py-1 bg-slate-900 text-xs text-center transition-all duration-300">Sympathetic NS</div>
      <div :class="$clicks >= 3 ? 'text-slate-500' : 'text-slate-800'" class="text-center transition-all duration-300">↓</div>
      <div :class="$clicks >= 3 ? 'border-blue-600 text-slate-200' : 'border-slate-700 text-slate-700'" class="border rounded px-4 py-1 bg-slate-900 text-xs text-center transition-all duration-300">Adrenal Medulla</div>
      <div :class="$clicks >= 3 ? 'text-slate-500' : 'text-slate-800'" class="text-center transition-all duration-300">↓</div>
      <div :class="$clicks >= 4 ? 'border-blue-400 bg-blue-950 text-blue-200' : 'border-slate-700 bg-slate-900 text-slate-700'" class="border rounded px-4 py-1 text-xs text-center font-bold transition-all duration-500">Epinephrine / Norepinephrine</div>
      <div v-show="$clicks >= 4" class="text-blue-400 text-xs text-center mt-1">↑ HR · ↑ BP · mobilize energy<br/><span class="font-bold">resolves in minutes</span></div>
    </div>
    <div class="flex flex-col items-center gap-1">
      <div :class="$clicks >= 3 ? 'text-orange-300' : 'text-slate-700'" class="font-bold text-xs tracking-widest mb-1 transition-all duration-300">HPA AXIS — slow</div>
      <div :class="$clicks >= 3 ? 'border-orange-600 text-slate-200' : 'border-slate-700 text-slate-700'" class="border rounded px-4 py-1 bg-slate-900 text-xs text-center transition-all duration-300">Hypothalamus</div>
      <div :class="$clicks >= 3 ? 'text-slate-500' : 'text-slate-800'" class="text-center transition-all duration-300">↓</div>
      <div :class="$clicks >= 3 ? 'border-orange-600 text-slate-200' : 'border-slate-700 text-slate-700'" class="border rounded px-4 py-1 bg-slate-900 text-xs text-center transition-all duration-300">Pituitary</div>
      <div :class="$clicks >= 3 ? 'text-slate-500' : 'text-slate-800'" class="text-center transition-all duration-300">↓</div>
      <div :class="$clicks >= 3 ? 'border-orange-600 text-slate-200' : 'border-slate-700 text-slate-700'" class="border rounded px-4 py-1 bg-slate-900 text-xs text-center transition-all duration-300">Adrenal Cortex</div>
      <div :class="$clicks >= 3 ? 'text-slate-500' : 'text-slate-800'" class="text-center transition-all duration-300">↓</div>
      <div :class="$clicks >= 5 ? 'border-orange-400 bg-orange-950 text-orange-200' : 'border-slate-700 bg-slate-900 text-slate-700'" class="border rounded px-4 py-1 text-xs text-center font-bold transition-all duration-500">Cortisol</div>
      <div v-show="$clicks >= 5" class="text-orange-400 text-xs text-center mt-1">sustained dysregulation<br/><span class="font-bold">accumulates as allostatic load</span></div>
    </div>
  </div>
</div>

---
clicks: 3
---

# When Does the HPA Shut Off?

<div class="grid grid-cols-2 gap-10 mt-4" style="font-size: 0.78em">
  <div class="flex flex-col items-center gap-1">
    <div class="text-green-300 font-bold text-xs tracking-widest mb-2">HEALTHY SYSTEM</div>
    <div class="border border-orange-600 rounded px-5 py-1 bg-slate-900 text-slate-300 text-xs text-center">HPA Axis Activates</div>
    <div class="text-slate-500 text-center">↓</div>
    <div class="border border-orange-400 rounded px-5 py-1 bg-orange-950 text-orange-200 text-xs text-center font-bold">Cortisol ↑</div>
    <div v-show="$clicks >= 1" class="flex flex-col items-center gap-1 w-full">
      <div class="text-slate-500 text-center">↓</div>
      <div class="border border-green-600 rounded px-5 py-1 bg-green-950 text-green-200 text-xs text-center">⟲  Negative feedback<br/>Cortisol suppresses HPA</div>
      <div class="text-slate-500 text-center">↓</div>
      <div class="border-2 border-green-400 rounded px-5 py-2 bg-green-950 text-green-100 text-xs text-center font-bold">Response terminates ✓<br/><span class="font-normal opacity-70">system returns to baseline</span></div>
    </div>
  </div>
  <div class="flex flex-col items-center gap-1">
    <div class="text-red-300 font-bold text-xs tracking-widest mb-2">ALLOSTATIC LOAD</div>
    <div class="border border-orange-600 rounded px-5 py-1 bg-slate-900 text-slate-300 text-xs text-center">HPA Axis Activates</div>
    <div class="text-slate-500 text-center">↓</div>
    <div class="border border-orange-400 rounded px-5 py-1 bg-orange-950 text-orange-200 text-xs text-center font-bold">Cortisol ↑</div>
    <div v-show="$clicks >= 2" class="flex flex-col items-center gap-1 w-full">
      <div class="text-slate-500 text-center">↓</div>
      <div class="border border-red-600 rounded px-5 py-1 bg-red-950 text-red-200 text-xs text-center">✗  Feedback fails<br/>HPA won't shut off</div>
      <div class="text-slate-500 text-center">↓</div>
      <div class="border-2 border-red-400 rounded px-5 py-2 bg-red-950 text-red-100 text-xs text-center font-bold">Persistent hyperarousal<br/><span class="font-normal opacity-70">cardiovascular · metabolic · immune wear</span></div>
    </div>
  </div>
</div>
<div v-show="$clicks >= 3" class="mt-4 text-xs text-center opacity-60 italic">This failure to terminate — not mere elevation — is the defining pathology of allostatic load.</div>

---
clicks: 4
---

# The Measurement Problem

<div class="flex flex-col gap-3 mt-1" style="font-size: 0.68em; line-height: 1.3">
  <div class="flex flex-col items-center">
    <div class="border-2 border-yellow-300 bg-yellow-900 text-yellow-100 rounded px-6 py-1 font-bold tracking-widest">STRESSOR</div>
    <div class="text-slate-500 leading-none my-0.5">↓</div>
    <div class="flex items-center gap-3">
      <div class="border-2 border-yellow-400 bg-yellow-950 text-yellow-100 rounded px-6 py-1">
        <span class="font-bold">Cognitive Appraisal</span>
        <span class="opacity-60 ml-2">Lazarus &amp; Folkman</span>
      </div>
      <div v-show="$clicks >= 1" class="border border-yellow-500 rounded px-2 py-0.5 bg-slate-900 text-yellow-300 whitespace-nowrap">← wearables measure here</div>
    </div>
    <div class="text-slate-500 leading-none my-0.5">↓</div>
    <div class="flex gap-16">
      <div class="flex flex-col items-center gap-0.5">
        <div class="text-blue-300 font-bold tracking-widest">SAM AXIS — fast</div>
        <div class="border border-blue-600 rounded px-3 py-0.5 bg-slate-900 text-slate-200 text-center">Hypothalamus</div>
        <div class="text-slate-500 text-center">↓</div>
        <div class="border border-blue-600 rounded px-3 py-0.5 bg-slate-900 text-slate-200 text-center">Sympathetic NS</div>
        <div class="text-slate-500 text-center">↓</div>
        <div class="border border-blue-600 rounded px-3 py-0.5 bg-slate-900 text-slate-200 text-center">Adrenal Medulla</div>
        <div class="text-slate-500 text-center">↓</div>
        <div class="border border-blue-400 bg-blue-950 text-blue-200 rounded px-3 py-0.5 text-center font-bold">Epinephrine / Norepinephrine</div>
        <div class="text-blue-400 text-center">resolves in minutes</div>
      </div>
      <div class="flex flex-col items-center gap-0.5">
        <div class="text-orange-300 font-bold tracking-widest">HPA AXIS — slow</div>
        <div class="border border-orange-600 rounded px-3 py-0.5 bg-slate-900 text-slate-200 text-center">Hypothalamus</div>
        <div class="text-slate-500 text-center">↓</div>
        <div class="border border-orange-600 rounded px-3 py-0.5 bg-slate-900 text-slate-200 text-center">Pituitary</div>
        <div class="text-slate-500 text-center">↓</div>
        <div class="border border-orange-600 rounded px-3 py-0.5 bg-slate-900 text-slate-200 text-center">Adrenal Cortex</div>
        <div class="text-slate-500 text-center">↓</div>
        <div class="border border-orange-400 bg-orange-950 text-orange-200 rounded px-3 py-0.5 text-center font-bold">Cortisol</div>
        <div class="text-orange-400 text-center">accumulates as allostatic load</div>
      </div>
    </div>
  </div>
  <div class="grid grid-cols-2 gap-5">
    <div v-show="$clicks >= 2" class="border border-yellow-700 rounded-lg p-3 bg-yellow-950 bg-opacity-30">
      <div class="text-yellow-400 font-bold tracking-widest mb-1">WHERE WEARABLE RESEARCH LIVES</div>
      <div>Detects <strong>acute autonomic arousal</strong> at the appraisal phase. The signal is real but <strong>state-level</strong> — transient, situation-bound, resolving in minutes.</div>
      <div class="mt-2 opacity-50 italic">WESAD · Trier Social Stress Test · ML stress classifiers</div>
    </div>
    <div v-show="$clicks >= 3" class="border border-orange-600 rounded-lg p-3 bg-orange-950 bg-opacity-30">
      <div class="text-orange-400 font-bold tracking-widest mb-1">WHERE THE MORTALITY SIGNAL LIVES</div>
      <div>Allostatic load lives <strong>downstream of appraisal entirely</strong> — in the slow HPA axis. It is <strong>trait-level</strong>: cortisol dysregulation accumulated over months and years.</div>
      <div class="mt-2 opacity-50 italic">predicts 7-year mortality · cognitive decline · depression · anhedonia</div>
    </div>
  </div>
  <div v-show="$clicks >= 4" class="text-center italic opacity-70 border-t border-slate-700 pt-2">The field has built increasingly sophisticated tools to measure the wrong thing. <strong>No wearable study has yet targeted allostatic load directly.</strong></div>
</div>

---

# Allostatic Load — The Construct

The body maintains stability not by holding parameters fixed, but by adjusting them to anticipated demand — a process McEwen and Stellar (1993) termed **allostasis**.

<v-click>

The machinery is the HPA axis and the autonomic nervous system. In the acute case this response is **adaptive and self-limiting**: it mobilizes resources, then shuts off.

**Allostatic load is what accumulates when it does not.**

Under chronic or repeated activation — or when the response fails to terminate once a threat has passed — the primary mediators overstimulate the secondary systems they regulate. The cumulative "wear and tear" propagates outward into cardiovascular, metabolic, and immune dysregulation.

</v-click>

<v-click>

Two features of the construct that matter for everything that follows:

| | |
|---|---|
| **Trait-like** | It is the integral of stress exposure over months and years, not a momentary state. Its predictive value lies in that stability. |
| **Dynamical** | The defining pathology is an *inability to terminate the stress response* — not the mere elevation of any single marker. |

</v-click>

---
layout: center
class: text-center
---

# The Research Question

<div class="mt-8 text-2xl leading-relaxed max-w-2xl mx-auto">
Can we recover allostatic load — a <em>trait-level</em>, cumulative construct — from a consumer-grade wearable device alone?
</div>

<v-click>

<div class="mt-8 text-sm opacity-60 max-w-xl mx-auto">Allostatic load has been accessible only through invasive clinical bloodwork. The wearable stress literature has aimed entirely at the appraisal phase. Nobody has tried to connect the two.</div>

</v-click>

---

# The MacArthur Approach

Seeman et al. made AL empirically tractable with a **summed-quartile composite**: score each participant in the high-risk quartile across ~10 biomarkers spanning neuroendocrine, cardiovascular, and metabolic systems, then sum.

<v-click>

This worked. The composite predicted 7-year mortality, cognitive decline, and physical functional decline in older adults — and the summation captured something real about cumulative biological burden that no individual marker did.

</v-click>

<v-click>

**But the scalar composite collapses a critical dimension.** By summing equally across systems it treats a participant whose load is concentrated in the autonomic axis and one whose load is concentrated in the metabolic axis as *equivalent* whenever their totals coincide. The composite tells you *how much* dysregulation, not *which systems*.

</v-click>

---

# Carbone's Latent Class Analysis

Carbone addressed the cross-system limitation directly: instead of summing across systems, apply **latent class analysis** to recover the structure the scalar score cannot represent.

<v-click>

Applied to a national community sample, LCA identified two clinically meaningful subpopulations:

<div class="grid grid-cols-2 gap-6 mt-3 text-sm">
<div class="border border-purple-700 rounded p-3 bg-purple-950 bg-opacity-30">
<div class="text-purple-300 font-bold tracking-widest text-xs mb-2">PARASYMPATHETIC DYSREGULATION</div>

Autonomic and sleep-regulatory axis. Emerged as a principal carrier of **depression and anhedonia** signal.

</div>
<div class="border border-slate-600 rounded p-3">
<div class="text-slate-400 font-bold tracking-widest text-xs mb-2">IMMUNOMETABOLIC DYSREGULATION</div>

Metabolic and inflammatory axis. Differentially tracked different downstream outcomes.

</div>
</div>

</v-click>

<v-click>

**Why this matters for us:** the parasympathetic class — the axis a wearable can directly access through nocturnal HRV and sleep architecture — is one of the *principal loci of mental-health signal* in the broader AL construct. A wearable measuring the autonomic facet is not measuring a degraded proxy; it is measuring a coherent and clinically meaningful sub-construct.

</v-click>

<v-click>

**But Carbone's enrichment is still cross-sectional.** It partitions people by the *shape of dysregulation across systems* at a single point in time — not across time.

</v-click>

---

# The Temporal Axis: What Neither Can See

AL theory defines the construct by two properties — *accumulation* and *failure to shut off* — both of which are properties of a **trajectory**, not a snapshot. A single cross-sectional blood draw registers the present level of dysregulation, but it cannot observe how long a person has been dysregulated, whether they recover between stressors, or whether the stress response ever terminates at all. A measurement made at one timepoint is structurally unable to capture the temporal features the construct is defined by.

<v-click>

<div class="mt-4 border-l-4 border-amber-500 pl-5 py-2 bg-amber-950 bg-opacity-20 rounded-r">
<div class="text-amber-200 text-base italic leading-relaxed">"The majority of studies, to date, are cross-sectional. More longitudinal research is therefore necessary, examining AL for different subpopulations and cohorts as they evolve across time/space."</div>
<div class="mt-3 text-xs opacity-60">Buckwalter et al. (2016), <em>Complexity</em></div>
</div>

</v-click>

<v-click>

<div class="mt-3 text-sm border border-slate-700 rounded p-3 bg-slate-900">
This call comes from a paper co-authored by <strong>Teresa Seeman</strong> — who developed the MacArthur summed-quartile composite — and <strong>Bruce McEwen</strong> — who coined allostatic load in 1993. The original architects of the field are asking for exactly what LEMURS provides.
</div>

</v-click>

<v-click>

Carbone's cross-system axis and this **temporal axis** are orthogonal enrichments. Each recovers information the other cannot. **LEMURS** — 605 students, Oura rings, 8 weeks of nightly data — is the dataset that makes the temporal axis tractable for the first time.

</v-click>

---
layout: center
class: text-center
---

# 03 — Methods

LEMURS · Six Features · AL_z · Hierarchical Bayesian HMM

---

# LEMURS Dataset

**Lived Experiences Measured Using Rings Study** — University of Vermont

<div class="grid grid-cols-2 gap-6 mt-4">
<div>

**Participants & data**
- N = 605 college students
- Gen3 Oura rings worn nightly during sleep
- 8-week window: October – December 2022
- 30,716 nights total (median 55 per participant)

</div>
<div>

**Validation instruments**
- Weekly PSS (Perceived Stress Scale)
- Weekly GAD-7 (Generalized Anxiety Disorder)
- Baseline mental health diagnosis survey
- Clinical bloodwork: cardiovascular, metabolic, lipid, inflammatory panels

</div>
</div>

<v-click>

> The longitudinal structure + concurrent psychometrics + clinical bloodwork together supply exactly the validation criteria a wearable-derived AL measure requires.

</v-click>

---

# Six Sleep Features

Daytime measurement is confounded by the SAM axis reacting to movement, posture, and caffeine on a timescale of seconds. Sleep removes this noise — the slower HPA axis leaves a persistent imprint on resting autonomic tone, and chronic stress alters that imprint in characteristic, measurable ways.

<div class="grid grid-cols-2 gap-4 mt-3 text-sm">
<div>

**1. Nightly HRV (RMSSD)**
Gold-standard non-invasive proxy for vagal tone. Depressed nocturnal HRV → parasympathetic withdrawal.

**2. Deep Sleep Duration (SWS)**
HPA-axis inhibition and cortisol clearance happen here. Absolute duration, not percentage — restorative dose depends on total exposure.

**3. REM Sleep Duration**
Chronic stress fragments REM and reduces density. Absolute duration for the same reason.

</div>
<div>

**4. Sleep Latency**
Prolonged onset → inability to transition from sympathetic dominance to parasympathetic rest.

**5. Number of Awakenings**
Frequent nocturnal awakenings → transient sympathetic spikes, hypervigilant nervous system.

**6. Recovery Index**
Time to reach lowest resting HR during the night. Delayed → body struggling to clear daytime stress hormones.

</div>
</div>

<v-click>

> Nocturnal physiology carries a signal of *sustained* stress exposure that daytime acute-arousal measurement is poorly positioned to recover.

</v-click>

---

# Model 1: Magnitude — AL_z

A direct analog of the MacArthur summed-quartile score, replacing quartile dichotomization with a continuous z-score.

<v-click>

**Grand z-scoring** against the cohort distribution (not within-person — between-person variance is what we want to capture):

$$z_{i,t}^{(k)} = \frac{x_{i,t}^{(k)} - \mu^{(k)}}{\sigma^{(k)}}$$

Each biomarker oriented so higher = more dysregulated (HRV, SWS, REM are negated).

</v-click>

<v-click>

**Nightly composite** = unweighted average across 6 biomarkers:

$$\text{AL}_z(i,t) = \frac{1}{6}\sum_{k=1}^{6} z_{i,t}^{(k)}$$

**Participant-level score** = within-person mean across the study window.

</v-click>

---

# Model 2: Shape — Hierarchical Bayesian HMM

Recovers dynamical structure that AL_z averages over.

<v-click>

Each participant's nightly trajectory modeled as emissions from a **two-state HMM**:
- State 1: regulated
- State 2: dysregulated

Emission distributions: $\mathbf{x}_{i,t} \mid S_{i,t} = s \sim \mathcal{N}(\mu_s^{(i)}, \Sigma_s)$

State-specific means **partially pooled** across participants — borrow strength from cohort while preserving person-specific deviations.

</v-click>

<v-click>

From the fitted model, two participant-level shape statistics:

| Statistic | Definition | Captures |
| --- | --- | --- |
| **AL_dwell** | Expected consecutive nights in dysregulated state: $1/(1-A_{22}^{(i)})$ | *Stability* of dysregulation |
| **AL_vuln** | Probability of transitioning regulated → dysregulated: $A_{12}^{(i)}$ | *Vulnerability* to dysregulation |

</v-click>

---

# Validation Framework

**Two orthogonal frameworks** — neither alone is sufficient:

<div class="grid grid-cols-2 gap-6 mt-4 text-sm">
<div>

**Psychometric validation**

- Trait-like stability: ICC > 0.5 over 8-week window
- Association with known correlates: prior trauma, mental health diagnoses, chronic anxiety
- Prediction: shape measures (AL_dwell, AL_vuln) should carry trait-like mental-health signal

</div>
<div>

**Clinical validation**

- Correspondence with canonical MacArthur clinical biomarker composite from LEMURS bloodwork
- Expectation is *partial*: wearable indexes autonomic axis, not metabolic/inflammatory axis
- Strong correlation with metabolic markers would *falsify* the autonomic-axis framing

</div>
</div>

**Differential validation hypothesis:** AL_z should track clinical biomarker magnitude; AL_dwell and AL_vuln should track trait-like mental health indicators. A double dissociation would establish the two measures are non-redundant.

---
layout: center
class: text-center
---

# 04 — Results

Complementary measures · Trait stability · Psychometric · Clinical

---

# Operationalization: Two Complementary Facets

<div class="grid grid-cols-2 gap-8 mt-4 items-center">
<div>

The HMM shape measures and AL_z capture largely non-overlapping information:

- AL_dwell vs AL_z: **r = 0.26** (cycling subgroup)
- AL_vuln vs AL_z: **r = 0.24**

AL_z asks *how far* a participant deviates from baseline; AL_vuln and AL_dwell ask *how* that deviation is distributed in time. A participant who is chronically dysregulated and one who is intermittently so can share an identical mean AL_z.

<v-click>

> Two measures are not redundant. They merit separate and combined validation.

</v-click>

</div>
<div class="flex items-center justify-center">
<img :src="'/alz_alhmm_corr.png'" class="max-h-72 rounded shadow-lg" />
</div>
</div>

---

# Trait-like Stability of AL_z

<div class="grid grid-cols-2 gap-8 mt-4">
<div>

**Single-night reliability:**
$$\text{ICC}(1,1) = 0.431 \quad [0.399, 0.462]$$

Between-person variance accounts for 43% of total variance in nightly AL_z.

A single night is not a trait — but the participant-level mean is.

</div>
<div v-click>

**k-night reliability (Spearman–Brown):**

At the cohort median of 55 nights:
$$\text{ICC}(1, 55) = 0.977$$

The trait-like threshold (> 0.5) is exceeded for any participant with at least 2 nights — holds for **99.8%** of the cohort.

</div>
</div>

<v-click>

> The participant-level AL_z score behaves as a trait, with median reliability 0.977, even though any single night does not.

</v-click>

---

# HMM State Sequences

<img :src="'/al_hmm_heatmap.png'" class="w-full rounded mt-1" style="max-height: 290px; object-fit: contain;" />

<div class="grid grid-cols-2 gap-6 mt-3 text-sm">
<div>

**Long yellow streaks** — participants stuck in the dysregulated state for weeks. Captured by high **AL_dwell** (stable dysregulation).

</div>
<div>

**Fine alternating striping** — rapid regulated↔dysregulated transitions with low dwell time. Captured by high **AL_vuln** (labile dysregulation).

</div>
</div>


---
clicks: 3
---

# Psychometric Validation

<div class="text-xs opacity-50 mb-2">Logistic regression · controlling for age, BMI, sex · odds ratios for self-reported mental health diagnoses</div>
<table class="w-full text-xs border-collapse">
  <thead>
    <tr class="border-b border-slate-600 text-slate-400">
      <th class="text-left py-1 pr-4 font-normal">Predictor</th>
      <th class="text-left py-1 pr-4 font-normal">Outcome</th>
      <th class="text-center py-1 pr-4 font-normal">OR (95% CI)</th>
      <th class="text-center py-1 pr-4 font-normal">p</th>
      <th class="text-center py-1 font-normal">p<sub>BH</sub></th>
    </tr>
  </thead>
  <tbody>
    <tr :class="$clicks === 0 ? 'opacity-40' : $clicks === 1 ? 'opacity-90' : 'opacity-15'" class="border-b border-slate-800 transition-all duration-500">
      <td class="py-1 pr-4">AL<sub>z</sub></td>
      <td class="py-1 pr-4">Anxiety</td>
      <td class="text-center py-1 pr-4">1.29 (1.06–1.58)</td>
      <td class="text-center py-1 pr-4">0.013</td>
      <td class="text-center py-1">0.186</td>
    </tr>
    <tr :class="$clicks < 2 ? ($clicks === 0 ? 'opacity-40' : 'opacity-90') : 'bg-orange-950 border-orange-700'" class="border-b transition-all duration-500">
      <td class="py-1 pr-4" :class="$clicks >= 2 ? 'font-bold text-orange-200' : ''">AL<sub>z</sub></td>
      <td class="py-1 pr-4" :class="$clicks >= 2 ? 'font-bold text-orange-200' : ''">Depression</td>
      <td class="text-center py-1 pr-4" :class="$clicks >= 2 ? 'font-bold text-orange-200' : ''">1.50 (1.20–1.86)</td>
      <td class="text-center py-1 pr-4" :class="$clicks >= 2 ? 'font-bold text-orange-200' : ''">&lt;0.001</td>
      <td class="text-center py-1" :class="$clicks >= 2 ? 'font-bold text-orange-200' : ''">0.018 ✓</td>
    </tr>
    <tr :class="$clicks === 0 ? 'opacity-40' : $clicks === 1 ? 'opacity-90' : 'opacity-15'" class="border-b border-slate-800 transition-all duration-500">
      <td class="py-1 pr-4">AL<sub>vuln</sub></td>
      <td class="py-1 pr-4">Depression</td>
      <td class="text-center py-1 pr-4">1.37 (1.13–1.67)</td>
      <td class="text-center py-1 pr-4">0.002</td>
      <td class="text-center py-1">0.095</td>
    </tr>
    <tr :class="$clicks === 0 ? 'opacity-40' : $clicks === 1 ? 'opacity-90' : 'opacity-15'" class="border-b border-slate-800 transition-all duration-500">
      <td class="py-1 pr-4">AL<sub>vuln</sub></td>
      <td class="py-1 pr-4">ADHD</td>
      <td class="text-center py-1 pr-4">1.31 (1.00–1.72)</td>
      <td class="text-center py-1 pr-4">0.049</td>
      <td class="text-center py-1">0.612</td>
    </tr>
    <tr :class="$clicks === 0 ? 'opacity-40' : $clicks === 1 ? 'opacity-90' : 'opacity-15'" class="border-b border-slate-800 transition-all duration-500">
      <td class="py-1 pr-4">AL<sub>dwell</sub><sup>finite</sup></td>
      <td class="py-1 pr-4">Anxiety</td>
      <td class="text-center py-1 pr-4">1.33 (1.08–1.64)</td>
      <td class="text-center py-1 pr-4">0.006</td>
      <td class="text-center py-1">0.238</td>
    </tr>
    <tr :class="$clicks === 0 ? 'opacity-40' : $clicks === 1 ? 'opacity-90' : 'opacity-15'" class="border-b border-slate-800 transition-all duration-500">
      <td class="py-1 pr-4">AL<sub>dwell</sub><sup>finite</sup></td>
      <td class="py-1 pr-4">Depression</td>
      <td class="text-center py-1 pr-4">1.33 (1.08–1.64)</td>
      <td class="text-center py-1 pr-4">0.008</td>
      <td class="text-center py-1">0.238</td>
    </tr>
    <tr :class="$clicks === 0 ? 'opacity-40' : $clicks === 1 ? 'opacity-90' : 'opacity-15'" class="border-b border-slate-800 transition-all duration-500">
      <td class="py-1 pr-4">AL<sub>dwell</sub><sup>always</sup> × AL<sub>z</sub></td>
      <td class="py-1 pr-4">Anxiety</td>
      <td class="text-center py-1 pr-4">2.26 (1.09–4.66)</td>
      <td class="text-center py-1 pr-4">0.028</td>
      <td class="text-center py-1">0.319</td>
    </tr>
    <tr :class="$clicks === 0 ? 'opacity-40' : $clicks === 1 ? 'opacity-90' : 'opacity-15'" class="border-b border-slate-800 transition-all duration-500">
      <td class="py-1 pr-4">AL<sub>dwell</sub><sup>finite</sup> × AL<sub>z</sub></td>
      <td class="py-1 pr-4">Emotional disorder</td>
      <td class="text-center py-1 pr-4">0.24 (0.07–0.86)</td>
      <td class="text-center py-1 pr-4">0.028</td>
      <td class="text-center py-1">0.873</td>
    </tr>
  </tbody>
</table>
<div v-show="$clicks >= 3" class="mt-3 text-xs border-l-2 border-orange-600 pl-3 opacity-80">Only AL<sub>z</sub> → Depression survived Benjamini–Hochberg correction. The magnitude measure carries the most robust psychometric signal.</div>

---
clicks: 7
---

# Clinical Validation — Across Systems

<div class="grid grid-cols-3 gap-3 mt-3" style="font-size: 0.72em">
  <div :class="$clicks < 1 ? 'opacity-25 border-slate-700' : 'border-orange-600 bg-orange-950 bg-opacity-30 opacity-100'" class="border rounded-lg p-3 transition-all duration-500">
    <div :class="$clicks >= 1 ? 'text-orange-300' : 'text-slate-600'" class="font-bold tracking-widest text-xs mb-2 transition-all duration-500">CARDIOVASCULAR</div>
    <div v-show="$clicks >= 1" class="text-slate-200 space-y-1">
      <div>AL<sub>dwell</sub><sup>finite</sup> → Diastolic BP &nbsp;<span class="text-orange-300 font-bold">p=0.015</span></div>
      <div>AL<sub>vuln</sub> → Systolic BP &nbsp;<span class="text-orange-300 font-bold">p=0.003</span></div>
    </div>
  </div>
  <div :class="$clicks < 2 ? 'opacity-25 border-slate-700' : 'border-amber-400 bg-amber-950 bg-opacity-30 opacity-100'" class="border rounded-lg p-3 transition-all duration-500">
    <div :class="$clicks >= 2 ? 'text-amber-300' : 'text-slate-600'" class="font-bold tracking-widest text-xs mb-2 transition-all duration-500">RENAL</div>
    <div v-show="$clicks >= 2" class="text-slate-200">
      <div>AL<sub>z</sub> → BUN &nbsp;<span class="text-amber-300 font-bold">p=0.002</span></div>
      <div class="text-amber-400 text-xs mt-1">⭐ survives BH correction</div>
    </div>
  </div>
  <div :class="$clicks < 3 ? 'opacity-25 border-slate-700' : 'border-orange-600 bg-orange-950 bg-opacity-30 opacity-100'" class="border rounded-lg p-3 transition-all duration-500">
    <div :class="$clicks >= 3 ? 'text-orange-300' : 'text-slate-600'" class="font-bold tracking-widest text-xs mb-2 transition-all duration-500">LIVER</div>
    <div v-show="$clicks >= 3" class="text-slate-200 space-y-1">
      <div>AL<sub>z</sub> → Albumin &nbsp;<span class="text-orange-300 font-bold">p=0.017</span></div>
      <div>AL<sub>z</sub> → GGT<sub>z</sub> &nbsp;<span class="text-orange-300 font-bold">p=0.026</span></div>
    </div>
  </div>
  <div :class="$clicks < 4 ? 'opacity-25 border-slate-700' : 'opacity-80 border-slate-500'" class="border rounded-lg p-3 transition-all duration-500">
    <div class="font-bold tracking-widest text-xs mb-2">HEMATOLOGY</div>
    <div v-show="$clicks >= 4" class="italic text-xs">no significant associations</div>
  </div>
  <div :class="$clicks < 5 ? 'opacity-25 border-slate-700' : 'opacity-80 border-slate-500'" class="border rounded-lg p-3 transition-all duration-500">
    <div class="font-bold tracking-widest text-xs mb-2">IMMUNE</div>
    <div v-show="$clicks >= 5" class="italic text-xs">no significant associations</div>
  </div>
  <div :class="$clicks < 6 ? 'opacity-25 border-slate-700' : 'opacity-80 border-slate-500'" class="border rounded-lg p-3 transition-all duration-500">
    <div class="font-bold tracking-widest text-xs mb-2">LIPIDS</div>
    <div v-show="$clicks >= 6" class="italic text-xs">no significant associations</div>
  </div>
</div>
<div v-show="$clicks >= 7" class="mt-4 text-xs border-l-2 border-amber-500 pl-3 opacity-85">AL<sub>z</sub> is the only predictor with consistent clinical signal — and the only one to survive BH correction (Renal: BUN). Shape metrics showed raw associations in cardiovascular and renal systems; <strong>none survived correction</strong>.</div>

---

# Cardiovascular Signal — An Interaction Effect

The cardiovascular signal in this data doesn't come from any single predictor. It comes from their combination.

<v-click>

<div class="grid grid-cols-2 gap-8 mt-3 items-start">
<div>

**AL_dwell^always × AL_z** — participants who *never recovered* from dysregulation during the study window AND have high allostatic load magnitude show amplified cardiovascular risk across four outcomes simultaneously:

<table class="w-full text-xs border-collapse mt-3">
  <thead>
    <tr class="border-b border-slate-600 text-slate-400">
      <th class="text-left py-0.5 font-normal">Outcome</th>
      <th class="text-center py-0.5 font-normal">β / OR</th>
      <th class="text-center py-0.5 font-normal">p</th>
    </tr>
  </thead>
  <tbody>
    <tr class="border-b border-slate-800">
      <td class="py-0.5 text-slate-300">Diastolic BP (mmHg)</td>
      <td class="text-center py-0.5">2.54</td>
      <td class="text-center py-0.5 text-orange-300">0.029</td>
    </tr>
    <tr class="border-b border-slate-800">
      <td class="py-0.5 text-slate-300">Systolic BP (mmHg)</td>
      <td class="text-center py-0.5">3.98</td>
      <td class="text-center py-0.5 text-orange-300">0.034</td>
    </tr>
    <tr class="border-b border-slate-800">
      <td class="py-0.5 text-slate-300">Hypertension</td>
      <td class="text-center py-0.5">OR 2.48</td>
      <td class="text-center py-0.5 text-orange-300">0.012</td>
    </tr>
    <tr class="border-b border-slate-800">
      <td class="py-0.5 text-slate-300">Hypertension event count</td>
      <td class="text-center py-0.5">0.24</td>
      <td class="text-center py-0.5 text-orange-300">0.011</td>
    </tr>
  </tbody>
</table>

</div>
<div class="flex flex-col gap-4 text-sm">

<v-click>

**The biological story.** High allostatic load alone doesn't hit cardiovascular markers here. Chronic non-recovery alone doesn't either. It's the combination — sustained autonomic dysregulation at high magnitude — that places chronic demand on the cardiovascular system. This is exactly the failure-to-shut-off pathology allostatic load theory predicts.

</v-click>

<v-click>

**The caveat.** None of these interaction terms survived Benjamini–Hochberg correction. The pattern across four cardiovascular outcomes in one system is striking, but at this sample size the coefficients are unstable. This is a hypothesis to test in larger cohorts — not a confirmed finding.

</v-click>

</div>
</div>

</v-click>

---
clicks: 2
---

# Clinical Validation — Results

<div class="text-xs opacity-50 mb-0.5">Main effects · OLS (β) except Hypertension (OR) · controlling for age, sex, BMI · significant results only (p &lt; 0.05 raw)</div>
<table class="w-full text-xs border-collapse" style="line-height: 1.25">
  <thead>
    <tr class="border-b border-slate-600">
      <th class="text-left py-0.5 pr-3 font-normal text-slate-400 w-1/4">Outcome</th>
      <th class="text-center py-0.5 pr-3 font-normal text-orange-300">AL<sub>z</sub></th>
      <th :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 font-normal text-slate-400 transition-all duration-500">AL<sub>dwell</sub><sup>finite</sup></th>
      <th :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 font-normal text-slate-400 transition-all duration-500">AL<sub>dwell</sub><sup>always</sup></th>
      <th :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 font-normal text-slate-400 transition-all duration-500">AL<sub>vuln</sub></th>
    </tr>
  </thead>
  <tbody>
    <tr class="border-b border-slate-800 bg-slate-800 bg-opacity-30">
      <td class="py-px pr-3 text-slate-400 italic" colspan="5">Cardiovascular</td>
    </tr>
    <tr class="border-b border-slate-800">
      <td class="py-0.5 pr-3 text-slate-300">Diastolic BP</td>
      <td class="text-center py-0.5 pr-3 text-slate-600">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-200 transition-all duration-500">0.96 <span class="text-orange-400">p=0.015</span></td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-600 transition-all duration-500">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 text-slate-600 transition-all duration-500">—</td>
    </tr>
    <tr class="border-b border-slate-800">
      <td class="py-0.5 pr-3 text-slate-300">Systolic BP</td>
      <td class="text-center py-0.5 pr-3 text-slate-600">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-600 transition-all duration-500">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-600 transition-all duration-500">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 text-slate-200 transition-all duration-500">−1.74 <span class="text-orange-400">p=0.003</span></td>
    </tr>
    <tr class="border-b border-slate-800 bg-slate-800 bg-opacity-30">
      <td class="py-px pr-3 text-slate-400 italic" colspan="5">Renal</td>
    </tr>
    <tr class="border-b border-slate-800 bg-amber-950 bg-opacity-20">
      <td class="py-0.5 pr-3 text-slate-300">BUN (mg/dL)</td>
      <td class="text-center py-0.5 pr-3 font-bold text-amber-200">−0.50 <span class="text-amber-300">p=0.002 ‡</span></td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-600 transition-all duration-500">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-600 transition-all duration-500">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 text-slate-600 transition-all duration-500">—</td>
    </tr>
    <tr class="border-b border-slate-800 bg-slate-800 bg-opacity-30">
      <td class="py-px pr-3 text-slate-400 italic" colspan="5">Liver</td>
    </tr>
    <tr class="border-b border-slate-800">
      <td class="py-0.5 pr-3 text-slate-300">Albumin (g/dL)</td>
      <td class="text-center py-0.5 pr-3 text-orange-200">−0.03 <span class="text-orange-400">p=0.017</span></td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-600 transition-all duration-500">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-600 transition-all duration-500">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 text-slate-200 transition-all duration-500">−0.03 <span class="text-orange-400">p=0.029</span></td>
    </tr>
    <tr class="border-b border-slate-800">
      <td class="py-0.5 pr-3 text-slate-300">GGT<sub>z</sub> (norm.)</td>
      <td class="text-center py-0.5 pr-3 text-orange-200">0.03 <span class="text-orange-400">p=0.026</span></td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-600 transition-all duration-500">—</td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 pr-3 text-slate-200 transition-all duration-500">−0.07 <span class="text-orange-400">p=0.036</span></td>
      <td :class="$clicks >= 1 ? 'opacity-20' : ''" class="text-center py-0.5 text-slate-600 transition-all duration-500">—</td>
    </tr>
    <tr class="border-b border-slate-800 opacity-40">
      <td class="py-px pr-3 text-slate-500 italic" colspan="5">Hematology · Immune · Lipids — no significant associations</td>
    </tr>
  </tbody>
</table>
<div v-show="$clicks >= 2" class="mt-1 text-xs border-l-2 border-slate-600 pl-3 opacity-60">‡ Only BH-corrected result across all clinical outcomes. No shape metrics survived Benjamini–Hochberg correction within their predictor family.</div>

---
layout: center
class: text-center
---

# 05 — Discussion & Future Work

What we showed · Scope · Threats · What's next

---

# Conclusions — The MacArthur Composite

No wearable measure was significantly associated with the MacArthur-style clinical composite constructed from the LEMURS bloodwork. The only reliable predictor across all models was BMI.

<v-click>

This null result was **anticipated and pre-specified**, not a post-hoc rationalization. The LEMURS bloodwork composite is built from secondary cardiometabolic outcomes — blood pressure, lipids, glucose — and omits the neuroendocrine and sympathetic primary mediators (cortisol, DHEA-S, catecholamines) closest to the autonomic axis the wearable indexes. A measure of parasympathetic sleep dynamics would not be expected to recover a composite that does not contain its nearest biomarker analogues.

</v-click>

---

# Conclusions — Magnitude

**AL_z is the most robust measure to emerge from this work.** A simple unweighted average of six z-scored sleep biomarkers — derivable from a consumer ring worn during sleep — survived Benjamini–Hochberg correction in its association with depression, and showed consistent signal in renal and liver clinical markers.

<v-click>

**What this means for the construct — and why Carbone predicted it.** Carbone (2021) applied latent class analysis to a national sample and identified four classes of biological dysregulation. The **parasympathetic class** — defined by elevated RMSSD, HFHRV, and LFHRV, precisely the signals a wearable captures during sleep — was associated with **71% greater odds** of meeting CES-D depression criteria (ARR=1.71, 95% CI: 1.04–2.82). The SAM pathway class showed no such association. Critically, Carbone's cumulative multisystem AL score was *not* significantly associated with depression treatment (p=0.50). Our autonomic-only AL_z is. Isolating the parasympathetic facet doesn't degrade the signal — for mental health outcomes, it may sharpen it.

</v-click>

<v-click>

**What this means for practice.** The MacArthur operationalization requires an invasive clinical panel. AL_z requires a consumer ring worn during sleep. That a measure this accessible and this simple can predict depression outcomes — one of the leading causes of disability in college students — opens a path toward scalable, continuous, non-invasive risk stratification in populations where clinical bloodwork is impractical.

</v-click>

---

# Conclusions — Shape

The HMM-derived shape measures — **AL_dwell** (how long a person stays in a dysregulated state) and **AL_vuln** (how readily they enter one) — capture a facet of allostatic load that AL_z cannot: the temporal topology of dysregulation.

<v-click>

**What the data showed.** AL_dwell^finite was associated with elevated diastolic blood pressure (β=0.96, p=0.015) and AL_vuln with systolic blood pressure (β=−1.74, p=0.003). These are directionally consistent with the known autonomic → cardiovascular pathway: sustained or recurrent parasympathetic withdrawal places chronic demand on the cardiovascular system, driving upward pressure on resting blood pressure. The biological story is coherent.

</v-click>

<v-click>

**The limitation.** Neither association survived Benjamini–Hochberg correction within the shape predictor family. The signal is present but not robust enough — in this sample, at this sample size — to be declared confirmatory. These results should be treated as hypothesis-generating rather than conclusive.

</v-click>

<v-click>

**What is needed.** Larger cohorts, longer observation windows, and ideally populations with greater cardiovascular risk burden — older adults, clinical populations — where the autonomic → cardiovascular pathway has more room to express itself. The shape measures are theoretically well-motivated; the evidence base simply needs to grow.

</v-click>

---

# Inconclusive Clinical Findings

The clinical panel produced signals in renal and hepatic systems. None are confirmatory — each fails one of the two admissibility conditions required for construct-valid evidence: correct direction, and survival of multiple-comparison correction.

<v-click>

**BUN — survived correction, wrong direction.** AL_z → BUN (β=−0.50, p=0.002) is the only clinical association to survive Benjamini–Hochberg correction. But the sign is opposite to prediction: higher allostatic load is associated with *lower* BUN. An autonomic-axis measure should not recover this marker at all — BUN is governed primarily by dietary protein intake, hepatic urea synthesis, and hydration status, inputs orthogonal to autonomic regulation. Low protein intake, chronic alcohol use, and overhydration all depress BUN, producing exactly this negative sign. Because the protocol recorded neither dietary intake, alcohol use, nor hydration at the time of the blood draw, we cannot distinguish a genuine inverse relationship from confounding by these non-autonomic factors. We treat the BUN association as robust in the data but uninformative for construct validation.

</v-click>

<v-click>

**GGT and Albumin — raw signals, did not survive correction.** AL_z showed raw associations with GGT_z (p=0.026) and albumin (p=0.017), both consistent with chronic systemic inflammation suppressing hepatic synthetic function. Neither survived multiple-testing correction. GGT carries an additional interpretive problem: it can be elevated gradually by chronic liver disease but also acutely — within hours — by binge alcohol use. A single cross-sectional blood draw cannot separate the chronic pathway relevant to allostatic load from the acute one.

</v-click>

---

# Scope and Threats to Validity

**Bounded claim — autonomic facet, not full construct.** A wearable cannot access neuroendocrine or metabolic components of the MacArthur panel. That absence is a boundary, not a failure.

<v-click>

**Threats to validity:**

- *Temporal scope*: 8-week window may not capture the full accumulation timescale of allostatic load, which can span years.
- *Population*: College students are a specific demographic — young, relatively healthy, academic stressors dominant. Generalizability to older or clinical populations requires further study.
- *Proprietary sleep staging*: REM and slow-wave sleep durations are derived from the Oura ring's internal classification models, which are proprietary and subject to unannounced firmware updates. These features are not clinical polysomnography. Any pipeline that includes them as inputs inherits a dependence on a black-box algorithm, which limits strict reproducibility across device generations or firmware versions.

</v-click>

---

# Future Work

- Validate against cohorts with concurrent neuroendocrine assays (cortisol, DHEA-S, catecholamines) — the primary mediators closest to the autonomic axis, not available in the present cohort
- Extend validation to older and clinical populations where AL's health-outcome relationships are best established
- Longitudinal follow-up: does wearable AL predict health trajectories over years?
- The temporal axis opened here remains largely unexplored in the broader AL literature — dynamical features of dysregulation such as dwell time and vulnerability are recoverable from any longitudinal physiological panel, and the HMM framework generalizes well beyond sleep data

---
layout: center
class: text-center
---

# Thank You

<div class="mt-8 text-sm opacity-70 max-w-lg mx-auto leading-relaxed">

This work would not have been possible without the guidance and support of my advisors.

</div>

<div class="mt-6 grid grid-cols-4 gap-6 max-w-2xl mx-auto text-center text-sm">
<div class="flex flex-col items-center gap-2">
<img :src="'/danforth.webp'" class="w-20 h-20 rounded-full object-cover opacity-90" />
<div class="font-bold text-xs">Christopher M. Danforth</div>
<div class="opacity-50 text-xs tracking-widest">ADVISOR</div>
</div>
<div class="flex flex-col items-center gap-2">
<img :src="'/lovato.webp'" class="w-20 h-20 rounded-full object-cover opacity-90" />
<div class="font-bold text-xs">Juniper Lovato</div>
<div class="opacity-50 text-xs tracking-widest">ADVISOR</div>
</div>
<div class="flex flex-col items-center gap-2">
<img :src="'/price.webp'" class="w-20 h-20 rounded-full object-cover opacity-90" />
<div class="font-bold text-xs">Matthew Price</div>
<div class="opacity-50 text-xs tracking-widest">COMMITTEE CHAIR</div>
</div>
<div class="flex flex-col items-center gap-2">
<img :src="'/feng.webp'" class="w-20 h-20 rounded-full object-cover opacity-90" />
<div class="font-bold text-xs">Yuanyuan Feng</div>
<div class="opacity-50 text-xs tracking-widest">COMMITTEE</div>
</div>
</div>

<div class="mt-8 border-t border-slate-700 pt-6 flex items-center gap-8 justify-center">
  <img :src="'/ethics_lab_logo.png'" class="h-10 opacity-80" />
  <div class="text-xs opacity-50 text-left">Special thanks to my peers at the<br/>UVM Computational Ethics Lab</div>
  <div class="w-px h-8 bg-slate-700"></div>
  <div class="flex items-center gap-3">
    <img :src="'/fudolig.png'" class="w-10 h-10 rounded-full object-cover opacity-90" />
    <div class="text-xs text-left"><div class="font-bold">Mikaela Fudolig</div><div class="opacity-50">for guidance on the LEMURS dataset</div></div>
  </div>
</div>
<div class="mt-6 text-sm opacity-40">Questions?</div>
