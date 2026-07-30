<div align="center">
  <h1>Shell Scripting Part 2</h1>
    <img src="https://img.shields.io/badge/Course-Shell%20Scripting%20Part%202-green?style=for-the-badge">
</div>

---

<h2 id="section-1">1. Writing a Node Health Monitoring Script</h2>

<h3>Objective</h3>
<ul>
  <li>Create a reusable shell script to check operating system metrics (disk space, memory, and CPU availability) for automated troubleshooting.</li>
</ul>

<h3>Initial Script Structure (`node_health.sh`)</h3>
<ul>
  <li><b>Shebang:</b> Always start with <code>#!/bin/bash</code> to define the correct shell interpreter.</li>
  <li><b>Metadata Header:</b> Include comments at the top detailing the author, date, purpose, and version.</li>
  <li><b>Core Commands Used:</b>
    <ul>
      <li><code>df -h</code>: Prints disk storage space.</li>
      <li><code>free -g</code>: Prints memory status in gigabytes.</li>
      <li><code>nproc</code>: Prints the total CPU count.</li>
    </ul>
  </li>
</ul>

---

<h2 id="section-2">2. Debugging & Error Handling Flags</h2>

<h3>Adding Metadata & Debug Modes</h3>
<ul>
  <li><b>Echo Statements:</b> Useful for manual labeling (e.g., <code>echo "Disk Space:"</code>), but hard to maintain in large scripts.</li>
  <li><b>Debug Flag (<code>set -x</code>):</b> Forces the shell to print every command and its expanded variables to the terminal before showing output.</li>
</ul>

<h3>Enterprise Error-Handling Flags</h3>
<ul>
  <li><b><code>set -e</code>:</b> Exits the script immediately if any command returns a non-zero exit status (fails).</li>
  <li><b><code>set -o pipefail</code>:</b> Ensures that if any command <i>within a piped chain</i> fails, the entire pipeline fails (fixing a blind spot in <code>set -e</code>).</li>
  <li><b>Best Practice:</b> Declare flags on separate lines for easier modular toggling.</li>
</ul>

---

<h2 id="section-3">3. Process Filtering, AWK, and Pipes</h2>

<h3>Inspecting System Processes</h3>
<ul>
  <li><b><code>ps -ef</code>:</b> Displays all currently running system processes.</li>
  <li><b>Filtering:</b> Use <code>ps -ef | grep amazon</code> to isolate specific rows.</li>
</ul>

<h3>The Pipe Operator (<code>|</code>)</h3>
<ul>
  <li>Sends the standard output (<code>STDOUT</code>) of the command on the left directly as standard input (<code>STDIN</code>) to the command on the right.</li>
</ul>

<h3>Column Extraction with AWK</h3>
<ul>
  <li>While <code>grep</code> filters rows, <b>AWK</b> isolates specific columns/fields.</li>
  <li><b>Example (Extracting Process IDs):</b> 
    <pre><code>ps -ef | grep amazon | awk -F" " '{print $2}'</code></pre>
  </li>
  <li><b>Explanation:</b> <code>-F" "</code> sets space as a delimiter; <code>print $2</code> outputs only the second column (PID).</li>
</ul>

---

<h2 id="section-4">4. Network Utilities: CURL vs. WGET</h2>

<ul>
  <li><b>CURL:</b> Makes HTTP/HTTPS requests to web links and prints the output directly to the terminal screen (commonly used for fetching remote logs or hitting APIs).</li>
  <li><b>WGET:</b> Downloads the target file from the internet and permanently saves it to the local machine disk.</li>
</ul>

---

<h2 id="section-5">5. Filesystem Discovery & Root Permissions</h2>

<ul>
  <li><b>Find Command:</b> Searches the entire filesystem tree based on patterns (e.g., <code>sudo find / -name "config.file"</code>).</li>
  <li><b>Sudo / User Switching:</b> Avoid running everyday tasks as <code>root</code> to prevent accidental file deletion. Use <code>sudo su -</code> only when elevated privileges are required.</li>
</ul>

---

<h2 id="section-6">6. Control Flow: Conditionals & For Loops</h2>

<h3>If-Else Conditional Syntax</h3>
<pre><code>if [ $NUM1 -gt $NUM2 ]; then
    echo "Greater"
else
    echo "Smaller"
fi</code></pre>
<p><i>Note:</i> Conditional blocks always close with the reverse spelling keyword: <code>fi</code>.</p>

<h3>For Loop Syntax</h3>
<pre><code>for i in {1..5}; do
    echo "Iteration: $i"
done</code></pre>

---

<h2 id="section-7">7. Signal Handling & The TRAP Command</h2>

<ul>
  <li><b>Signals:</b> Asynchronous notifications sent to processes (e.g., pressing <code>Ctrl + C</code> sends the <code>SIGINT</code> interrupt signal to kill a script).</li>
  <li><b>The TRAP Command:</b> Intercepts system signals to handle graceful shutdowns or cleanup operations.
    <pre><code>trap "echo 'Interrupted! Cleaning up...'; exit 1" SIGINT</code></pre>
  </li>
  <li><b>Use Case:</b> Prevents database corruption by cleaning up half-written files if an engineer cancels a script midway.</li>
</ul>
