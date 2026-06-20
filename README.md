
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pseudocode Pro - Offline Editor</title>
<style>
  :root {
    --bg: #1a1a2e;
    --bg2: #16213e;
    --bg3: #0f3460;
    --accent: #e94560;
    --accent2: #533483;
    --text: #e0e0e0;
    --text2: #a0a0b0;
    --border: #2a2a4a;
    --green: #4ade80;
    --yellow: #fbbf24;
    --red: #f87171;
    --blue: #60a5fa;
    --purple: #c084fc;
    --font-mono: 'Courier New', 'Consolas', monospace;
    --font-ui: 'Segoe UI', system-ui, sans-serif;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { background: var(--bg); color: var(--text); font-family: var(--font-ui); height: 100vh; display: flex; flex-direction: column; overflow: hidden; }

  /* Header */
  header { background: var(--bg2); border-bottom: 1px solid var(--border); padding: 8px 16px; display: flex; align-items: center; gap: 16px; flex-shrink: 0; }
  .logo { font-weight: 800; font-size: 1rem; color: var(--accent); letter-spacing: 0.05em; text-transform: uppercase; }
  .logo span { color: var(--text2); font-weight: 400; }
  .header-tabs { display: flex; gap: 2px; flex: 1; }
  .tab-btn { background: none; border: none; color: var(--text2); padding: 4px 12px; cursor: pointer; border-radius: 4px; font-size: 0.8rem; transition: all 0.15s; }
  .tab-btn:hover { background: var(--border); color: var(--text); }
  .tab-btn.active { background: var(--accent); color: white; }
  .header-right { display: flex; gap: 8px; align-items: center; }
  .exec-mode { font-size: 0.75rem; color: var(--text2); }
  select.mode-select { background: var(--bg3); color: var(--text); border: 1px solid var(--border); border-radius: 4px; padding: 3px 6px; font-size: 0.75rem; cursor: pointer; }

  /* Main layout */
  .main { display: flex; flex: 1; overflow: hidden; }

  /* Sidebar */
  .sidebar { width: 200px; background: var(--bg2); border-right: 1px solid var(--border); display: flex; flex-direction: column; flex-shrink: 0; }
  .sidebar-header { padding: 10px 12px; font-size: 0.7rem; text-transform: uppercase; letter-spacing: 0.1em; color: var(--text2); border-bottom: 1px solid var(--border); }
  .file-list { flex: 1; overflow-y: auto; padding: 4px; }
  .file-item { padding: 6px 8px; border-radius: 4px; cursor: pointer; font-size: 0.82rem; color: var(--text2); transition: all 0.15s; display: flex; align-items: center; gap: 6px; }
  .file-item:hover { background: var(--border); color: var(--text); }
  .file-item.active { background: var(--accent2); color: white; }
  .file-item .file-icon { font-size: 0.7rem; }
  .sidebar-footer { padding: 8px; display: flex; gap: 4px; border-top: 1px solid var(--border); }
  .icon-btn { background: var(--bg3); border: none; color: var(--text2); padding: 5px 8px; border-radius: 4px; cursor: pointer; font-size: 0.75rem; transition: all 0.15s; flex: 1; }
  .icon-btn:hover { background: var(--accent); color: white; }

  /* Editor area */
  .editor-area { flex: 1; display: flex; flex-direction: column; overflow: hidden; }
  .editor-toolbar { background: var(--bg2); border-bottom: 1px solid var(--border); padding: 6px 12px; display: flex; gap: 6px; align-items: center; flex-shrink: 0; }
  .run-btn { background: var(--green); color: #000; border: none; border-radius: 50%; width: 28px; height: 28px; cursor: pointer; font-size: 1rem; display: flex; align-items: center; justify-content: center; transition: all 0.15s; font-weight: bold; }
  .run-btn:hover { transform: scale(1.1); box-shadow: 0 0 12px rgba(74,222,128,0.5); }
  .tool-btn { background: var(--bg3); border: 1px solid var(--border); color: var(--text2); padding: 4px 10px; border-radius: 4px; cursor: pointer; font-size: 0.75rem; transition: all 0.15s; }
  .tool-btn:hover { background: var(--border); color: var(--text); }
  .status-indicator { margin-left: auto; font-size: 0.75rem; padding: 3px 10px; border-radius: 10px; }
  .status-ok { background: rgba(74,222,128,0.15); color: var(--green); }
  .status-err { background: rgba(248,113,113,0.15); color: var(--red); }

  /* Split pane */
  .editor-split { flex: 1; display: flex; overflow: hidden; }
  .code-pane { flex: 1; display: flex; flex-direction: column; position: relative; }
  .code-editor { flex: 1; background: #0d0d1a; color: var(--text); font-family: var(--font-mono); font-size: 14px; line-height: 1.6; border: none; outline: none; resize: none; padding: 12px 12px 12px 52px; tab-size: 4; spellcheck: false; }
  .line-numbers { position: absolute; left: 0; top: 0; bottom: 0; width: 44px; background: #0a0a15; padding: 12px 0; font-family: var(--font-mono); font-size: 14px; line-height: 1.6; color: var(--text2); text-align: right; user-select: none; overflow: hidden; pointer-events: auto; cursor: pointer; z-index: 1; }
  .divider { width: 4px; background: var(--border); cursor: col-resize; transition: background 0.15s; }
  .divider:hover { background: var(--accent2); }
  .output-pane { width: 380px; min-width: 200px; display: flex; flex-direction: column; border-left: 1px solid var(--border); }
  .output-header { background: var(--bg2); padding: 8px 12px; font-size: 0.75rem; color: var(--text2); border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 8px; }
  .output-header strong { color: var(--text); }
  .clear-btn { margin-left: auto; background: none; border: none; color: var(--text2); cursor: pointer; font-size: 0.75rem; }
  .clear-btn:hover { color: var(--red); }
  .output-body { flex: 1; overflow-y: auto; padding: 12px; font-family: var(--font-mono); font-size: 13px; line-height: 1.6; }
  .output-line { margin-bottom: 2px; }
  .output-line.out { color: var(--text); }
  .output-line.err { color: var(--red); }
  .output-line.sys { color: var(--blue); font-style: italic; }
  .input-row { display: flex; border-top: 1px solid var(--border); padding: 8px; gap: 6px; }
  .input-field { flex: 1; background: var(--bg3); border: 1px solid var(--border); color: var(--text); font-family: var(--font-mono); font-size: 13px; padding: 5px 8px; border-radius: 4px; outline: none; }
  .input-field:focus { border-color: var(--accent2); }
  .input-send { background: var(--accent); border: none; color: white; padding: 5px 12px; border-radius: 4px; cursor: pointer; font-size: 0.8rem; }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 6px; height: 6px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }

  /* Syntax highlight overlay */
  .kw { color: #c084fc; }
  .str { color: #fbbf24; }
  .num { color: #60a5fa; }
  .comment { color: #4a5568; font-style: italic; }
  .fn { color: #4ade80; }

  /* ── Debugger toolbar ── */
  .debug-bar { display: none; background: #0d0d1a; border-bottom: 1px solid var(--border); padding: 5px 12px; gap: 6px; align-items: center; flex-shrink: 0; }
  .debug-bar.active { display: flex; }
  .dbg-btn { background: var(--bg3); border: 1px solid var(--border); color: var(--text2); padding: 3px 10px; border-radius: 4px; cursor: pointer; font-size: 0.75rem; transition: all 0.15s; }
  .dbg-btn:hover:not(:disabled) { background: var(--border); color: var(--text); }
  .dbg-btn:disabled { opacity: 0.4; cursor: default; }
  .dbg-btn.dbg-step  { border-color: var(--yellow); color: var(--yellow); }
  .dbg-btn.dbg-cont  { border-color: var(--green);  color: var(--green); }
  .dbg-btn.dbg-stop  { border-color: var(--red);    color: var(--red); }
  .dbg-line-info { font-size: 0.72rem; color: var(--text2); margin-left: 8px; font-family: var(--font-mono); }
  .dbg-line-info span { color: var(--yellow); font-weight: 700; }

  /* ── Line number gutter: breakpoints + current line ── */
  .ln-row { display: block; width: 100%; padding-right: 8px; position: relative; transition: color 0.1s; box-sizing: border-box; }
  .ln-row:hover { color: var(--text); }
  .ln-row.bp { color: var(--red) !important; }
  .ln-row.bp::before { content: '●'; position: absolute; left: 4px; color: var(--red); font-size: 10px; top: 3px; }
  .ln-row.current-line { background: rgba(251,191,36,0.15); color: var(--yellow) !important; }
  .ln-row.current-line::after { content: '▶'; position: absolute; left: 4px; color: var(--yellow); font-size: 9px; top: 4px; }

  /* ── Variable Watch panel ── */
  .watch-panel { background: var(--bg2); border-top: 1px solid var(--border); flex-shrink: 0; max-height: 220px; display: flex; flex-direction: column; }
  .watch-header { padding: 5px 12px; font-size: 0.7rem; text-transform: uppercase; letter-spacing: 0.08em; color: var(--text2); display: flex; align-items: center; gap: 8px; cursor: pointer; border-bottom: 1px solid transparent; }
  .watch-header:hover { color: var(--text); }
  .watch-header .watch-toggle-icon { margin-left: auto; transition: transform 0.2s; }
  .watch-header.open { border-bottom-color: var(--border); }
  .watch-header.open .watch-toggle-icon { transform: rotate(180deg); }
  .watch-body { display: none; overflow-y: auto; flex: 1; }
  .watch-body.open { display: block; }
  .watch-table { width: 100%; border-collapse: collapse; font-family: var(--font-mono); font-size: 12px; }
  .watch-table th { position: sticky; top: 0; background: var(--bg2); color: var(--text2); padding: 3px 10px; text-align: left; font-weight: 600; font-size: 0.68rem; text-transform: uppercase; border-bottom: 1px solid var(--border); }
  .watch-table td { padding: 3px 10px; border-bottom: 1px solid rgba(42,42,74,0.5); vertical-align: top; }
  .watch-table tr:last-child td { border-bottom: none; }
  .watch-table tr.changed td { background: rgba(251,191,36,0.08); }
  .wv-name  { color: var(--blue); }
  .wv-type  { color: var(--text2); font-size: 0.68rem; }
  .wv-val   { color: var(--green); word-break: break-all; }
  .wv-val.bool-true  { color: var(--green); }
  .wv-val.bool-false { color: var(--red); }
  .wv-val.undef  { color: var(--text2); font-style: italic; }
  .wv-empty { color: var(--text2); font-style: italic; font-size: 0.75rem; padding: 8px 12px; }
  .watch-stack { padding: 4px 10px 6px; font-size: 0.7rem; color: var(--text2); font-family: var(--font-mono); border-top: 1px solid var(--border); }
  .watch-stack strong { color: var(--purple); }

  /* Modal */
  .modal-overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.7); z-index: 100; align-items: center; justify-content: center; }
  .modal-overlay.open { display: flex; }
  .modal { background: var(--bg2); border: 1px solid var(--border); border-radius: 8px; padding: 20px; min-width: 300px; max-width: 480px; }
  .modal h3 { margin-bottom: 12px; color: var(--text); }
  .modal input { width: 100%; background: var(--bg3); border: 1px solid var(--border); color: var(--text); padding: 8px; border-radius: 4px; font-family: var(--font-mono); margin-bottom: 12px; outline: none; }
  .modal-btns { display: flex; gap: 8px; justify-content: flex-end; }
  .modal-btns button { padding: 6px 16px; border-radius: 4px; border: none; cursor: pointer; font-size: 0.85rem; }
  .btn-primary { background: var(--accent); color: white; }
  .btn-cancel { background: var(--border); color: var(--text); }
  .help-text { font-size: 0.78rem; color: var(--text2); margin-bottom: 12px; line-height: 1.5; }

  /* Syllabus toggle */
  .syllabus-toggle { display: flex; align-items: center; gap: 2px; background: var(--bg3); border: 1px solid var(--border); border-radius: 4px; padding: 2px 6px; cursor: pointer; font-size: 0.75rem; user-select: none; }
  .syl-opt { padding: 1px 5px; border-radius: 3px; color: var(--text2); transition: all 0.15s; }
  .syl-opt.active { background: var(--accent); color: white; font-weight: 700; }
  .syl-sep { color: var(--border); }

  /* Virtual file manager panel */
  .vfs-panel { background: var(--bg2); border-top: 1px solid var(--border); flex-shrink: 0; }
  .vfs-header { padding: 5px 12px; font-size: 0.7rem; text-transform: uppercase; letter-spacing: 0.08em; color: var(--text2); display: flex; align-items: center; gap: 8px; cursor: pointer; }
  .vfs-header:hover { color: var(--text); }
  .vfs-header .vfs-toggle-icon { margin-left: auto; transition: transform 0.2s; }
  .vfs-header.open .vfs-toggle-icon { transform: rotate(180deg); }
  .vfs-body { display: none; padding: 8px 12px; gap: 8px; flex-wrap: wrap; align-items: flex-start; }
  .vfs-body.open { display: flex; }
  .vfs-file-chip { background: var(--bg3); border: 1px solid var(--border); border-radius: 4px; padding: 3px 10px; font-size: 0.75rem; font-family: var(--font-mono); color: var(--text2); display: flex; align-items: center; gap: 6px; }
  .vfs-file-chip .vfs-del { cursor: pointer; color: var(--text2); font-size: 0.65rem; }
  .vfs-file-chip .vfs-del:hover { color: var(--red); }
  .vfs-file-chip .vfs-view { cursor: pointer; color: var(--blue); font-size: 0.7rem; }
  .vfs-empty { color: var(--text2); font-size: 0.75rem; font-style: italic; }
  .vfs-actions { display: flex; gap: 6px; margin-left: auto; }

  /* File content modal extras */
  .modal textarea { width: 100%; background: var(--bg3); border: 1px solid var(--border); color: var(--text); padding: 8px; border-radius: 4px; font-family: var(--font-mono); font-size: 12px; margin-bottom: 12px; outline: none; resize: vertical; min-height: 120px; }

  /* Syllabus badge in status */
  .syl-badge { font-size: 0.65rem; padding: 1px 6px; border-radius: 3px; background: var(--accent2); color: #ddd; margin-left: 4px; vertical-align: middle; }
</style>
</head>
<body>

<header>
  <div class="logo">Pseudo<span>Coding</span> <span style="font-size:0.65rem;color:var(--accent2)">MC</span></div>
  <div class="header-tabs">
    <button class="tab-btn active" onclick="switchTab('pseudocode')">Pseudocode</button>
    <button class="tab-btn" onclick="switchTab('python')">→ Python</button>
    <button class="tab-btn" onclick="switchTab('vb')">→ VB.NET</button>
  </div>
  <div class="header-right">
    <span class="exec-mode">Syllabus:</span>
    <div class="syllabus-toggle" id="syllabusToggle" onclick="toggleSyllabus()" title="Switch CIE syllabus">
      <span class="syl-opt" id="syl2210">2210</span>
      <span class="syl-sep">/</span>
      <span class="syl-opt" id="syl9618">9618</span>
    </div>
    <span class="exec-mode">Mode:</span>
    <select class="mode-select" id="execMode">
      <option value="click">Run on click</option>
      <option value="live">Live</option>
    </select>
  </div>
</header>

<div class="main">
  <div class="sidebar">
    <div class="sidebar-header">📁 Programs</div>
    <div class="file-list" id="fileList"></div>
    <div class="sidebar-footer">
      <button class="icon-btn" onclick="newProgram()" title="New">+ New</button>
      <button class="icon-btn" onclick="deleteProgram()" title="Delete">🗑</button>
    </div>
  </div>

  <div class="editor-area">
    <div class="editor-toolbar">
      <button class="run-btn" onclick="runCode()" title="Run (F5)">▶</button>
      <button class="tool-btn" onclick="clearOutput()">Clear</button>
      <button class="tool-btn" onclick="formatCode()">Format</button>
      <button class="tool-btn" onclick="saveFile()">💾 Save</button>
      <button class="tool-btn" onclick="loadFile()">📂 Load</button>
      <button class="tool-btn" onclick="downloadFile()">⬇ Download</button>
      <button class="tool-btn" id="debugStartBtn" onclick="startDebug()" title="Debug step-by-step (F6)" style="border-color:var(--yellow);color:var(--yellow)">🐞 Debug</button>
      <div class="status-indicator status-ok" id="statusBadge">✅ No errors</div>
    </div>
    <div class="debug-bar" id="debugBar">
      <button class="dbg-btn dbg-step" id="btnStep" onclick="debugStep()">⏭ Step</button>
      <button class="dbg-btn dbg-cont" id="btnCont" onclick="debugContinue()">▶ Continue</button>
      <button class="dbg-btn dbg-stop" id="btnStop" onclick="debugStop()">⏹ Stop</button>
      <span class="dbg-line-info">Line <span id="dbgLineNum">—</span> &nbsp;|&nbsp; <span id="dbgLineSrc" style="color:var(--text2);font-weight:400"></span></span>
    </div>

    <div class="editor-split">
      <div class="code-pane">
        <div class="line-numbers" id="lineNums">1</div>
        <textarea class="code-editor" id="codeEditor" spellcheck="false" placeholder="// Write your Cambridge pseudocode here...
// e.g.
DECLARE x : INTEGER
x ← 5
OUTPUT x * 2"
        ></textarea>
      </div>
      <div class="divider" id="divider"></div>
      <div class="output-pane">
        <div class="output-header">
          <strong>Output</strong>
          <span id="outputStatus" style="color:var(--text2)">Ready</span>
          <button class="clear-btn" onclick="clearOutput()">✕ Clear</button>
        </div>
        <div class="output-body" id="outputBody">
          <div class="output-line sys">// Welcome to Pseudocode Pro (Offline)</div>
          <div class="output-line sys">// Supports Cambridge IGCSE & A-Level syntax</div>
          <div class="output-line sys">// Press ▶ or F5 to run your code</div>
        </div>
        <div class="vfs-panel">
          <div class="vfs-header" id="vfsHeader" onclick="toggleVfsPanel()">
            📂 Virtual Files <span id="vfsCount" style="color:var(--accent);font-weight:700"></span>
            <div class="vfs-actions" onclick="event.stopPropagation()">
              <button class="tool-btn" style="font-size:0.7rem;padding:2px 7px" onclick="vfsNewFile()">+ New</button>
              <button class="tool-btn" style="font-size:0.7rem;padding:2px 7px" onclick="vfsImportFile()">Import</button>
            </div>
            <span class="vfs-toggle-icon">▼</span>
          </div>
          <div class="vfs-body" id="vfsBody"></div>
        </div>
        <!-- Variable Watch Panel -->
        <div class="watch-panel">
          <div class="watch-header open" id="watchHeader" onclick="toggleWatchPanel()">
            🔍 Variables &amp; Watch <span id="watchVarCount" style="color:var(--accent);font-weight:700"></span>
            <span class="watch-toggle-icon">▼</span>
          </div>
          <div class="watch-body open" id="watchBody">
            <div class="wv-empty">Run or debug your code to see variables here.</div>
          </div>
        </div>
        <div class="input-row" id="inputRow" style="display:none">
          <input class="input-field" id="inputField" placeholder="Enter input..." />
          <button class="input-send" onclick="submitInput()">↵</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- New file modal -->
<div class="modal-overlay" id="newFileModal">
  <div class="modal">
    <h3>New Program</h3>
    <p class="help-text">Give your program a name.</p>
    <input type="text" id="newFileName" placeholder="Program name..." />
    <div class="modal-btns">
      <button class="btn-cancel" onclick="closeModal('newFileModal')">Cancel</button>
      <button class="btn-primary" onclick="confirmNewProgram()">Create</button>
    </div>
  </div>
</div>

<!-- Input modal (for INPUT statements) -->
<div class="modal-overlay" id="inputModal">
  <div class="modal">
    <h3 id="inputPromptLabel">Enter value:</h3>
    <input type="text" id="inputModalField" placeholder="Type here..." />
    <div class="modal-btns">
      <button class="btn-primary" onclick="confirmModalInput()">OK</button>
    </div>
  </div>
</div>

<!-- VFS file view/edit modal -->
<div class="modal-overlay" id="vfsViewModal">
  <div class="modal" style="min-width:420px">
    <h3 id="vfsViewTitle">File: —</h3>
    <p class="help-text" id="vfsViewMeta"></p>
    <textarea id="vfsViewContent" rows="10"></textarea>
    <div class="modal-btns">
      <button class="btn-cancel" onclick="closeModal('vfsViewModal')">Close</button>
      <button class="btn-primary" onclick="vfsSaveEdit()">Save changes</button>
    </div>
  </div>
</div>

<!-- VFS new file modal -->
<div class="modal-overlay" id="vfsNewModal">
  <div class="modal">
    <h3>New Virtual File</h3>
    <p class="help-text">Create a file the pseudocode can OPENFILE/READFILE/WRITEFILE. Pre-populate with content if desired.</p>
    <input type="text" id="vfsNewName" placeholder="filename.txt" />
    <textarea id="vfsNewContent" rows="5" placeholder="Initial file contents (optional)..."></textarea>
    <div class="modal-btns">
      <button class="btn-cancel" onclick="closeModal('vfsNewModal')">Cancel</button>
      <button class="btn-primary" onclick="vfsConfirmNew()">Create</button>
    </div>
  </div>
</div>

<input type="file" id="fileLoader" accept=".pseudo,.txt" style="display:none" onchange="handleFileLoad(event)" />
<input type="file" id="vfsImporter" accept=".txt,.csv,.dat,.pseudo" style="display:none" onchange="vfsHandleImport(event)" />

<script>
// ─── State ───────────────────────────────────────────────────────────────────
let programs = JSON.parse(localStorage.getItem('pcp_programs') || 'null') || {
  'Hello World': `// Hello World\nOUTPUT "Hello, World!"`,
  'Variables': `DECLARE name : STRING\nDECLARE age : INTEGER\nname ← "Alice"\nage ← 17\nOUTPUT "Name: " & name\nOUTPUT "Age: " & age`,
  'For Loop': `DECLARE i : INTEGER\nFOR i ← 1 TO 10\n    OUTPUT i\nNEXT i`,
  'While Loop': `DECLARE n : INTEGER\nn ← 1\nWHILE n <= 5 DO\n    OUTPUT n * n\n    n ← n + 1\nENDWHILE`,
  'Fibonacci': `DECLARE a : INTEGER\nDECLARE b : INTEGER\nDECLARE temp : INTEGER\nDECLARE i : INTEGER\na ← 0\nb ← 1\nOUTPUT a\nOUTPUT b\nFOR i ← 1 TO 8\n    temp ← a + b\n    a ← b\n    b ← temp\n    OUTPUT b\nNEXT i`,
  'IF ELSE': `DECLARE x : INTEGER\nx ← 42\nIF x > 50 THEN\n    OUTPUT "Big"\nELSE\n    OUTPUT "Small"\nENDIF`,
  'CASE': `DECLARE grade : STRING\ngrade ← "B"\nCASE OF grade\n    "A" : OUTPUT "Excellent"\n    "B" : OUTPUT "Good"\n    "C" : OUTPUT "Pass"\n    OTHERWISE : OUTPUT "Fail"\nENDCASE`,
  'Procedure': `PROCEDURE greet(name : STRING)\n    OUTPUT "Hello, " & name & "!"\nENDPROCEDURE\n\nCALL greet("World")\nCALL greet("Cambridge")`,
  'Function': `FUNCTION square(n : INTEGER) RETURNS INTEGER\n    RETURN n * n\nENDFUNCTION\n\nOUTPUT square(5)\nOUTPUT square(12)`,
  'Array': `DECLARE nums : ARRAY[1:5] OF INTEGER\nDECLARE i : INTEGER\nFOR i ← 1 TO 5\n    nums[i] ← i * i\nNEXT i\nFOR i ← 1 TO 5\n    OUTPUT nums[i]\nNEXT i`,
  'Repeat Until': `DECLARE n : INTEGER\nn ← 1\nREPEAT\n    OUTPUT n\n    n ← n + 1\nUNTIL n > 5`,
  'File I/O': `// File I/O Demo\n// First create a virtual file called "data.txt" in the\n// Virtual Files panel, with some lines of text.\nDECLARE line : STRING\nOPENFILE "data.txt" FOR READ\nWHILE NOT EOF("data.txt") DO\n    READFILE "data.txt", line\n    OUTPUT line\nENDWHILE\nCLOSEFILE "data.txt"`,
  'Write File': `// Write File Demo\nDECLARE i : INTEGER\nOPENFILE "output.txt" FOR WRITE\nFOR i ← 1 TO 5\n    WRITEFILE "output.txt", "Line " & i\nNEXT i\nCLOSEFILE "output.txt"\nOUTPUT "Done writing. Check Virtual Files panel."`,
};

let currentProgram = Object.keys(programs)[0];
let currentTab = 'pseudocode';
let inputResolve = null;
let syllabus = localStorage.getItem('pcp_syllabus') || '2210'; // '2210' or '9618'

// Virtual File System: filename → { lines: string[], mode: null/'READ'/'WRITE'/'APPEND', pos: int }
let vfsFiles = JSON.parse(localStorage.getItem('pcp_vfs') || '{}');
let vfsEditingFile = null; // filename currently open in edit modal

// ─── Init ────────────────────────────────────────────────────────────────────
function savePrograms() {
  localStorage.setItem('pcp_programs', JSON.stringify(programs));
}

function init() {
  renderFileList();
  loadProgramIntoEditor(currentProgram);
  setupLineNumbers();
  setupDivider();
  setupKeyboard();
  document.getElementById('execMode').addEventListener('change', () => {});
  applySyllabus();
  renderVfs();
}

function renderFileList() {
  const list = document.getElementById('fileList');
  list.innerHTML = '';
  for (const name of Object.keys(programs)) {
    const el = document.createElement('div');
    el.className = 'file-item' + (name === currentProgram ? ' active' : '');
    el.innerHTML = `<span class="file-icon">📄</span>${escHtml(name)}`;
    el.onclick = () => { switchProgram(name); };
    list.appendChild(el);
  }
}

function switchProgram(name) {
  // Save current
  programs[currentProgram] = document.getElementById('codeEditor').value;
  savePrograms();
  currentProgram = name;
  renderFileList();
  loadProgramIntoEditor(name);
}

function loadProgramIntoEditor(name) {
  document.getElementById('codeEditor').value = programs[name] || '';
  updateLineNumbers();
}

// ─── Line numbers + breakpoints ───────────────────────────────────────────────
let breakpoints = new Set(); // 1-based line numbers

function setupLineNumbers() {
  const editor = document.getElementById('codeEditor');
  editor.addEventListener('input', () => {
    updateLineNumbers();
    autosave();
    if (document.getElementById('execMode').value === 'live') runCode();
  });
  editor.addEventListener('scroll', syncLineNumbers);
  editor.addEventListener('keydown', handleEditorKey);
  const nums = document.getElementById('lineNums');
  nums.addEventListener('click', e => {
    const row = e.target.closest('.ln-row');
    if (!row) return;
    const n = parseInt(row.dataset.line);
    if (breakpoints.has(n)) breakpoints.delete(n); else breakpoints.add(n);
    updateLineNumbers();
  });
  updateLineNumbers();
}

function updateLineNumbers() {
  const editor = document.getElementById('codeEditor');
  const count = editor.value.split('\n').length;
  const nums = document.getElementById('lineNums');
  let html = '';
  for (let i = 1; i <= count; i++) {
    let cls = 'ln-row';
    if (breakpoints.has(i)) cls += ' bp';
    if (debugCurrentLine === i) cls += ' current-line';
    html += `<span class="${cls}" data-line="${i}">${i}</span>`;
  }
  nums.innerHTML = html;
  syncLineNumbers();
}

function syncLineNumbers() {
  const editor = document.getElementById('codeEditor');
  document.getElementById('lineNums').scrollTop = editor.scrollTop;
}

// ─── Variable Watch ───────────────────────────────────────────────────────────
let watchPrevSnap = {};

function toggleWatchPanel() {
  const h = document.getElementById('watchHeader');
  const b = document.getElementById('watchBody');
  h.classList.toggle('open');
  b.classList.toggle('open');
}

function renderWatch(env) {
  const body = document.getElementById('watchBody');
  const countEl = document.getElementById('watchVarCount');
  if (!env) {
    body.innerHTML = '<div class="wv-empty">Run or debug your code to see variables here.</div>';
    countEl.textContent = '';
    watchPrevSnap = {};
    return;
  }

  const rows = [];

  // Scalar vars
  for (const [name, val] of Object.entries(env.vars)) {
    rows.push({ name, val, kind: 'var' });
  }
  // Arrays
  for (const [name, arr] of Object.entries(env.arrays || {})) {
    const preview = arr.data.slice(0, 8).map((v,i) =>
      `[${arr.lo+i}]:${v===undefined?'…':v}`).join(', ') + (arr.data.length > 8 ? ', …' : '');
    rows.push({ name, val: preview, kind: 'array', lo: arr.lo, hi: arr.hi });
  }

  countEl.textContent = rows.length ? `(${rows.length})` : '';

  if (!rows.length) {
    body.innerHTML = '<div class="wv-empty">No variables declared yet.</div>';
    watchPrevSnap = {};
    return;
  }

  let html = '<table class="watch-table"><thead><tr><th>Name</th><th>Type</th><th>Value</th></tr></thead><tbody>';
  for (const r of rows) {
    const changed = watchPrevSnap[r.name] !== undefined && String(watchPrevSnap[r.name]) !== String(r.val);
    const changedCls = changed ? ' class="changed"' : '';
    const type = r.kind === 'array' ? `ARRAY[${r.lo}:${r.hi}]` : inferType(r.val);
    let valCls = 'wv-val';
    if (r.val === undefined) valCls += ' undef';
    else if (r.val === true) valCls += ' bool-true';
    else if (r.val === false) valCls += ' bool-false';
    const dispVal = r.val === undefined ? 'undefined' : String(r.val);
    html += `<tr${changedCls}><td class="wv-name">${escHtml(r.name)}</td><td class="wv-type">${type}</td><td class="${valCls}">${escHtml(dispVal)}</td></tr>`;
  }
  html += '</tbody></table>';

  // Call stack
  if (env.callStack && env.callStack.length) {
    html += `<div class="watch-stack"><strong>Call stack:</strong> ${env.callStack.map(escHtml).join(' → ')}</div>`;
  }

  body.innerHTML = html;

  // Update prev snap
  watchPrevSnap = {};
  for (const r of rows) watchPrevSnap[r.name] = r.val;
}

function inferType(val) {
  if (val === undefined) return '—';
  if (val === true || val === false) return 'BOOLEAN';
  if (typeof val === 'number') return Number.isInteger(val) ? 'INTEGER' : 'REAL';
  if (typeof val === 'string' && val.length === 1) return 'CHAR';
  return 'STRING';
}

// ─── Debugger ─────────────────────────────────────────────────────────────────
let debugMode = false;
let debugCurrentLine = -1;
let debugResolve = null;   // called by Step/Continue
let debugStopped = false;
let debugEnvRef = null;

function startDebug() {
  if (debugMode) return;
  autosave();
  clearOutput();
  vfsReset();
  watchPrevSnap = {};
  renderWatch(null);
  debugMode = true;
  debugStopped = false;
  debugCurrentLine = -1;
  document.getElementById('debugBar').classList.add('active');
  document.getElementById('debugStartBtn').disabled = true;
  setStatus('🐞 Debugging…', 'ok');
  document.getElementById('outputStatus').textContent = 'Debugging';

  const code = document.getElementById('codeEditor').value;
  const warns = checkSyllabusViolations(code);
  warns.forEach(w => addOutput('⚠ Syllabus warning: ' + w, 'sys'));

  interpretDebug(code).then(() => {
    if (!debugStopped) {
      addOutput('// Debug complete', 'sys');
      setStatus('✅ Done', 'ok');
    }
    endDebug();
  }).catch(e => {
    addOutput('ERROR: ' + e.message, 'err');
    setStatus('❌ Error', 'err');
    endDebug();
  });
}

function endDebug() {
  debugMode = false;
  debugCurrentLine = -1;
  debugResolve = null;
  document.getElementById('debugBar').classList.remove('active');
  document.getElementById('debugStartBtn').disabled = false;
  document.getElementById('dbgLineNum').textContent = '—';
  document.getElementById('dbgLineSrc').textContent = '';
  document.getElementById('outputStatus').textContent = 'Done';
  updateLineNumbers();
}

function debugStep() {
  if (debugResolve) { const r = debugResolve; debugResolve = null; r('step'); }
}

function debugContinue() {
  if (debugResolve) { const r = debugResolve; debugResolve = null; r('continue'); }
}

function debugStop() {
  debugStopped = true;
  if (debugResolve) { const r = debugResolve; debugResolve = null; r('stop'); }
  addOutput('// Stopped by user', 'sys');
  setStatus('⏹ Stopped', 'err');
}

// Pauses at line n, updates UI, waits for user action
async function debugPause(lineIdx, src, env) {
  debugCurrentLine = lineIdx + 1; // 1-based
  document.getElementById('dbgLineNum').textContent = debugCurrentLine;
  document.getElementById('dbgLineSrc').textContent = src.length > 60 ? src.slice(0, 57) + '…' : src;
  updateLineNumbers();
  renderWatch(env);
  // Scroll editor to line
  scrollEditorToLine(lineIdx);

  return new Promise(resolve => {
    debugResolve = resolve;
    // if breakpoint was hit during Continue mode, we've already paused — do nothing extra
  });
}

let debugContinueMode = false; // true = run until next breakpoint

// Patched interpret for debug mode
async function interpretDebug(src) {
  debugContinueMode = false;
  const lines = src.split('\n').map(l => l.trim());
  const env = { vars: {}, funcs: {}, procs: {}, arrays: {}, types: {}, callStack: [] };

  // First pass: collect functions/procedures (same as interpret)
  let i = 0;
  while (i < lines.length) {
    const line = lines[i];
    const fnMatch = line.match(/^FUNCTION\s+(\w+)\s*\(([^)]*)\)\s+RETURNS\s+(\w+)/i);
    const prMatch = line.match(/^PROCEDURE\s+(\w+)\s*\(([^)]*)\)/i);
    if (fnMatch) {
      const name = fnMatch[1], params = parseParams(fnMatch[2]), retType = fnMatch[3];
      const body = []; i++;
      let depth = 1;
      while (i < lines.length && depth > 0) {
        if (/^FUNCTION\b/i.test(lines[i]) || /^PROCEDURE\b/i.test(lines[i])) depth++;
        if (/^ENDFUNCTION\b/i.test(lines[i])) { depth--; if (!depth) break; }
        if (/^ENDPROCEDURE\b/i.test(lines[i])) { depth--; if (!depth) break; }
        body.push(lines[i]); i++;
      }
      env.funcs[name.toUpperCase()] = { params, body, retType };
    } else if (prMatch) {
      const name = prMatch[1], params = parseParams(prMatch[2]);
      const body = []; i++;
      let depth = 1;
      while (i < lines.length && depth > 0) {
        if (/^FUNCTION\b/i.test(lines[i]) || /^PROCEDURE\b/i.test(lines[i])) depth++;
        if (/^ENDFUNCTION\b/i.test(lines[i])) { depth--; if (!depth) break; }
        if (/^ENDPROCEDURE\b/i.test(lines[i])) { depth--; if (!depth) break; }
        body.push(lines[i]); i++;
      }
      env.procs[name.toUpperCase()] = { params, body };
    }
    i++;
  }
  debugEnvRef = env;
  await execLinesDebug(lines, env, 0, lines); // pass original lines for line mapping
}

// line numbers are indices into the *original* top-level lines array
async function execLinesDebug(lines, env, startIdx, originalLines) {
  let i = startIdx;
  while (i < lines.length) {
    if (debugStopped) return;
    const src = lines[i];
    const isTrivial = !src || src.startsWith('//') || src.startsWith('REM') ||
      /^(ENDFUNCTION|ENDPROCEDURE|ENDIF|ENDWHILE|ENDFOR|ENDCASE|ELSE|ELSEIF|NEXT\s|UNTIL|TYPE|ENDTYPE|CLASS|ENDCLASS)\b/i.test(src) ||
      /^(FUNCTION|PROCEDURE)\b/i.test(src);

    if (!isTrivial) {
      const globalLineIdx = originalLines ? originalLines.indexOf(src) : i;
      const pause = debugContinueMode ? breakpoints.has(globalLineIdx + 1) : true;
      if (pause) {
        debugContinueMode = false;
        const action = await debugPause(globalLineIdx >= 0 ? globalLineIdx : i, src, env);
        if (action === 'stop' || debugStopped) return;
        if (action === 'continue') debugContinueMode = true;
      }
    }

    const result = await execLine(lines, i, env);
    renderWatch(env); // update watch after every line
    if (result && result.type === 'return') return result;
    if (result && result.type === 'continue') { i = result.nextIdx; continue; }
    i++;
  }
}

function scrollEditorToLine(lineIdx) {
  const editor = document.getElementById('codeEditor');
  const lineHeight = parseFloat(getComputedStyle(editor).lineHeight) || 22.4;
  const targetScroll = lineIdx * lineHeight - editor.clientHeight / 2;
  editor.scrollTop = Math.max(0, targetScroll);
  syncLineNumbers();
}

function handleEditorKey(e) {
  if (e.key === 'Tab') {
    e.preventDefault();
    const s = e.target.selectionStart, end = e.target.selectionEnd;
    e.target.value = e.target.value.substring(0, s) + '    ' + e.target.value.substring(end);
    e.target.selectionStart = e.target.selectionEnd = s + 4;
    updateLineNumbers();
  }
}

function autosave() {
  programs[currentProgram] = document.getElementById('codeEditor').value;
  savePrograms();
}

// ─── Divider drag ─────────────────────────────────────────────────────────────
function setupDivider() {
  const div = document.getElementById('divider');
  let dragging = false, startX, startW;
  div.addEventListener('mousedown', e => {
    dragging = true;
    startX = e.clientX;
    const pane = document.querySelector('.output-pane');
    startW = pane.offsetWidth;
    document.body.style.userSelect = 'none';
  });
  document.addEventListener('mousemove', e => {
    if (!dragging) return;
    const pane = document.querySelector('.output-pane');
    const delta = startX - e.clientX;
    pane.style.width = Math.max(150, Math.min(window.innerWidth * 0.7, startW + delta)) + 'px';
  });
  document.addEventListener('mouseup', () => { dragging = false; document.body.style.userSelect = ''; });
}

// ─── Keyboard ─────────────────────────────────────────────────────────────────
function setupKeyboard() {
  document.addEventListener('keydown', e => {
    if (e.key === 'F5') { e.preventDefault(); runCode(); }
    if (e.key === 'F5' || (e.ctrlKey && e.key === 'Enter')) { e.preventDefault(); runCode(); }
    if (e.key === 'F6') { e.preventDefault(); startDebug(); }
    if (e.key === 'F10' && debugMode) { e.preventDefault(); debugStep(); }
    if (e.key === 'F8'  && debugMode) { e.preventDefault(); debugContinue(); }
  });
  document.getElementById('inputField').addEventListener('keydown', e => {
    if (e.key === 'Enter') submitInput();
  });
}

// ─── Tabs ─────────────────────────────────────────────────────────────────────
function switchTab(tab) {
  currentTab = tab;
  document.querySelectorAll('.tab-btn').forEach((b, i) => {
    b.classList.toggle('active', ['pseudocode','python','vb'][i] === tab);
  });
  if (tab !== 'pseudocode') {
    const code = document.getElementById('codeEditor').value;
    if (tab === 'python') showConverted(toPython(code), 'Python');
    if (tab === 'vb') showConverted(toVB(code), 'VB.NET (Console)');
  }
}

function showConverted(code, lang) {
  clearOutput();
  addOutput(`// Converted to ${lang} (approximate)`, 'sys');
  addOutput('// ─────────────────────────────', 'sys');
  code.split('\n').forEach(l => addOutput(l, 'out'));
}

// ─── File operations ──────────────────────────────────────────────────────────
function newProgram() {
  document.getElementById('newFileName').value = '';
  openModal('newFileModal');
  setTimeout(() => document.getElementById('newFileName').focus(), 100);
}

function confirmNewProgram() {
  const name = document.getElementById('newFileName').value.trim();
  if (!name) return;
  programs[name] = `// ${name}\n`;
  savePrograms();
  closeModal('newFileModal');
  switchProgram(name);
  renderFileList();
}

function deleteProgram() {
  if (Object.keys(programs).length <= 1) return alert('Cannot delete last program.');
  if (!confirm(`Delete "${currentProgram}"?`)) return;
  delete programs[currentProgram];
  savePrograms();
  currentProgram = Object.keys(programs)[0];
  renderFileList();
  loadProgramIntoEditor(currentProgram);
}

function saveFile() {
  autosave();
  setStatus('💾 Saved', 'ok');
  setTimeout(() => setStatus('✅ No errors', 'ok'), 1200);
}

function loadFile() {
  document.getElementById('fileLoader').click();
}

function handleFileLoad(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    const name = file.name.replace(/\.(pseudo|txt)$/, '');
    programs[name] = ev.target.result;
    savePrograms();
    switchProgram(name);
    renderFileList();
  };
  reader.readAsText(file);
  e.target.value = '';
}

function downloadFile() {
  autosave();
  const blob = new Blob([programs[currentProgram]], {type: 'text/plain'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = currentProgram + '.pseudo';
  a.click();
}

// ─── Syllabus Toggle ──────────────────────────────────────────────────────────
function toggleSyllabus() {
  syllabus = syllabus === '2210' ? '9618' : '2210';
  localStorage.setItem('pcp_syllabus', syllabus);
  applySyllabus();
}

function applySyllabus() {
  document.getElementById('syl2210').classList.toggle('active', syllabus === '2210');
  document.getElementById('syl9618').classList.toggle('active', syllabus === '9618');
  // Update placeholder hint
  const editor = document.getElementById('codeEditor');
  if (syllabus === '9618') {
    editor.placeholder = `// CIE A-Level 9618 Pseudocode\n// Supports: OOP, Pointers, ADTs, Recursion, File I/O\nDECLARE x : INTEGER\nx ← 42\nOUTPUT x`;
  } else {
    editor.placeholder = `// CIE IGCSE/O-Level 2210 Pseudocode\n// Supports: Variables, Arrays, Loops, Functions, File I/O\nDECLARE x : INTEGER\nx ← 42\nOUTPUT x`;
  }
  // Show/hide 9618-only demos note
  updateSyllabusWarnings();
}

function updateSyllabusWarnings() {
  // Called after run to warn about out-of-syllabus constructs
  // Lightweight: just update the badge tooltip
  const badge = document.getElementById('statusBadge');
  const syl = syllabus === '2210' ? '2210' : '9618';
  badge.title = `Syllabus: CIE ${syl}`;
}

function checkSyllabusViolations(code) {
  const warnings = [];
  if (syllabus === '2210') {
    // 9618-only features not in 2210
    if (/\bNEW\b/i.test(code))         warnings.push('NEW (OOP) is A-Level 9618 only');
    if (/\bINHERITS\b/i.test(code))     warnings.push('INHERITS is A-Level 9618 only');
    if (/\b\^[\w]+\b/.test(code))       warnings.push('Pointer syntax (^) is A-Level 9618 only');
    if (/\bSET\b.*\{/i.test(code))      warnings.push('SET ADT is A-Level 9618 only');
  }
  return warnings;
}

// ─── Virtual File System ──────────────────────────────────────────────────────
function saveVfs() {
  localStorage.setItem('pcp_vfs', JSON.stringify(vfsFiles));
}

function renderVfs() {
  const body = document.getElementById('vfsBody');
  const count = document.getElementById('vfsCount');
  const names = Object.keys(vfsFiles);
  count.textContent = names.length ? `(${names.length})` : '';
  body.innerHTML = '';
  if (!names.length) {
    body.innerHTML = '<span class="vfs-empty">No virtual files yet. Use OPENFILE in pseudocode or create one manually.</span>';
    return;
  }
  names.forEach(name => {
    const f = vfsFiles[name];
    const lines = f.lines.length;
    const chip = document.createElement('div');
    chip.className = 'vfs-file-chip';
    chip.innerHTML = `
      <span>📄</span>
      <span style="color:var(--text);font-weight:600">${escHtml(name)}</span>
      <span style="font-size:0.65rem">${lines} line${lines!==1?'s':''}</span>
      <span class="vfs-view" onclick="vfsViewFile('${escHtml(name)}')" title="View/Edit">✏️</span>
      <span class="vfs-view" onclick="vfsDownload('${escHtml(name)}')" title="Download">⬇</span>
      <span class="vfs-del" onclick="vfsDelete('${escHtml(name)}')" title="Delete">✕</span>`;
    body.appendChild(chip);
  });
}

function toggleVfsPanel() {
  const header = document.getElementById('vfsHeader');
  const body = document.getElementById('vfsBody');
  header.classList.toggle('open');
  body.classList.toggle('open');
}

function vfsNewFile() {
  document.getElementById('vfsNewName').value = '';
  document.getElementById('vfsNewContent').value = '';
  openModal('vfsNewModal');
  setTimeout(() => document.getElementById('vfsNewName').focus(), 100);
}

function vfsConfirmNew() {
  const name = document.getElementById('vfsNewName').value.trim();
  if (!name) return;
  const content = document.getElementById('vfsNewContent').value;
  vfsFiles[name] = { lines: content ? content.split('\n') : [] };
  saveVfs();
  closeModal('vfsNewModal');
  renderVfs();
  // Auto-open panel
  const body = document.getElementById('vfsBody');
  const header = document.getElementById('vfsHeader');
  if (!body.classList.contains('open')) { body.classList.add('open'); header.classList.add('open'); }
}

function vfsImportFile() {
  document.getElementById('vfsImporter').click();
}

function vfsHandleImport(e) {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = ev => {
    vfsFiles[file.name] = { lines: ev.target.result.split('\n') };
    saveVfs();
    renderVfs();
    const body = document.getElementById('vfsBody');
    const header = document.getElementById('vfsHeader');
    if (!body.classList.contains('open')) { body.classList.add('open'); header.classList.add('open'); }
  };
  reader.readAsText(file);
  e.target.value = '';
}

function vfsViewFile(name) {
  vfsEditingFile = name;
  document.getElementById('vfsViewTitle').textContent = `File: ${name}`;
  const f = vfsFiles[name];
  document.getElementById('vfsViewMeta').textContent = `${f.lines.length} line(s) · mode: ${f.mode || 'closed'}`;
  document.getElementById('vfsViewContent').value = f.lines.join('\n');
  openModal('vfsViewModal');
}

function vfsSaveEdit() {
  if (!vfsEditingFile) return;
  const content = document.getElementById('vfsViewContent').value;
  vfsFiles[vfsEditingFile].lines = content.split('\n');
  saveVfs();
  closeModal('vfsViewModal');
  renderVfs();
}

function vfsDelete(name) {
  if (!confirm(`Delete virtual file "${name}"?`)) return;
  delete vfsFiles[name];
  saveVfs();
  renderVfs();
}

function vfsDownload(name) {
  const content = vfsFiles[name].lines.join('\n');
  const blob = new Blob([content], { type: 'text/plain' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = name;
  a.click();
}

// Runtime VFS handle table (per execution, not persisted)
let vfsHandles = {}; // varName → { filename, mode, pos }

function vfsReset() { vfsHandles = {}; }

// ─── Output helpers ───────────────────────────────────────────────────────────
function addOutput(text, type='out') {
  const body = document.getElementById('outputBody');
  const el = document.createElement('div');
  el.className = 'output-line ' + type;
  el.textContent = text;
  body.appendChild(el);
  body.scrollTop = body.scrollHeight;
}

function clearOutput() {
  document.getElementById('outputBody').innerHTML = '';
  renderWatch(null);
}

function setStatus(msg, type='ok') {
  const badge = document.getElementById('statusBadge');
  badge.textContent = msg;
  badge.className = 'status-indicator ' + (type === 'ok' ? 'status-ok' : 'status-err');
}

// ─── Format code ──────────────────────────────────────────────────────────────
function formatCode() {
  const editor = document.getElementById('codeEditor');
  const lines = editor.value.split('\n');
  let indent = 0;
  const keywords_open = /^(IF|ELSE|ELSEIF|FOR|WHILE|REPEAT|PROCEDURE|FUNCTION|TYPE|CLASS|CASE\s+OF)/i;
  const keywords_close = /^(ENDIF|ENDWHILE|ENDFOR|NEXT|UNTIL|ENDPROCEDURE|ENDFUNCTION|ENDTYPE|ENDCLASS|ENDCASE)/i;
  const keywords_mid = /^(ELSE|ELSEIF|OTHERWISE)/i;
  const result = lines.map(line => {
    const trimmed = line.trim();
    if (!trimmed) return '';
    if (keywords_close.test(trimmed) || keywords_mid.test(trimmed)) indent = Math.max(0, indent - 1);
    const formatted = '    '.repeat(indent) + trimmed;
    if (keywords_open.test(trimmed) && !trimmed.match(/^(IF.*THEN\s*OUTPUT|WHILE.*DO\s*\S)/i)) indent++;
    if (keywords_mid.test(trimmed)) indent++;
    return formatted;
  });
  editor.value = result.join('\n');
  updateLineNumbers();
  autosave();
}

// ─── Pseudocode Interpreter ───────────────────────────────────────────────────
async function runCode() {
  autosave();
  clearOutput();
  vfsReset();
  setStatus('⏳ Running…', 'ok');
  document.getElementById('outputStatus').textContent = 'Running…';
  const code = document.getElementById('codeEditor').value;

  // Syllabus warnings (non-fatal)
  const warns = checkSyllabusViolations(code);
  warns.forEach(w => addOutput('⚠ Syllabus warning: ' + w, 'sys'));

  try {
    await interpret(code);
    // Flush any open WRITE files back to VFS
    for (const [, h] of Object.entries(vfsHandles)) {
      if ((h.mode === 'WRITE' || h.mode === 'APPEND') && vfsFiles[h.filename]) {
        saveVfs(); renderVfs();
      }
    }
    setStatus('✅ No errors', 'ok');
    document.getElementById('outputStatus').textContent = 'Done';
    updateSyllabusWarnings();
  } catch(e) {
    addOutput('ERROR: ' + e.message, 'err');
    setStatus('❌ Error', 'err');
    document.getElementById('outputStatus').textContent = 'Error';
  }
}

// ─── Core Interpreter ─────────────────────────────────────────────────────────
async function interpret(src) {
  const lines = src.split('\n').map(l => l.trim());
  const env = { vars: {}, funcs: {}, procs: {}, arrays: {}, types: {}, callStack: [] };

  // First pass: collect function & procedure definitions
  let i = 0;
  while (i < lines.length) {
    const line = lines[i];
    const fnMatch = line.match(/^FUNCTION\s+(\w+)\s*\(([^)]*)\)\s+RETURNS\s+(\w+)/i);
    const prMatch = line.match(/^PROCEDURE\s+(\w+)\s*\(([^)]*)\)/i);
    if (fnMatch) {
      const name = fnMatch[1], params = parseParams(fnMatch[2]), retType = fnMatch[3];
      const body = [];
      i++;
      let depth = 1;
      while (i < lines.length && depth > 0) {
        if (/^FUNCTION\b/i.test(lines[i]) || /^PROCEDURE\b/i.test(lines[i])) depth++;
        if (/^ENDFUNCTION\b/i.test(lines[i])) { depth--; if (depth===0) break; }
        if (/^ENDPROCEDURE\b/i.test(lines[i])) { depth--; if (depth===0) break; }
        body.push(lines[i]);
        i++;
      }
      env.funcs[name.toUpperCase()] = { params, body, retType };
    } else if (prMatch) {
      const name = prMatch[1], params = parseParams(prMatch[2]);
      const body = [];
      i++;
      let depth = 1;
      while (i < lines.length && depth > 0) {
        if (/^FUNCTION\b/i.test(lines[i]) || /^PROCEDURE\b/i.test(lines[i])) depth++;
        if (/^ENDFUNCTION\b/i.test(lines[i])) { depth--; if (depth===0) break; }
        if (/^ENDPROCEDURE\b/i.test(lines[i])) { depth--; if (depth===0) break; }
        body.push(lines[i]);
        i++;
      }
      env.procs[name.toUpperCase()] = { params, body };
    }
    i++;
  }

  await execLines(lines, env);
  renderWatch(env); // show final state after normal run
}

function parseParams(paramStr) {
  if (!paramStr.trim()) return [];
  return paramStr.split(',').map(p => {
    const parts = p.trim().split(':');
    return { name: parts[0]?.trim(), type: parts[1]?.trim() };
  }).filter(p => p.name);
}

async function execLines(lines, env, startIdx=0) {
  let i = startIdx;
  while (i < lines.length) {
    const result = await execLine(lines, i, env);
    if (result && result.type === 'return') return result;
    if (result && result.type === 'continue') { i = result.nextIdx; continue; }
    i++;
  }
}

async function execLine(lines, idx, env) {
  const line = lines[idx];
  if (!line || line.startsWith('//') || line.startsWith('REM')) return null;

  // DECLARE
  if (/^DECLARE\s/i.test(line)) {
    const m = line.match(/^DECLARE\s+(\w+)\s*:\s*(.+)/i);
    if (m) {
      const name = m[1], typeInfo = m[2].trim();
      const arrMatch = typeInfo.match(/ARRAY\[(-?\d+):(-?\d+)\]\s+OF\s+(\w+)/i);
      if (arrMatch) {
        const lo = parseInt(arrMatch[1]), hi = parseInt(arrMatch[2]);
        env.arrays[name.toUpperCase()] = { lo, hi, data: new Array(hi - lo + 1).fill(undefined) };
      } else {
        if (!(name.toUpperCase() in env.vars)) env.vars[name.toUpperCase()] = defaultVal(typeInfo);
      }
    }
    return null;
  }

  // CONSTANT
  if (/^CONSTANT\s/i.test(line)) {
    const m = line.match(/^CONSTANT\s+(\w+)\s*[=←←]\s*(.+)/i);
    if (m) env.vars[m[1].toUpperCase()] = evalExpr(m[2].trim(), env);
    return null;
  }

  // ASSIGN (←, <-, =)
  const assignArr = line.match(/^(\w+)\[(.+?)\]\s*(?:←|←|<-|<--|←-)\s*(.+)/i);
  const assignSimple = line.match(/^(\w+)\s*(?:←|←|<-|<--|←-)\s*(.+)/i);
  if (assignArr) {
    const name = assignArr[1].toUpperCase();
    const idx2 = Math.round(evalExpr(assignArr[2], env));
    const val = evalExpr(assignArr[3], env);
    if (env.arrays[name]) {
      env.arrays[name].data[idx2 - env.arrays[name].lo] = val;
    }
    return null;
  }
  if (assignSimple) {
    const name = assignSimple[1].toUpperCase();
    const val = evalExpr(assignSimple[2], env);
    env.vars[name] = val;
    return null;
  }

  // OUTPUT / PRINT
  if (/^(OUTPUT|PRINT)\s/i.test(line)) {
    const expr = line.replace(/^(OUTPUT|PRINT)\s+/i, '');
    const val = evalExpr(expr, env);
    addOutput(String(val));
    return null;
  }

  // INPUT
  if (/^INPUT\s/i.test(line)) {
    const m = line.match(/^INPUT\s+(\w+)/i);
    if (m) {
      const val = await getInput(`INPUT ${m[1]}:`);
      const name = m[1].toUpperCase();
      if (isNaN(val) || val.trim()==='') env.vars[name] = val;
      else env.vars[name] = val.includes('.') ? parseFloat(val) : parseInt(val);
    }
    return null;
  }

  // IF
  if (/^IF\s.+THEN$/i.test(line)) {
    const cond = line.replace(/^IF\s+/i, '').replace(/\s+THEN$/i, '');
    const ifLines = [], elseLines = [];
    let j = idx + 1, depth = 1, inElse = false;
    while (j < lines.length && depth > 0) {
      const l = lines[j].trim();
      if (/^(IF|WHILE|FOR|REPEAT|CASE)/i.test(l)) depth++;
      if (/^(ENDIF|ENDWHILE|ENDFOR|NEXT\s|UNTIL|ENDCASE)/i.test(l)) depth--;
      if (depth === 1 && /^ELSE$/i.test(l)) { inElse = true; j++; continue; }
      if (depth === 1 && /^ELSEIF\s/i.test(l)) {
        // treat remainder as nested IF
        const rest = [l.replace(/^ELSEIF\s/i, 'IF '), ...lines.slice(j+1)];
        if (!inElse) { if (!evalCond(cond, env)) { inElse = true; } }
        if (inElse) { elseLines.push(...rest); break; }
        j++;
        continue;
      }
      if (depth === 0) break;
      (inElse ? elseLines : ifLines).push(l);
      j++;
    }
    const res = evalCond(cond, env)
      ? await execLines(ifLines, env)
      : await execLines(elseLines, env);
    if (res && res.type === 'return') return res;
    return { type: 'continue', nextIdx: j };
  }

  // FOR
  const forMatch = line.match(/^FOR\s+(\w+)\s*(?:←|←|<-|<--|←-)\s*(.+?)\s+TO\s+(.+?)(?:\s+STEP\s+(.+))?$/i);
  if (forMatch) {
    const varName = forMatch[1].toUpperCase();
    let start = evalExpr(forMatch[2], env);
    const end = evalExpr(forMatch[3], env);
    const step = forMatch[4] ? evalExpr(forMatch[4], env) : 1;
    const body = [];
    let j = idx + 1, depth = 1;
    while (j < lines.length && depth > 0) {
      const l = lines[j].trim();
      if (/^(IF|WHILE|FOR|REPEAT|CASE)/i.test(l)) depth++;
      if (/^(ENDIF|ENDWHILE|ENDFOR|NEXT\s|UNTIL|ENDCASE)/i.test(l)) { depth--; if (depth===0) break; }
      if (/^NEXT\s/i.test(l) && depth===1) { break; }
      body.push(l);
      j++;
    }
    let guard = 0;
    for (let v = start; step > 0 ? v <= end : v >= end; v += step) {
      if (++guard > 100000) throw new Error('Loop limit exceeded');
      env.vars[varName] = v;
      const res = await execLines(body, env);
      if (res && res.type === 'return') return res;
    }
    return { type: 'continue', nextIdx: j + 1 };
  }

  // WHILE
  if (/^WHILE\s.+\s+DO$/i.test(line)) {
    const cond = line.replace(/^WHILE\s+/i, '').replace(/\s+DO$/i, '');
    const body = [];
    let j = idx + 1, depth = 1;
    while (j < lines.length && depth > 0) {
      const l = lines[j].trim();
      if (/^(IF|WHILE|FOR|REPEAT|CASE)/i.test(l)) depth++;
      if (/^(ENDIF|ENDWHILE|ENDFOR|NEXT\s|UNTIL|ENDCASE)/i.test(l)) { depth--; if (depth===0) break; }
      body.push(l);
      j++;
    }
    let guard = 0;
    while (evalCond(cond, env)) {
      if (++guard > 100000) throw new Error('Loop limit exceeded');
      const res = await execLines(body, env);
      if (res && res.type === 'return') return res;
    }
    return { type: 'continue', nextIdx: j + 1 };
  }

  // REPEAT...UNTIL
  if (/^REPEAT$/i.test(line)) {
    const body = [];
    let j = idx + 1;
    while (j < lines.length && !/^UNTIL\s/i.test(lines[j].trim())) {
      body.push(lines[j].trim());
      j++;
    }
    const untilCond = lines[j]?.trim().replace(/^UNTIL\s+/i, '');
    let guard = 0;
    do {
      if (++guard > 100000) throw new Error('Loop limit exceeded');
      const res = await execLines(body, env);
      if (res && res.type === 'return') return res;
    } while (!evalCond(untilCond, env));
    return { type: 'continue', nextIdx: j + 1 };
  }

  // CASE OF
  if (/^CASE\s+OF\s+/i.test(line)) {
    const varExpr = line.replace(/^CASE\s+OF\s+/i, '').trim();
    const val = evalExpr(varExpr, env);
    const cases = {};
    let otherwise = null;
    let j = idx + 1, depth = 1;
    while (j < lines.length && depth > 0) {
      const l = lines[j].trim();
      if (/^CASE\s+OF/i.test(l)) depth++;
      if (/^ENDCASE$/i.test(l)) { depth--; if (depth===0) break; }
      if (depth===1) {
        const caseM = l.match(/^(.+?)\s*:\s*(.+)$/);
        if (caseM) {
          if (/^OTHERWISE$/i.test(caseM[1].trim())) otherwise = caseM[2].trim();
          else cases[caseM[1].trim()] = caseM[2].trim();
        }
      }
      j++;
    }
    const key = Object.keys(cases).find(k => String(evalExpr(k, env)) === String(val));
    const chosen = key ? cases[key] : otherwise;
    if (chosen) await execLines([chosen], env);
    return { type: 'continue', nextIdx: j + 1 };
  }

  // ── File I/O ─────────────────────────────────────────────────────────────
  // OPENFILE <filename> FOR READ|WRITE|APPEND
  const openFile = line.match(/^OPENFILE\s+(.+?)\s+FOR\s+(READ|WRITE|APPEND)/i);
  if (openFile) {
    const filename = String(evalExpr(openFile[1].trim(), env));
    const mode = openFile[2].toUpperCase();
    if (!vfsFiles[filename]) {
      if (mode === 'READ') throw new Error(`File not found: "${filename}"`);
      vfsFiles[filename] = { lines: [] };
    }
    if (mode === 'WRITE') vfsFiles[filename].lines = []; // truncate
    vfsHandles[filename] = { filename, mode, pos: 0 };
    saveVfs(); renderVfs();
    return null;
  }

  // CLOSEFILE <filename>
  const closeFile = line.match(/^CLOSEFILE\s+(.+)/i);
  if (closeFile) {
    const filename = String(evalExpr(closeFile[1].trim(), env));
    if (vfsHandles[filename]) {
      delete vfsHandles[filename];
      saveVfs(); renderVfs();
    }
    return null;
  }

  // READFILE <filename>, <variable>
  const readFile = line.match(/^READFILE\s+(.+?)\s*,\s*(\w+)/i);
  if (readFile) {
    const filename = String(evalExpr(readFile[1].trim(), env));
    const varName = readFile[2].toUpperCase();
    const handle = vfsHandles[filename];
    if (!handle) throw new Error(`File "${filename}" is not open`);
    if (handle.mode !== 'READ') throw new Error(`File "${filename}" not open for reading`);
    const f = vfsFiles[filename];
    if (handle.pos >= f.lines.length) throw new Error(`EOF reached on "${filename}"`);
    env.vars[varName] = f.lines[handle.pos++];
    return null;
  }

  // WRITEFILE <filename>, <expression>
  const writeFile = line.match(/^WRITEFILE\s+(.+?)\s*,\s*(.+)/i);
  if (writeFile) {
    const filename = String(evalExpr(writeFile[1].trim(), env));
    const val = String(evalExpr(writeFile[2].trim(), env));
    const handle = vfsHandles[filename];
    if (!handle) throw new Error(`File "${filename}" is not open`);
    if (handle.mode !== 'WRITE' && handle.mode !== 'APPEND') throw new Error(`File "${filename}" not open for writing`);
    vfsFiles[filename].lines.push(val);
    saveVfs(); renderVfs();
    return null;
  }

  // CALL procedure
  if (/^CALL\s+/i.test(line)) {
    const m = line.match(/^CALL\s+(\w+)\s*(?:\(([^)]*)\))?/i);
    if (m) await callProc(m[1], m[2] || '', env);
    return null;
  }

  // RETURN
  if (/^RETURN\s/i.test(line)) {
    const val = evalExpr(line.replace(/^RETURN\s+/i, ''), env);
    return { type: 'return', value: val };
  }

  // Skip definition lines
  if (/^(FUNCTION|PROCEDURE|ENDFUNCTION|ENDPROCEDURE|NEXT\s|ENDIF|ENDWHILE|ENDFOR|ENDCASE|ELSE|ELSEIF|TYPE|ENDTYPE|CLASS|ENDCLASS)\b/i.test(line)) return null;

  // Try as expression (procedure call without CALL)
  const callNoKeyword = line.match(/^(\w+)\s*\(([^)]*)\)\s*$/);
  if (callNoKeyword) {
    const name = callNoKeyword[1].toUpperCase();
    if (env.procs[name]) { await callProc(callNoKeyword[1], callNoKeyword[2], env); return null; }
    if (env.funcs[name]) { await callFunc(callNoKeyword[1], callNoKeyword[2], env); return null; }
  }

  return null;
}

async function callProc(name, argsStr, env) {
  const upName = name.toUpperCase();
  const proc = env.procs[upName];
  if (!proc) throw new Error(`Unknown procedure: ${name}`);
  const args = parseArgList(argsStr, env);
  const localEnv = { vars: { ...env.vars }, funcs: env.funcs, procs: env.procs, arrays: { ...env.arrays }, callStack: [...env.callStack, name] };
  if (proc.params) proc.params.forEach((p, i) => { localEnv.vars[p.name.toUpperCase()] = args[i] ?? undefined; });
  await execLines(proc.body, localEnv);
  // BYREF: write back
  if (proc.params) proc.params.forEach((p, i) => { if (i < args.length) env.vars[p.name.toUpperCase()] = localEnv.vars[p.name.toUpperCase()]; });
}

async function callFunc(name, argsStr, env) {
  const upName = name.toUpperCase();
  const fn = env.funcs[upName];
  if (!fn) throw new Error(`Unknown function: ${name}`);
  const args = parseArgList(argsStr, env);
  const localEnv = { vars: { ...env.vars }, funcs: env.funcs, procs: env.procs, arrays: { ...env.arrays }, callStack: [...env.callStack, name] };
  if (fn.params) fn.params.forEach((p, i) => { localEnv.vars[p.name.toUpperCase()] = args[i] ?? undefined; });
  const res = await execLines(fn.body, localEnv);
  return (res && res.type === 'return') ? res.value : undefined;
}

function parseArgList(argsStr, env) {
  if (!argsStr.trim()) return [];
  return argsStr.split(',').map(a => evalExpr(a.trim(), env));
}

function defaultVal(type) {
  const t = type.toUpperCase();
  if (t === 'INTEGER' || t === 'REAL') return 0;
  if (t === 'BOOLEAN') return false;
  return '';
}

function evalCond(expr, env) {
  return !!evalExpr(expr, env);
}

function evalExpr(expr, env) {
  if (!expr) return '';
  expr = expr.trim();

  // String literal
  if (/^".*"$/.test(expr)) return expr.slice(1, -1);
  // Char literal
  if (/^'.'$/.test(expr)) return expr[1];
  // TRUE/FALSE
  if (/^TRUE$/i.test(expr)) return true;
  if (/^FALSE$/i.test(expr)) return false;

  // Concatenation with &
  if (hasBinaryOp(expr, '&')) {
    const [l, r] = splitBinary(expr, '&');
    return String(evalExpr(l, env)) + String(evalExpr(r, env));
  }

  // Boolean OR / AND
  if (hasBinaryOpWord(expr, 'OR')) {
    const [l, r] = splitBinaryWord(expr, 'OR');
    return evalExpr(l, env) || evalExpr(r, env);
  }
  if (hasBinaryOpWord(expr, 'AND')) {
    const [l, r] = splitBinaryWord(expr, 'AND');
    return evalExpr(l, env) && evalExpr(r, env);
  }
  if (/^NOT\s+/i.test(expr)) {
    return !evalExpr(expr.replace(/^NOT\s+/i, ''), env);
  }

  // Comparison: >=, <=, <>, !=, =, <, >
  for (const op of ['>=', '<=', '<>', '!=', '=', '<', '>']) {
    if (hasBinaryOp(expr, op)) {
      const [l, r] = splitBinary(expr, op);
      const lv = evalExpr(l, env), rv = evalExpr(r, env);
      if (op === '=') return lv == rv;
      if (op === '<>') return lv != rv;
      if (op === '!=') return lv != rv;
      if (op === '>') return lv > rv;
      if (op === '<') return lv < rv;
      if (op === '>=') return lv >= rv;
      if (op === '<=') return lv <= rv;
    }
  }

  // +, - (left to right)
  for (const op of ['+', '-']) {
    if (hasBinaryOp(expr, op)) {
      const [l, r] = splitBinary(expr, op);
      const lv = evalExpr(l, env), rv = evalExpr(r, env);
      if (op === '+') return (typeof lv === 'number' && typeof rv === 'number') ? lv + rv : String(lv) + String(rv);
      if (op === '-') return lv - rv;
    }
  }

  // *, /, MOD, DIV
  for (const op of ['*', '/', 'MOD', 'DIV']) {
    if (hasBinaryOp(expr, op)) {
      const [l, r] = splitBinary(expr, op);
      const lv = evalExpr(l, env), rv = evalExpr(r, env);
      if (op === '*') return lv * rv;
      if (op === '/') return lv / rv;
      if (op === 'MOD') return lv % rv;
      if (op === 'DIV') return Math.trunc(lv / rv);
    }
  }

  // Unary minus
  if (/^-/.test(expr)) return -evalExpr(expr.slice(1), env);

  // Parentheses
  if (/^\(.*\)$/.test(expr)) {
    if (matchingParen(expr, 0) === expr.length - 1) return evalExpr(expr.slice(1, -1), env);
  }

  // Built-in functions
  const fnCall = expr.match(/^(\w+)\s*\(([^)]*)\)$/);
  if (fnCall) {
    const fname = fnCall[1].toUpperCase(), argStr = fnCall[2];
    const args = argStr.trim() ? argStr.split(',').map(a => evalExpr(a.trim(), env)) : [];
    const result = callBuiltin(fname, args, argStr, env);
    if (result !== undefined) return result;
  }

  // Array access
  const arrAccess = expr.match(/^(\w+)\[(.+)\]$/);
  if (arrAccess) {
    const name = arrAccess[1].toUpperCase();
    const idx2 = Math.round(evalExpr(arrAccess[2], env));
    if (env.arrays[name]) return env.arrays[name].data[idx2 - env.arrays[name].lo];
  }

  // Variable
  const num = parseFloat(expr);
  if (!isNaN(num) && expr !== '') return num;
  const key = expr.toUpperCase();
  if (key in env.vars) return env.vars[key];

  // Last resort: number
  return isNaN(expr) ? expr : Number(expr);
}

function callFuncSync(name, argsStr, env) {
  // Synchronous function call for use in expressions
  const upName = name.toUpperCase();
  const fn = env.funcs[upName];
  if (!fn) return undefined;
  const args = parseArgList(argsStr, env);
  const localEnv = { vars: { ...env.vars }, funcs: env.funcs, procs: env.procs, arrays: { ...env.arrays }, callStack: [] };
  if (fn.params) fn.params.forEach((p, i) => { localEnv.vars[p.name.toUpperCase()] = args[i] ?? undefined; });
  // Run synchronously by executing line-by-line
  for (const l of fn.body) {
    const line = l.trim();
    if (/^RETURN\s/i.test(line)) return evalExpr(line.replace(/^RETURN\s+/i, ''), localEnv);
    const assignSimple = line.match(/^(\w+)\s*(?:←|←|<-|<--|←-)\s*(.+)/i);
    if (assignSimple) localEnv.vars[assignSimple[1].toUpperCase()] = evalExpr(assignSimple[2], localEnv);
    if (/^(OUTPUT|PRINT)\s/i.test(line)) addOutput(String(evalExpr(line.replace(/^(OUTPUT|PRINT)\s+/i, ''), localEnv)));
  }
  return undefined;
}

// ─── Parsing helpers ──────────────────────────────────────────────────────────
function matchingParen(s, start) {
  let depth = 0;
  for (let i = start; i < s.length; i++) {
    if (s[i] === '(') depth++;
    else if (s[i] === ')') { depth--; if (depth === 0) return i; }
  }
  return -1;
}

function hasBinaryOp(expr, op) {
  // Find op outside strings and parens
  let depth = 0, inStr = false;
  for (let i = 0; i < expr.length; i++) {
    const c = expr[i];
    if (c === '"' && !inStr) inStr = true;
    else if (c === '"' && inStr) inStr = false;
    if (inStr) continue;
    if (c === '(') depth++;
    else if (c === ')') depth--;
    if (depth > 0) continue;
    if (expr.substr(i, op.length) === op) {
      // For single-char ops avoid ambiguity with multi-char
      if ((op === '<' && (expr[i+1] === '=' || expr[i+1] === '>')) ) continue;
      if ((op === '>' && expr[i+1] === '=')) continue;
      if ((op === '=' && (expr[i-1] === '<' || expr[i-1] === '>' || expr[i+1] === '>'))) continue;
      // Unary minus
      if (op === '-' && i === 0) continue;
      if (op === '-' && '+-*/<>=(&|!'.includes(expr[i-1])) continue;
      // word ops need word boundary
      if (/^[A-Z]+$/.test(op)) {
        if (/\w/.test(expr[i-1] || '') || /\w/.test(expr[i+op.length] || '')) continue;
      }
      return true;
    }
  }
  return false;
}

function hasBinaryOpWord(expr, op) {
  const re = new RegExp(`\\b${op}\\b`, 'i');
  // Check outside strings/parens
  let depth = 0, inStr = false, clean = '';
  for (let i = 0; i < expr.length; i++) {
    const c = expr[i];
    if (c === '"' && !inStr) { inStr = true; clean += ' '; continue; }
    if (c === '"' && inStr) { inStr = false; clean += ' '; continue; }
    if (inStr) { clean += ' '; continue; }
    if (c === '(') depth++;
    if (c === ')') depth--;
    clean += (depth > 0) ? ' ' : c;
  }
  return re.test(clean);
}

function splitBinary(expr, op) {
  let depth = 0, inStr = false;
  for (let i = expr.length - 1; i >= 0; i--) {
    const c = expr[i];
    if (c === '"') inStr = !inStr;
    if (inStr) continue;
    if (c === ')') depth++;
    if (c === '(') depth--;
    if (depth > 0) continue;
    if (expr.substr(i, op.length) === op) {
      if ((op === '<' && (expr[i+1] === '=' || expr[i+1] === '>'))) continue;
      if ((op === '>' && expr[i+1] === '=')) continue;
      if ((op === '=' && (expr[i-1] === '<' || expr[i-1] === '>' || expr[i+1] === '>'))) continue;
      if (op === '-' && i === 0) continue;
      if (op === '-' && i > 0 && '+-*/<>=(&|!'.includes(expr[i-1])) continue;
      if (/^[A-Z]+$/.test(op)) {
        if (/\w/.test(expr[i-1] || '') || /\w/.test(expr[i+op.length] || '')) continue;
      }
      return [expr.substr(0, i).trim(), expr.substr(i + op.length).trim()];
    }
  }
  return [expr, ''];
}

function splitBinaryWord(expr, op) {
  const re = new RegExp(`\\b${op}\\b`, 'i');
  let depth = 0, inStr = false;
  let lastMatch = -1;
  let i = 0;
  while (i < expr.length) {
    const c = expr[i];
    if (c === '"') inStr = !inStr;
    if (!inStr) {
      if (c === '(') depth++;
      if (c === ')') depth--;
      if (depth === 0) {
        const m = expr.slice(i).match(re);
        if (m && m.index === 0) {
          lastMatch = i;
          i += op.length;
          continue;
        }
      }
    }
    i++;
  }
  if (lastMatch >= 0) return [expr.slice(0, lastMatch).trim(), expr.slice(lastMatch + op.length).trim()];
  return [expr, ''];
}

// ─── Input (async) ───────────────────────────────────────────────────────────
function getInput(prompt) {
  return new Promise(resolve => {
    document.getElementById('inputPromptLabel').textContent = prompt;
    document.getElementById('inputModalField').value = '';
    openModal('inputModal');
    setTimeout(() => document.getElementById('inputModalField').focus(), 100);
    inputResolve = resolve;
  });
}

function confirmModalInput() {
  const val = document.getElementById('inputModalField').value;
  closeModal('inputModal');
  if (inputResolve) { inputResolve(val); inputResolve = null; }
}

document.addEventListener('keydown', e => {
  if (document.getElementById('inputModal').classList.contains('open') && e.key === 'Enter') {
    confirmModalInput();
  }
});

// ─── Converters ───────────────────────────────────────────────────────────────
function toPython(code) {
  return code.split('\n').map(line => {
    let l = line;
    l = l.replace(/^DECLARE\s+\w+\s*:\s*.+/i, '# ' + l.trim());
    l = l.replace(/^CONSTANT\s+(\w+)\s*[←=<-]+\s*/i, '$1 = ');
    l = l.replace(/^OUTPUT\s+/i, 'print(') + (l.match(/^OUTPUT\s+/i) ? ')' : '');
    l = l.replace(/^INPUT\s+(\w+)/i, '$1 = input()');
    l = l.replace(/\s*←\s*/g, ' = ');
    l = l.replace(/\s*<--\s*/g, ' = ');
    l = l.replace(/\s*<-\s*/g, ' = ');
    l = l.replace(/\bAND\b/g, 'and').replace(/\bOR\b/g, 'or').replace(/\bNOT\b/g, 'not');
    l = l.replace(/\bMOD\b/g, '%').replace(/\bDIV\b/g, '//');
    l = l.replace(/^IF\s+(.+)\s+THEN$/i, 'if $1:');
    l = l.replace(/^ELSE$/i, 'else:');
    l = l.replace(/^ELSEIF\s+(.+)\s+THEN$/i, 'elif $1:');
    l = l.replace(/^ENDIF$/i, '');
    l = l.replace(/^FOR\s+(\w+)\s*=\s*(.+)\s+TO\s+(.+)$/i, 'for $1 in range($2, $3+1):');
    l = l.replace(/^NEXT\s+\w+$/i, '');
    l = l.replace(/^WHILE\s+(.+)\s+DO$/i, 'while $1:');
    l = l.replace(/^ENDWHILE$/i, '');
    l = l.replace(/^REPEAT$/i, 'while True:');
    l = l.replace(/^UNTIL\s+(.+)$/i, '    if ($1): break');
    l = l.replace(/^PROCEDURE\s+(\w+)\s*\(([^)]*)\)/i, 'def $1($2):');
    l = l.replace(/^ENDPROCEDURE$/i, '');
    l = l.replace(/^FUNCTION\s+(\w+)\s*\(([^)]*)\)\s+RETURNS\s+\w+/i, 'def $1($2):');
    l = l.replace(/^ENDFUNCTION$/i, '');
    l = l.replace(/^CALL\s+/i, '');
    l = l.replace(/&/g, '+');
    return l;
  }).join('\n');
}

// ─── VB.NET Console Converter ────────────────────────────────────────────────
function toVB(code) {
  // First pass: collect procedure/function signatures so we can emit proper subs/functions
  const rawLines = code.split('\n');
  const out = [];
  out.push('Module Program');
  out.push('');

  // We do a two-pass approach: split top-level from subroutine bodies
  // Gather all PROCEDURE / FUNCTION blocks first, then emit Main, then the subs
  const mainLines = [];
  const subBlocks = []; // {header, body[], isFunc, retType}

  let i = 0;
  while (i < rawLines.length) {
    const raw = rawLines[i].trim();
    const fnMatch = raw.match(/^FUNCTION\s+(\w+)\s*\(([^)]*)\)\s+RETURNS\s+(\w+)/i);
    const prMatch = raw.match(/^PROCEDURE\s+(\w+)\s*\(([^)]*)\)/i);

    if (fnMatch || prMatch) {
      const isFunc = !!fnMatch;
      const name = isFunc ? fnMatch[1] : prMatch[1];
      const paramStr = isFunc ? fnMatch[2] : prMatch[2];
      const retType = isFunc ? fnMatch[3] : null;
      const body = [];
      i++;
      let depth = 1;
      while (i < rawLines.length && depth > 0) {
        const l = rawLines[i].trim();
        if (/^(FUNCTION|PROCEDURE)\b/i.test(l)) depth++;
        if (/^(ENDFUNCTION|ENDPROCEDURE)\b/i.test(l)) { depth--; if (depth === 0) { i++; break; } }
        body.push(rawLines[i]);
        i++;
      }
      subBlocks.push({ name, paramStr, retType, isFunc, body });
    } else {
      // Skip bare ENDFUNCTION/ENDPROCEDURE at top level (shouldn't exist but just in case)
      if (!/^(ENDFUNCTION|ENDPROCEDURE)\b/i.test(raw)) mainLines.push(rawLines[i]);
      i++;
    }
  }

  // Emit Sub Main
  out.push('    Sub Main()');
  convertVBLines(mainLines, out, 2);
  out.push('    End Sub');

  // Emit subs/functions
  for (const block of subBlocks) {
    out.push('');
    const params = convertVBParams(block.paramStr);
    if (block.isFunc) {
      const retVB = mapVBType(block.retType);
      out.push(`    Function ${block.name}(${params}) As ${retVB}`);
      convertVBLines(block.body, out, 2);
      out.push(`    End Function`);
    } else {
      out.push(`    Sub ${block.name}(${params})`);
      convertVBLines(block.body, out, 2);
      out.push(`    End Sub`);
    }
  }

  out.push('');
  out.push('End Module');
  return out.join('\n');
}

function mapVBType(t) {
  if (!t) return 'Object';
  switch (t.toUpperCase()) {
    case 'INTEGER': return 'Integer';
    case 'REAL':    return 'Double';
    case 'STRING':  return 'String';
    case 'BOOLEAN': return 'Boolean';
    case 'CHAR':    return 'Char';
    default:        return t;
  }
}

function convertVBParams(paramStr) {
  if (!paramStr || !paramStr.trim()) return '';
  return paramStr.split(',').map(p => {
    const m = p.trim().match(/^(\w+)\s*:\s*(.+)$/);
    if (!m) return p.trim();
    return `${m[1]} As ${mapVBType(m[2].trim())}`;
  }).join(', ');
}

function convertVBLines(lines, out, indentLevel) {
  const pad = n => '    '.repeat(n);
  let depth = indentLevel;

  for (let i = 0; i < lines.length; i++) {
    const raw = lines[i];
    const line = raw.trim();
    if (!line || line.startsWith('//') || line.startsWith('REM')) {
      if (line.startsWith('//')) out.push(pad(depth) + "' " + line.slice(2).trim());
      else if (line.startsWith('REM')) out.push(pad(depth) + "' " + line.slice(3).trim());
      continue;
    }

    // Close keywords (reduce indent before emitting)
    if (/^(ENDIF|ENDWHILE|ENDFOR|ENDCASE|ENDFUNCTION|ENDPROCEDURE)\b/i.test(line)) continue; // handled by block emitters
    if (/^NEXT\s+\w+/i.test(line)) { depth--; out.push(pad(depth) + 'Next'); continue; }
    if (/^ENDWHILE$/i.test(line))  { depth--; out.push(pad(depth) + 'End While'); continue; }
    if (/^ENDIF$/i.test(line))     { depth--; out.push(pad(depth) + 'End If'); continue; }
    if (/^ENDCASE$/i.test(line))   { depth--; out.push(pad(depth) + 'End Select'); continue; }
    if (/^UNTIL\s+(.+)$/i.test(line)) {
      const cond = line.replace(/^UNTIL\s+/i, '');
      depth--;
      out.push(pad(depth) + 'Loop Until ' + convertVBExpr(cond));
      continue;
    }
    if (/^ELSE$/i.test(line))     { out.push(pad(depth - 1) + 'Else'); continue; }
    if (/^ELSEIF\s+(.+)\s+THEN$/i.test(line)) {
      const cond = line.replace(/^ELSEIF\s+/i,'').replace(/\s+THEN$/i,'');
      out.push(pad(depth - 1) + 'ElseIf ' + convertVBExpr(cond) + ' Then');
      continue;
    }
    if (/^OTHERWISE$/i.test(line)) { out.push(pad(depth - 1) + 'Case Else'); continue; }

    // DECLARE
    const declArr = line.match(/^DECLARE\s+(\w+)\s*:\s*ARRAY\[(-?\d+):(-?\d+)\]\s+OF\s+(\w+)/i);
    if (declArr) {
      const lo = declArr[2], hi = declArr[3], vtype = mapVBType(declArr[4]);
      out.push(pad(depth) + `Dim ${declArr[1]}(${lo} To ${hi}) As ${vtype}`);
      continue;
    }
    const decl = line.match(/^DECLARE\s+(\w+)\s*:\s*(.+)/i);
    if (decl) {
      out.push(pad(depth) + `Dim ${decl[1]} As ${mapVBType(decl[2].trim())}`);
      continue;
    }
    const constant = line.match(/^CONSTANT\s+(\w+)\s*[=←<\-]+\s*(.+)/i);
    if (constant) {
      out.push(pad(depth) + `Const ${constant[1]} = ${convertVBExpr(constant[2].trim())}`);
      continue;
    }

    // OUTPUT
    const output = line.match(/^(OUTPUT|PRINT)\s+(.+)/i);
    if (output) {
      out.push(pad(depth) + `Console.WriteLine(${convertVBExpr(output[2].trim())})`);
      continue;
    }

    // INPUT
    const input = line.match(/^INPUT\s+(\w+)/i);
    if (input) {
      out.push(pad(depth) + `${input[1]} = Console.ReadLine()`);
      continue;
    }

    // RETURN
    const ret = line.match(/^RETURN\s+(.+)/i);
    if (ret) {
      out.push(pad(depth) + `Return ${convertVBExpr(ret[1].trim())}`);
      continue;
    }

    // CALL
    const call = line.match(/^CALL\s+(\w+)\s*(?:\(([^)]*)\))?/i);
    if (call) {
      const args = call[2] ? convertVBExpr(call[2]) : '';
      out.push(pad(depth) + `${call[1]}(${args})`);
      continue;
    }

    // IF ... THEN
    const ifLine = line.match(/^IF\s+(.+)\s+THEN$/i);
    if (ifLine) {
      out.push(pad(depth) + `If ${convertVBExpr(ifLine[1])} Then`);
      depth++;
      continue;
    }

    // FOR ... TO ... STEP?
    const forLine = line.match(/^FOR\s+(\w+)\s*(?:←|←|<-|<--|←-|=)\s*(.+?)\s+TO\s+(.+?)(?:\s+STEP\s+(.+))?$/i);
    if (forLine) {
      const step = forLine[4] ? ` Step ${convertVBExpr(forLine[4])}` : '';
      out.push(pad(depth) + `For ${forLine[1]} = ${convertVBExpr(forLine[2])} To ${convertVBExpr(forLine[3])}${step}`);
      depth++;
      continue;
    }

    // WHILE ... DO
    const whileLine = line.match(/^WHILE\s+(.+)\s+DO$/i);
    if (whileLine) {
      out.push(pad(depth) + `While ${convertVBExpr(whileLine[1])}`);
      depth++;
      continue;
    }

    // REPEAT
    if (/^REPEAT$/i.test(line)) {
      out.push(pad(depth) + 'Do');
      depth++;
      continue;
    }

    // CASE OF
    const caseLine = line.match(/^CASE\s+OF\s+(.+)/i);
    if (caseLine) {
      out.push(pad(depth) + `Select Case ${convertVBExpr(caseLine[1])}`);
      depth++;
      continue;
    }

    // Case value : statement  (inside CASE OF block)
    const caseVal = line.match(/^(.+?)\s*:\s*(.+)$/);
    if (caseVal && depth > indentLevel) {
      // Likely a case branch
      out.push(pad(depth - 1) + `Case ${convertVBExpr(caseVal[1].trim())}`);
      // emit the statement on the next line indented
      const stmt = caseVal[2].trim();
      // Re-process the statement by recursing with a single-item list
      const tmp = [];
      convertVBLines([stmt], tmp, depth);
      out.push(...tmp);
      continue;
    }

    // Array assignment
    const arrAssign = line.match(/^(\w+)\[(.+?)\]\s*(?:←|←|<-|<--|←-)\s*(.+)/i);
    if (arrAssign) {
      out.push(pad(depth) + `${arrAssign[1]}(${convertVBExpr(arrAssign[2])}) = ${convertVBExpr(arrAssign[3])}`);
      continue;
    }

    // Simple assignment
    const assign = line.match(/^(\w+)\s*(?:←|←|<-|<--|←-)\s*(.+)/i);
    if (assign) {
      out.push(pad(depth) + `${assign[1]} = ${convertVBExpr(assign[2].trim())}`);
      continue;
    }

    // FUNCTION/PROCEDURE definition lines — skip (handled outside)
    if (/^(FUNCTION|PROCEDURE|ENDFUNCTION|ENDPROCEDURE)\b/i.test(line)) continue;

    // Fallback: emit as comment
    out.push(pad(depth) + "' " + line);
  }
}

