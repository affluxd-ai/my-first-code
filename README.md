<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Cosmic Wonders</title>
    <style>
      :root {
        color-scheme: dark;
        --bg: #020617;
        --panel: rgba(15, 23, 42, 0.82);
        --panel-border: rgba(148, 163, 184, 0.25);
        --text: #e2e8f0;
        --muted: #94a3b8;
        --accent: #38bdf8;
        --accent-2: #a78bfa;
      }

      * {
        box-sizing: border-box;
      }

      body {
        margin: 0;
        font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
        color: var(--text);
        min-height: 100vh;
        background:
          radial-gradient(circle at top left, rgba(56, 189, 248, 0.2), transparent 28%),
          radial-gradient(circle at bottom right, rgba(167, 139, 250, 0.2), transparent 24%),
          linear-gradient(135deg, #020617 0%, #0f172a 100%);
        overflow-x: hidden;
      }

      body::before {
        content: "";
        position: fixed;
        inset: 0;
        background-image: radial-gradient(rgba(255, 255, 255, 0.14) 1px, transparent 1px);
        background-size: 24px 24px;
        opacity: 0.18;
        pointer-events: none;
      }

      .page {
        max-width: 1100px;
        margin: 0 auto;
        padding: 30px 20px 60px;
        position: relative;
      }

      .banner {
        padding: 24px 28px;
        border: 1px solid var(--panel-border);
        border-radius: 22px;
        background: linear-gradient(135deg, rgba(15, 23, 42, 0.95), rgba(2, 6, 23, 0.9));
        box-shadow: 0 20px 60px rgba(2, 6, 23, 0.45);
        backdrop-filter: blur(16px);
      }

      .banner h1 {
        margin: 0 0 10px;
        font-size: clamp(2rem, 4vw, 3rem);
        letter-spacing: 0.04em;
        text-transform: uppercase;
      }

      .banner p {
        margin: 0;
        font-size: 1rem;
        color: var(--muted);
        line-height: 1.7;
      }

      .controls {
        display: flex;
        justify-content: flex-end;
        margin: 20px 0 0;
      }

      button {
        border: 0;
        border-radius: 999px;
        padding: 10px 18px;
        font-weight: 700;
        color: #f8fafc;
        background: linear-gradient(90deg, var(--accent), var(--accent-2));
        cursor: pointer;
        box-shadow: 0 10px 30px rgba(56, 189, 248, 0.2);
        transition: transform 0.2s ease, box-shadow 0.2s ease;
      }

      button:hover {
        transform: translateY(-2px);
        box-shadow: 0 14px 34px rgba(56, 189, 248, 0.28);
      }

      .facts {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
        gap: 22px;
        margin-top: 28px;
      }

      .fact-card {
        position: relative;
        padding: 28px 22px 24px;
        border-radius: 18px;
        background: var(--panel);
        border: 1px solid var(--panel-border);
        box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.04);
        overflow: hidden;
      }

      .fact-card::before {
        content: "";
        position: absolute;
        inset: 0;
        background: linear-gradient(135deg, rgba(56, 189, 248, 0.12), transparent 40%);
        pointer-events: none;
      }

      .fact-number {
        display: inline-block;
        margin-bottom: 12px;
        font-size: 0.8rem;
        font-weight: 700;
        letter-spacing: 0.2em;
        text-transform: uppercase;
        color: var(--accent);
      }

      .fact-card p {
        margin: 0;
        font-size: 1.03rem;
        line-height: 1.7;
        color: #f8fafc;
      }

      @media (max-width: 640px) {
        .page {
          padding: 20px 14px 44px;
        }

        .banner {
          padding: 18px 20px;
        }
      }
    </style>
  </head>
  <body>
    <main class="page">
      <section class="banner">
        <h1>Cosmic Wonders</h1>
        <p>Three dazzling facts from the farthest reaches of the universe — refreshed each time you visit.</p>
        <div class="controls">
          <button id="refresh">Reload the cosmos ✨</button>
        </div>
      </section>

      <section id="fact-list" class="facts" aria-live="polite"></section>
    </main>

    <script>
      const facts = [
        "A day on Venus is longer than a year on Venus — it spins so slowly that one full rotation takes longer than one orbit around the Sun.",
        "Neutron stars are so dense that a teaspoon of their material would weigh about a billion tons on Earth.",
        "There are more stars in the observable universe than there are grains of sand on all the beaches on Earth.",
        "The Sun is so large that more than 1 million Earths could fit inside it.",
        "Some planets have clouds made of metal, and on Venus it may rain sulfuric acid high in the atmosphere.",
        "The Milky Way is racing through space at about 2.1 million kilometers per hour relative to the cosmic microwave background."
      ];

      function shuffleFacts() {
        const copy = [...facts];
        for (let i = copy.length - 1; i > 0; i -= 1) {
          const j = Math.floor(Math.random() * (i + 1));
          [copy[i], copy[j]] = [copy[j], copy[i]];
        }
        return copy.slice(0, 3);
      }

      function renderFacts() {
        const container = document.getElementById("fact-list");
        const selected = shuffleFacts();
        container.innerHTML = selected
          .map((fact, index) => `
            <article class="fact-card">
              <div class="fact-number">Fact 0${index + 1}</div>
              <p>${fact}</p>
            </article>
          `)
          .join("");
      }

      document.getElementById("refresh").addEventListener("click", renderFacts);
      window.addEventListener("DOMContentLoaded", renderFacts);
    </script>
  </body>
</html>
