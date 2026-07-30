<div align="center">
  <h1>Day 6 - Linux & Shell Scripting Complete Notes</h1>
  <p>Comprehensive breakdown of OS Architecture, Linux Kernel Responsibilities, and Basic Shell Commands</p>
    <img src="https://img.shields.io/badge/Course-DevOps%20Zero%20to%20Hero-green?style=for-the-badge">
  </a>
</div>

---

<h2 id="os-fundamentals">1. Operating System Fundamentals</h2>

<h3>What is an Operating System?</h3>
<ul>
  <li>An Operating System acts as the core <b>bridge/medium of communication</b> between user applications (software) and physical server components (hardware).</li>
  <li><b>Communication Lifecycle:</b>
    <ul>
      <li>User installs an application on a server.</li>
      <li>The application sends a request to the <b>OS</b>.</li>
      <li>The OS communicates with the <b>Hardware</b> (CPU, RAM, I/O, Hard Disk) and routes the response back through the application to the user.</li>
    </ul>
  </li>
</ul>

---

<h2 id="why-linux">2. Why Linux Dominates the IT & Production Industry</h2>
<p>Unlike personal laptops that usually run Windows or macOS, production and staging servers run Linux for several key reasons:</p>
<ul>
  <li><b>Free and Open Source:</b> Unlike proprietary Windows, Linux is freely available and customizable.</li>
  <li><b>Superior Security:</b> Linux is inherently more secure out-of-the-box, meaning you typically do not need to install heavy anti-malware or antivirus software like you do on Windows.</li>
  <li><b>Distributions (Distros):</b> Offers flexibility via various lightweight vendors/distributions such as <b>Ubuntu, CentOS, Red Hat, Alpine, and Debian</b>.</li>
  <li><b>Performance Speed:</b> Linux is extremely fast and lightweight because production servers omit resource-heavy graphical user interfaces (GUIs).</li>
</ul>

---

<h2 id="linux-architecture">3. Linux Operating System Architecture</h2>

<p>The Linux OS architecture consists of layered components:</p>

<div align="center">
  <pre>
  ┌────────────────────────────────────────────────────────┐
  |    Compilers | User Processes | System Software        |
  ├────────────────────────────────────────────────────────┤
  |                    System Libraries                    |
  ├────────────────────────────────────────────────────────┤
  |                     <b>THE KERNEL</b>                         |
  |     (Device, Memory, Process Management & Sys Calls)   |
  └────────────────────────────────────────────────────────┤
                             ▲
                             ▼
                      <b>HARDWARE LAYER</b>
                 (CPU, RAM, Storage, I/O)
  </pre>
</div>

<h3>The Kernel (The Heart of Linux)</h3>
<p>The kernel handles the core communication logic between user space and physical hardware. It has <b>four primary responsibilities</b>:</p>
<ol>
  <li><b>Device Management:</b> Controlling connected hardware devices.</li>
  <li><b>Memory Management:</b> Allocating and managing physical and virtual RAM.</li>
  <li><b>Process Management:</b> Monitoring and managing execution processes.</li>
  <li><b>Handling System Calls:</b> Processing application-level requests sent to the system level.</li>
</ol>

<h3>Supporting Architecture Layers</h3>
<ul>
  <li><b>System Libraries:</b> Functions (like <code>libc</code>) that handle standard tasks and pass requests down to the kernel.</li>
  <li><b>Compilers & User Processes:</b> Translators and background utilities needed to run application code (like Java, Python, or binaries).</li>
</ul>

---

<h2 id="shell-scripting-intro">4. Introduction to Shell & Shell Scripting</h2>
<ul>
  <li><b>What is a Shell?</b> A command-line tool used to talk directly to the Linux operating system.</li>
  <li><b>Why CLI over GUI?</b> Production servers do not run Graphical User Interfaces because GUIs consume unnecessary system resources.</li>
  <li><b>Bash:</b> The standard, most widely used shell environment across modern Linux distributions.</li>
</ul>

---

<h2 id="practical-commands">5. Practical Shell Commands & Server Management</h2>

<h3>A. Logging into an EC2 Instance via CLI</h3>
<p>To connect to an AWS Linux instance from your local terminal, use the SSH command:</p>
<pre><code>ssh -i "path/to/key.pem" ubuntu@&lt;public-ip-address&gt;</code></pre>
<p><i>Note on Permissions:</i> If your <code>.pem</code> key gives a "permissions too open" error, restrict access using: <code>chmod 600 key.pem</code></p>

<h3>B. Navigation & Exploration Commands</h3>
<ul>
  <li><b><code>pwd</code> (Print Working Directory):</b> Outputs your exact current absolute path.</li>
  <li><b><code>ls</code>:</b> Lists files and folders in the current directory.</li>
  <li><b><code>ls -lrt</code>:</b> Lists files with detailed metadata, including:
    <ul>
      <li>File type (<code>d</code> for directory, <code>-</code> for regular file)</li>
      <li>Permissions, owner, and group owner</li>
      <li>File size and exact creation timestamp</li>
    </ul>
  </li>
  <li><b><code>cd &lt;directory&gt;</code>:</b> Changes the current directory.</li>
  <li><b><code>cd ..</code>:</b> Moves back one directory level.</li>
  <li><b><code>cd ../..</code>:</b> Moves back multiple directory levels.</li>
</ul>

<h3>C. File Creation & Text Editing</h3>
<ul>
  <li><b><code>touch &lt;filename&gt;</code>:</b> Creates an empty file immediately.</li>
  <li><b><code>vi &lt;filename&gt;</code>:</b> Opens the <code>vi</code> text editor to create or edit a file.
    <ul>
      <li><i>How to use:</i> Press <code>Esc</code> then <code>i</code> to enter <b>Insert Mode</b> to type. Press <code>Esc</code> then type <code>:wq</code> to <b>Save and Quit</b>.</li>
    </ul>
  </li>
  <li><b><code>cat &lt;filename&gt;</code>:</b> Prints the text file contents directly to the terminal screen.</li>
  <li><b><code>mkdir &lt;foldername&gt;</code>:</b> Creates a new directory.</li>
  <li><b><code>rm &lt;filename&gt;</code>:</b> Deletes a file.</li>
  <li><b><code>rm -r &lt;foldername&gt;</code>:</b> Recursively deletes a directory and all of its contents.</li>
</ul>

<h3>D. System Monitoring & Resource Management</h3>
<ul>
  <li><b><code>free -m</code>:</b> Displays total, used, and free system memory (RAM) in megabytes.</li>
  <li><b><code>nproc</code>:</b> Returns the total number of CPU cores allocated to the system.</li>
  <li><b><code>df -h</code>:</b> Displays hard disk space usage and available capacity in a human-readable format.</li>
  <li><b><code>top</code>:</b> Opens a real-time monitoring dashboard showing overall CPU usage, memory utilization, and active system processes. <i>(The standard command used in troubleshooting bottlenecks).</i></li>
</ul>