function convertVBExpr(expr) {
  if (!expr) return '';
  let e = expr.trim();
  // String concat & → &
  // operators
  e = e.replace(/\bAND\b/gi, 'AndAlso');
  e = e.replace(/\bOR\b/gi,  'OrElse');
  e = e.replace(/\bNOT\b/gi, 'Not');
  e = e.replace(/\bMOD\b/gi, 'Mod');
  e = e.replace(/\bDIV\b/gi, '\\');
  e = e.replace(/<>/g, '<>');  // already VB
  // Boolean literals
  e = e.replace(/\bTRUE\b/gi,  'True');
  e = e.replace(/\bFALSE\b/gi, 'False');
  // Built-in function mapping
  e = e.replace(/\bLENGTH\s*\(/gi,     'Len(');
  e = e.replace(/\bUCASE\s*\(/gi,      'UCase(');
  e = e.replace(/\bLCASE\s*\(/gi,      'LCase(');
  e = e.replace(/\bMID\s*\(/gi,        'Mid(');
  e = e.replace(/\bLEFT\s*\(/gi,       'Left(');
  e = e.replace(/\bRIGHT\s*\(/gi,      'Right(');
  e = e.replace(/\bSQRT\s*\(/gi,       'Math.Sqrt(');
  e = e.replace(/\bABS\s*\(/gi,        'Math.Abs(');
  e = e.replace(/\bROUND\s*\(/gi,      'Math.Round(');
  e = e.replace(/\bINT\s*\(/gi,        'CInt(');
  e = e.replace(/\bCHR\s*\(/gi,        'Chr(');
  e = e.replace(/\bASC\s*\(/gi,        'Asc(');
  e = e.replace(/\bORD\s*\(/gi,        'Asc(');
  e = e.replace(/\bNUM_TO_STR\s*\(/gi, 'CStr(');
  e = e.replace(/\bSTR_TO_NUM\s*\(/gi, 'CInt(');
  e = e.replace(/\bTOSTRING\s*\(/gi,   'CStr(');
  e = e.replace(/\bTOINTEGER\s*\(/gi,  'CInt(');
  e = e.replace(/\bTOREAL\s*\(/gi,     'CDbl(');
  e = e.replace(/\bRANDOM\s*\(\s*\)/gi,'Rnd()');
  // Array access: name[x] → name(x)
  e = e.replace(/(\w+)\[([^\]]+)\]/g, '$1($2)');
  return e;
}
function openModal(id) { document.getElementById(id).classList.add('open'); }
function closeModal(id) { document.getElementById(id).classList.remove('open'); }

// ─── Utils ────────────────────────────────────────────────────────────────────
function escHtml(s) { return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

// ─── Startup ──────────────────────────────────────────────────────────────────
init();
</script>
</body>
</html>
