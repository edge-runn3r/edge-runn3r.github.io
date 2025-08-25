---
title: "Password Generator"
description: "Generate strong, customizable passwords."
slug: "password-generator"
type: "page"
menu:
  main:
    name: "Password Gen"
    weight: 50
---

Generate strong, customizable passwords right in your browser.

<form id="pw-options">
  <label>
    Length:
    <input type="number" id="length" min="4" max="64" value="12">
  </label><br>

  <label><input type="checkbox" id="upper" checked> Uppercase</label><br>
  <label><input type="checkbox" id="lower" checked> Lowercase</label><br>
  <label><input type="checkbox" id="numbers" checked> Numbers</label><br>
  <label><input type="checkbox" id="symbols" checked> Symbols</label><br>

  <button type="button" id="generate">Generate</button>
</form>

<div class="mt-4">
  <label for="output">Generated Password:</label><br>
  <input type="text" id="output" readonly>
  <button type="button" id="copy">Copy</button>
</div>

<script>
(function(){
  const upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  const lower = "abcdefghijklmnopqrstuvwxyz";
  const numbers = "0123456789";
  const symbols = "!@#$%^&*()_+-=[]{}|;:,.<>?";

  function generatePassword(opts) {
    let chars = "";
    if (opts.upper) chars += upper;
    if (opts.lower) chars += lower;
    if (opts.numbers) chars += numbers;
    if (opts.symbols) chars += symbols;
    if (!chars) return "";

    let pw = "";
    for (let i=0; i<opts.length; i++) {
      pw += chars.charAt(Math.floor(Math.random() * chars.length));
    }
    return pw;
  }

  document.getElementById("generate").onclick = () => {
    const opts = {
      length: parseInt(document.getElementById("length").value, 10) || 12,
      upper: document.getElementById("upper").checked,
      lower: document.getElementById("lower").checked,
      numbers: document.getElementById("numbers").checked,
      symbols: document.getElementById("symbols").checked,
    };
    document.getElementById("output").value = generatePassword(opts);
  };

  document.getElementById("copy").onclick = () => {
    const out = document.getElementById("output");
    out.select();
    document.execCommand("copy");
  };
})();
</script>
