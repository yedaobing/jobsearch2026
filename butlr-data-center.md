---
layout: default
title: Butlr Data Center Program Workflow
permalink: /butlr-data-center/
---


{% capture workflow %}{% include_relative butlr-data-center-program-workflow.md %}{% endcapture %}
{{ workflow | replace: '](assets/', '](../assets/' | replace: '](butlr-data-center-diagram.html', '](../butlr-data-center-diagram.html' | replace: '](butlr-business-workflow.md', '](../butlr/' | markdownify }}

<script type="module">
  import mermaid from "https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs";

  document.querySelectorAll("pre > code.language-mermaid").forEach((code) => {
    const diagram = document.createElement("div");
    diagram.className = "mermaid";
    diagram.textContent = code.textContent;
    code.parentElement.replaceWith(diagram);
  });

  mermaid.initialize({
    startOnLoad: false,
    securityLevel: "strict",
    theme: "neutral",
    flowchart: { useMaxWidth: true }
  });
  await mermaid.run({ querySelector: ".mermaid" });
</script>

<style>
  .wrapper {
    max-width: 1180px;
  }

  table {
    display: table;
    width: 100%;
    font-size: 0.92rem;
  }

  th {
    background: #eef5fb;
  }

  .mermaid {
    margin: 2rem auto;
    overflow-x: auto;
    text-align: center;
  }
</style>

