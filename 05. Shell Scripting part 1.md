<div align="center">
  <h1>Shell Scripting Part 1</h1>
  <p>Every single concept, command, code example, and explanation from the lecture</p>
    <img src="https://img.shields.io/badge/Course-Shell%20Scripting%20Zero%202%20Hero-green?style=for-the-badge">
  </a>
</div>

---

<h2 id="section-1">1. Why Shell Scripting? (Automation Concept & Examples)</h2>

<h3>Definition of Automation</h3>
<ul>
  <li>Automation is the process of reducing or eliminating repetitive, manual effort.</li>
</ul>

<h3>The Progression Example</h3>
<ol>
  <li><b>Printing 1 to 10:</b> Easy to do manually using <code>echo</code>.</li>
  <li><b>Printing 1 to 1,000:</b> Painful manually, but technically possible.</li>
  <li><b>Printing 1 to 1,000,000:</b> Humanly impossible by hand—requires scripting.</li>
  <li><b>Creating Files:</b> Creating 100 or 2,000 files using <code>touch</code> manually takes too long; shell scripts execute this instantly.</li>
</ol>

---

<h2 id="section-2">2. Creating, Listing, and Documenting Commands</h2>

<h3>Commands Covered</h3>
<ul>
  <li><b><code>touch &lt;filename.sh&gt;</code>:</b> Creates an empty file. Uses <code>.sh</code> extension by convention.</li>
  <li><b><code>ls</code>:</b> Lists files/folders in the current directory.</li>
  <li><b><code>ls -lrt</code>:</b> Long format listing sorted by time in reverse order. Shows:
    <ul>
      <li>Permissions & file type</li>
      <li>Owner and Group owner</li>
      <li>File size</li>
      <li>Modification timestamp</li>
    </ul>
  </li>
  <li><b><code>man &lt;command&gt;</code>:</b> Opens the Linux instruction manual for any command (e.g., <code>man ls</code>, <code>man touch</code>).</li>
</ul>

<h3>Linux Terminal UX Tip</h3>
<ul>
  <li>Double-clicking text on a Linux terminal automatically copies it; use <code>Cmd+V</code> / <code>Ctrl+V</code> to paste.</li>
</ul>

---

<h2 id="section-3">3. Text Editors (VI vs. VIM vs. Touch)</h2>

<h3>Touch vs. VIM/VI Comparison</h3>
<ul>
  <li><b><code>touch</code>:</b> Creates an empty file without opening it.
    <ul>
      <li><i>Crucial Automation Rule:</i> Use <code>touch</code> inside automated scripts when generating bulk files (e.g., 1,000 files). Never use VIM in a script loop because opening thousands of editor buffers simultaneously will consume memory and crash the system.</li>
    </ul>
  </li>
  <li><b><code>vi</code> / <code>vim</code>:</b> Creates <i>and</i> opens the file for editing simultaneously. <code>vi</code> comes pre-installed on every Linux distribution.</li>
</ul>

<h3>VIM Navigation Basics</h3>
<ol>
  <li>Open file: <code>vim script.sh</code></li>
  <li>Enter Insert Mode: Press <code>Esc</code> then type <code>i</code> (look for <code>-- INSERT --</code> at the bottom).</li>
  <li>Save and Exit: Press <code>Esc</code> ➔ type <code>:wq!</code> ➔ press Enter.</li>
  <li>Exit without saving: Press <code>Esc</code> ➔ type <code>:q!</code> ➔ press Enter.</li>
</ol>

<h3>Reading Files Without Opening</h3>
<ul>
  <li><b><code>cat &lt;filename&gt;</code>:</b> Prints text contents directly to the terminal without launching an editor.</li>
</ul>

---

<h2 id="section-4">4. The Shebang Line & Deep-Dive Interpreter Logic</h2>

<h3>What is the Shebang?</h3>
<p>The first line of a script starting with <code>#!</code> tells the operating system kernel which executable/interpreter to use:</p>
<pre><code>#!/bin/bash</code></pre>

<h3>Available Shell Executables</h3>
<ul>
  <li><code>bash</code> (Bourne Again Shell)</li>
  <li><code>sh</code> (Bourne Shell)</li>
  <li><code>ksh</code> (Korn Shell)</li>
  <li><code>dash</code> (Debian Almquist Shell)</li>
</ul>

<h3>The <code>/bin/sh</code> vs. <code>/bin/dash</code> Interview Question</h3>
<ul>
  <li><b>Historical Behavior:</b> <code>/bin/sh</code> was soft-linked to <code>/bin/bash</code> in older systems.</li>
  <li><b>Modern Behavior:</b> Operating systems like Ubuntu now soft-link <code>/bin/sh</code> to <code>/bin/dash</code> by default.</li>
  <li><b>Why it breaks:</b> Syntax differs between shells (e.g., how for-loops execute). If you write a script using Bash features but declare <code>#!/bin/sh</code> on an OS where `sh` points to `dash`, the script will fail.</li>
  <li><b>Best Practice:</b> Always explicitly use <code>#!/bin/bash</code>.</li>
