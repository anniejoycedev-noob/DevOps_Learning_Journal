<div align="center">
  <h1>Git Branching Strategy</h1>
    <img src="https://img.shields.io/badge/Course-Git%20Branching%20Strategy-green?style=for-the-badge">
  </a>
</div>

---

<h2 id="section-1">1. Introduction to Git Branching Strategy</h2>

<h3>Why Git Branching Strategy Matters</h3>
<ul>
  <li>If you go through top 20 or top 50 DevOps interview questions on any website, git branching strategy is almost always included.</li>
  <li><b>The Primary Goal of any Organization:</b> To ensure that customers get prompt releases and new features on time (e.g., delivering updates every 15 days, 1 month, or 2 months like products such as Amazon or Flipkart). An efficient branching strategy makes this possible.</li>
</ul>

<h3>Practical Reference Used in Lecture</h3>
<ul>
  <li><b>Kubernetes Repository:</b> Hosted on GitHub as an open-source project with close to <b>3,300 contributors</b>. Looking at how Kubernetes coordinates thousands of contributors and delivers new versions every few months serves as a real-world blueprint that can be added to resumes and explained in interviews.</li>
</ul>

---

<h2 id="section-2">2. What is a Branch? (Definition & Analogy)</h2>

<ul>
  <li><b>Definition:</b> A branch is essentially a <b>separation</b> from the existing codebase.</li>
  <li><b>The Calculator Analogy:</b> 
    <ul>
      <li>Imagine you have a calculator application with addition, subtraction, multiplication, and division working fine on the default `master` or `main` branch.</li>
      <li>If you want to introduce breaking or advanced changes—such as version 2 calculator features like percentages—you don't make changes directly to the existing master/main branch.</li>
      <li>Instead, you create a new branch (called `V2`, `feature_calculator`, `feature_V2`, or `feature_advanced_calculator`), develop and test the code there, and once confident, merge it back into the existing functionality. Afterward, the feature branch can be deleted.</li>
      <li><b>Core Reason:</b> Creating a branch ensures that major or breaking changes do not affect the existing stable functionality delivered to customers.</li>
    </ul>
  </li>
</ul>

---

<h2 id="section-3">3. Real-World Scenario 1: The Uber App Evolution</h2>

<p>To understand why feature branching is critical, consider how Uber evolved over time:</p>
<div align="center">
  <pre>
  <b>Master / Main Branch (Cabs):</b> ───●─────●─────●─────●─────●─────>
                                 \               /
  <b>Feature Branch (Bikes):</b>         └───o─────o───┘ (Merged back when ready)
                                                 \               /
  <b>Feature Branch (Intercity):</b>                     └───o─────o───┘
  </pre>
</div>

<ul>
  <li><b>Phase 1 (Cabs Only):</b> Uber operated purely as a cab application. Active development and fixes happened on the main codebase.</li>
  <li><b>Phase 2 (Introducing Bikes):</b> To gain traction, product managers wanted to introduce "Uber Bikes". Developers weren't confident if adding bikes would break the existing cab experience. 
    <ul>
      <li><i>Solution:</i> They created a separate <code>feature_bikes</code> branch. 5 to 6 developers worked and tested the bike functionality independently while active cab development continued safely on the main branch. Once fully confident, the bike changes were merged back into the repository, and the feature branch was deleted.</li>
    </ul>
  </li>
  <li><b>Phase 3 (Introducing Intercity):</b> Later, they wanted to introduce an "Intercity" travel feature (operating between different cities). 
    <ul>
      <li><i>Solution:</i> Following the exact same model, they created a new <code>feature_intercity</code> branch, developed and tested it safely, and merged it back into master once complete.</li>
    </ul>
  </li>
</ul>

---

<h2 id="section-4">4. Real-World Scenario 2: Kubernetes GitHub Repository Structure</h2>

<ul>
  <li><b>Master Branch:</b> People actively work on the core master branch for continuous development.</li>
  <li><b>Feature Branches:</b> The repository contains multiple active feature branches managed by sub-teams, such as:
    <ul>
      <li><code>feature-rate-limiting</code></li>
      <li><code>feature-server-side-applying</code></li>
      <li><code>feature-workload-ga</code></li>
    </ul>
  </li>
  <li><b>How it flows:</b> Developers work on these specific feature branches. Once their changes are verified, they merge them back into the master branch and delete the feature branches.</li>
  <li><b>Release Branches:</b> When Kubernetes prepares for a scheduled update (e.g., moving from release 1.26 to a new release in April like <code>release-1.27</code>), they spin off a dedicated release branch. Active development continues on master, while end-to-end functionality testing is locked down and executed on the release branch before shipping to customers.</li>
</ul>

---

<h2 id="section-5">5. The Four Core Branches in a Branching Strategy</h2>

<div align="center">
  <pre>
  <b>Master / Main Branch</b> ◄────── (All features, hotfixes, and release changes merge back here)
         │
         ├──► <b>Feature Branches</b>     (For developing new features & breaking changes)
         │
         ├──► <b>Release Branches</b>     (Frozen codebases used for QA testing & shipping to customers)
         │
         └──► <b>Hotfix Branches</b>      (Short-lived patches for urgent production bugs)
  </pre>
</div>

<h3>1. Master / Trunk / Main Branch</h3>
<ul>
  <li><b>Rule:</b> Must always be kept completely up-to-date with the latest code changes.</li>
  <li><b>Rule:</b> All branch types (feature branches, hotfix branches, and sometimes release branches) should eventually cascade and merge their changes back into Master so anyone can reference the latest version of the application.</li>
</ul>

<h3>2. Feature Branches</h3>
<ul>
  <li><b>Purpose:</b> Used when teams want to introduce new features or breaking changes.</li>
  <li><b>Examples mentioned:</b> `feature_percentage`, `feature_exponent`, `feature_dividend`, `feature_bikes`, `feature_intercity`.</li>
  <li><b>Workflow:</b> Multiple developers collaborate here. When testing passes and stability is assured, it merges back into Master and is deleted.</li>
</ul>

<h3>3. Release Branches</h3>
<ul>
  <li><b>Purpose:</b> Used to ship code safely to customers.</li>
  <li><b>Why not release directly from Master?</b> Master is constantly moving due to active development. While running end-to-end testing or SRE tests, you don't want new, unverified changes entering the test pipeline. A release branch cuts off a stable point in time so testing can run safely.</li>
  <li><b>Example:</b> Kubernetes creates branches like `release-1.26` or `release-1.27`.</li>
</ul>

<h3>4. Hotfix / Bugfix Branches</h3>
<ul>
  <li><b>Purpose:</b> Created immediately when a user reports a critical production bug.</li>
  <li><b>Characteristics:</b> Very short-lived (lasting 1 to 2 days). </li>
  <li><b>Crucial Rule:</b> Changes made in a hotfix branch must be merged back into <b>both</b> the Master branch <b>and</b> all active Release branches.</li>
</ul>

---

<h2 id="section-6">6. Interview Questions & Summary Takeaways</h2>
<ul>
  <li><b>Q1: From which branch do you perform releases?</b> Answer: Release branches.</li>
  <li><b>Q2: What is a feature branch?</b> Answer: A branch used to introduce new features or breaking changes away from the main application until testing is complete.</li>
  <li><b>Q3: Which branch must always stay up to date?</b> Answer: Master, trunk, or main branch.</li>
  <li><b>Q4: What is a hotfix branch and where must its code merge?</b> Answer: A short-lived patch branch for urgent production bugs whose fixes must merge into both Master and active Release branches.</li>
</ul>