</ul>

---

<h2 id="section-5">5. File Permissions & CHMOD Mechanics</h2>

<h3>Why "Permission Denied"?</h3>
<p>Linux is secure by default. Newly created files lack execute rights when you attempt <code>./script.sh</code>. You must assign permissions using <code>chmod</code> (Change Mode).</p>

<h3>The 3 Categories of Users</h3>
<ol>
  <li><b>User (Owner):</b> The individual who created the file.</li>
  <li><b>Group:</b> The user group the owner belongs to.</li>
  <li><b>Others (Everyone):</b> All other system users.</li>
</ol>

<h3>The 4-2-1 Numeric Formula</h3>
<ul>
  <li><b>Read (r) = 4</b></li>
  <li><b>Write (w) = 2</b></li>
  <li><b>Execute (x) = 1</b></li>
</ul>

<p><b>Sums for combinations:</b></p>
<ul>
  <li><code>7</code> = 4 + 2 + 1 (Full Read, Write, Execute)</li>
  <li><code>6</code> = 4 + 2 (Read & Write)</li>
  <li><code>5</code> = 4 + 1 (Read & Execute)</li>
  <li><code>4</code> = Read Only</li>
  <li><code>1</code> = Execute Only</li>
</ul>

<p><b>Examples:</b></p>
<pre><code>chmod 777 script.sh   # Read/Write/Execute for Owner, Group, Others
chmod 770 script.sh   # Full access for Owner & Group; zero for Others
chmod 444 script.sh   # Read-only for everyone (Execution denied)</code></pre>

---

<h2 id="section-6">6. Directory Operations & Shell History</h2>

<ul>
  <li><b><code>pwd</code> (Print Working Directory):</b> Shows absolute current path.</li>
  <li><b><code>mkdir &lt;directory_name&gt;</code>:</b> Creates a new directory.</li>
  <li><b><code>cd &lt;directory&gt;</code>:</b> Changes directory.
    <ul>
      <li><code>cd ..</code>: Move up 1 level.</li>
      <li><code>cd ../..</code>: Move up 2 levels.</li>
    </ul>
  </li>
  <li><b><code>rm &lt;filename&gt;</code>:</b> Removes a file.</li>
  <li><b><code>rm -r &lt;foldername&gt;</code> / <code>rm -rf</code>:</b> Recursively/forcefully deletes a directory and contents.</li>
  <li><b><code>history</code>:</b> Displays all previously typed commands in the current session.</li>
</ul>

---

<h2 id="section-7">7. Writing & Executing Your First Complete Script</h2>

<h3>Script Example (`sample.sh`)</h3>
<pre><code>#!/bin/bash

# Comment: Create a directory and populating files
mkdir Abhishek
cd Abhishek
touch firstfile secondfile</code></pre>

<h3>Execution Steps</h3>
<ol>
  <li>Make executable: <code>chmod 777 sample.sh</code></li>
  <li>Run script: <code>./sample.sh</code> or <code>sh sample.sh</code></li>
  <li>Verify creation: <code>cd Abhishek && ls</code></li>
</ol>

---

<h2 id="section-8">8. Real-World DevOps Use Case (John's 10,000 Linux VMs)</h2>

<h3>Scenario</h3>
<p>A DevOps Engineer named John manages <b>10,000 Linux VMs</b> at Amazon. Developers frequently report performance degradation, out-of-memory errors, and thread slowdowns on specific nodes.</p>

<h3>The Shell Script Solution</h3>
<ol>
  <li>Instead of manually logging into servers, John writes a centralized node-health monitoring shell script saved in Git.</li>
  <li>The script executes via automated cron job daily/weekly.</li>
  <li>It checks CPU spikes, memory limits, process states, and open file handles.</li>
  <li>It sends an automated summary email: <i>"Checked 10,000 VMs: 10 suspicious nodes found (5 high memory, 5 high CPU)."</i></li>
</ol>

---

<h2 id="section-9">9. Node Health & Performance Monitoring Commands</h2>

<ul>
  <li><b><code>nproc</code>:</b> Returns the count of assigned CPU cores.</li>
  <li><b><code>free -m</code>:</b> Displays available, used, and total memory (RAM) in MBs.</li>
  <li><b><code>df -h</code>:</b> Displays mounted disk storage capacity and percentage used.</li>
  <li><b><code>top</code>:</b> Opens a live system dashboard displaying overall CPU%, RAM usage, process list, and Process IDs (PIDs).</li>
</ul>
