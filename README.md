# Goblin-disgnostic-centre-V1
<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Goblin Diagnostic Center</title>  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700&family=Lora:wght@400;500;600;700&display=swap" rel="stylesheet">  <style>
    :root {
      --forest: #182416;
      --forest-soft: #26351f;
      --moss: #5f7144;
      --mushroom: #d8c7aa;
      --parchment: #f3e7cf;
      --ink: #261f19;
      --gold: #b99a58;
      --plum: #4a2f3d;
      --shadow: rgba(0, 0, 0, 0.35);
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      font-family: "Lora", serif;
      color: var(--parchment);
      background:
        radial-gradient(circle at top left, rgba(185, 154, 88, 0.18), transparent 32%),
        radial-gradient(circle at bottom right, rgba(74, 47, 61, 0.35), transparent 35%),
        linear-gradient(135deg, #0c120b, var(--forest), #10170f);
      overflow-x: hidden;
    }

    body::before {
      content: "";
      position: fixed;
      inset: 0;
      background-image:
        radial-gradient(circle, rgba(243, 231, 207, 0.11) 1px, transparent 1px),
        radial-gradient(circle, rgba(185, 154, 88, 0.08) 1px, transparent 1px);
      background-size: 38px 38px, 78px 78px;
      pointer-events: none;
      opacity: 0.45;
    }

    .app {
      width: min(1100px, 94vw);
      margin: 0 auto;
      padding: 38px 0 60px;
      position: relative;
      z-index: 1;
    }

    header {
      text-align: center;
      margin-bottom: 28px;
    }

    .eyebrow {
      letter-spacing: 0.22em;
      text-transform: uppercase;
      color: var(--gold);
      font-size: 0.78rem;
      margin-bottom: 8px;
    }

    h1 {
      font-family: "Cinzel Decorative", serif;
      font-size: clamp(2.2rem, 7vw, 5rem);
      line-height: 0.98;
      margin: 0;
      text-shadow: 0 10px 25px var(--shadow);
    }

    .subtitle {
      max-width: 650px;
      margin: 16px auto 0;
      color: rgba(243, 231, 207, 0.82);
      font-size: 1.05rem;
      line-height: 1.6;
    }

    .grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 22px;
      align-items: start;
    }

    .panel,
    .result-card {
      background: rgba(24, 36, 22, 0.78);
      border: 1px solid rgba(185, 154, 88, 0.35);
      border-radius: 26px;
      box-shadow: 0 22px 60px var(--shadow);
      backdrop-filter: blur(8px);
    }

    .panel {
      padding: 24px;
    }

    h2 {
      margin: 0 0 14px;
      font-family: "Cinzel Decorative", serif;
      color: var(--gold);
      font-size: 1.4rem;
    }

    .state-list,
    .symptom-list {
      display: grid;
      gap: 10px;
    }

    .state-list {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }

    .symptom-list {
      grid-template-columns: repeat(2, minmax(0, 1fr));
      margin-top: 10px;
    }

    button {
      font-family: inherit;
      cursor: pointer;
      border: none;
    }

    .chip {
      padding: 13px 14px;
      border-radius: 18px;
      background: rgba(243, 231, 207, 0.08);
      color: var(--parchment);
      border: 1px solid rgba(243, 231, 207, 0.16);
      text-align: left;
      transition: 0.2s ease;
      min-height: 58px;
    }

    .chip:hover {
      transform: translateY(-2px);
      background: rgba(243, 231, 207, 0.13);
      border-color: rgba(185, 154, 88, 0.65);
    }

    .chip.active {
      background: rgba(185, 154, 88, 0.22);
      border-color: var(--gold);
      box-shadow: inset 0 0 0 1px rgba(185, 154, 88, 0.35);
    }

    .chip span {
      display: block;
      font-size: 1.3rem;
      margin-bottom: 5px;
    }

    .diagnose-btn {
      width: 100%;
      margin-top: 20px;
      padding: 16px 18px;
      border-radius: 999px;
      background: linear-gradient(135deg, var(--gold), #e1c57e);
      color: var(--ink);
      font-weight: 700;
      font-size: 1.05rem;
      box-shadow: 0 16px 35px rgba(0, 0, 0, 0.32);
      transition: 0.2s ease;
    }

    .diagnose-btn:hover {
      transform: translateY(-2px) scale(1.01);
    }

    .result-wrap {
      position: sticky;
      top: 20px;
    }

    .result-card {
      min-height: 600px;
      padding: 20px;
      background:
        linear-gradient(rgba(243, 231, 207, 0.9), rgba(243, 231, 207, 0.86)),
        radial-gradient(circle at top, rgba(185, 154, 88, 0.25), transparent 45%);
      color: var(--ink);
      border: 6px double rgba(74, 47, 61, 0.65);
      position: relative;
      overflow: hidden;
    }

    .result-card::before,
    .result-card::after {
      position: absolute;
      font-size: 7rem;
      opacity: 0.12;
      pointer-events: none;
    }

    .result-card::before {
      content: "☾";
      top: 2px;
      left: 18px;
    }

    .result-card::after {
      content: "✦";
      right: 22px;
      bottom: 2px;
    }

    .card-inner {
      border: 1px solid rgba(38, 31, 25, 0.25);
      border-radius: 20px;
      padding: 24px;
      min-height: 552px;
      position: relative;
      z-index: 1;
    }

    .card-label {
      text-align: center;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      font-size: 0.72rem;
      color: var(--plum);
      font-weight: 700;
    }

    .card-title {
      text-align: center;
      font-family: "Cinzel Decorative", serif;
      font-size: clamp(1.8rem, 5vw, 3.1rem);
      margin: 8px 0 2px;
      color: var(--forest);
    }

    .card-subtitle {
      text-align: center;
      color: var(--plum);
      font-weight: 700;
      margin-bottom: 18px;
    }

    .divider {
      text-align: center;
      color: var(--gold);
      margin: 14px 0;
      letter-spacing: 0.5em;
    }

    .section {
      margin: 14px 0;
    }

    .section strong {
      display: block;
      color: var(--forest);
      margin-bottom: 5px;
      font-size: 0.9rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
    }

    .section p {
      margin: 0;
      line-height: 1.55;
    }

    ul {
      margin: 6px 0 0;
      padding-left: 20px;
      line-height: 1.7;
    }

    .placeholder {
      display: grid;
      place-items: center;
      min-height: 510px;
      text-align: center;
      color: rgba(38, 31, 25, 0.75);
    }

    .placeholder h3 {
      font-family: "Cinzel Decorative", serif;
      font-size: 2rem;
      margin: 0 0 10px;
      color: var(--forest);
    }

    .footer-note {
      margin-top: 18px;
      text-align: center;
      color: rgba(243, 231, 207, 0.66);
      font-size: 0.88rem;
    }

    @media (max-width: 850px) {
      .grid {
        grid-template-columns: 1fr;
      }

      .result-wrap {
        position: static;
      }
    }

    @media (max-width: 540px) {
      .state-list,
      .symptom-list {
        grid-template-columns: 1fr;
      }

      .panel {
        padding: 18px;
      }

      .card-inner {
        padding: 18px;
      }
    }
  </style></head>
<body>
  <main class="app">
    <header>
      <div class="eyebrow">Forest Approved • Clinically Suspicious</div>
      <h1>Goblin Diagnostic Center</h1>
      <p class="subtitle">
        Choose your current goblin state, tap the symptoms haunting your tiny woodland body,
        and receive one highly questionable medical tarot diagnosis.
      </p>
    </header><section class="grid">
  <div class="panel">
    <h2>Choose Your Goblin State</h2>
    <div class="state-list" id="stateList"></div>

    <h2 style="margin-top: 26px;">Tap Symptoms</h2>
    <div class="symptom-list" id="symptomList"></div>

    <button class="diagnose-btn" id="diagnoseBtn">Diagnose My Goblin ✨</button>
    <p class="footer-note">No goblins were harmed. Several were perceived.</p>
  </div>

  <div class="result-wrap">
    <article class="result-card">
      <div class="card-inner" id="resultCard">
        <div class="placeholder">
          <div>
            <h3>Awaiting Diagnosis</h3>
            <p>The forest healer is sharpening a tiny clipboard.</p>
          </div>
        </div>
      </div>
    </article>
  </div>
</section>

  </main>  <script>
    const goblinStates = [
      {
        id: "functional",
        emoji: "🪵",
        name: "Functional Goblin",
        tarot: "The Polished Stick",
        weather: "Partly cloudy with suspicious bursts of competence.",
        translation: "You are functioning just enough to make people think you are fine. Dangerous illusion. Useful, but dangerous.",
        protocol: [
          "Drink water before the caffeine unionizes.",
          "Do one task that will make tomorrow-you less feral.",
          "Eat something with actual nutrients, not just vibes.",
          "Accept the win. Do not interrogate it."
        ],
        threat: "Low Risk Goblin"
      },
      {
        id: "crunchy",
        emoji: "🍂",
        name: "Emotionally Crunchy",
        tarot: "The Hollow Branch",
        weather: "Dry winds. Brittle mood conditions. Chance of snapping if perceived incorrectly.",
        translation: "Your nervous system is over-toasted. You are not broken, but you are making a sound like old leaves under boots.",
        protocol: [
          "Protein immediately. The forest demands it.",
          "Lower the brightness of your life by 30%.",
          "No complicated conversations until your soul has rehydrated.",
          "Comfort show. Blanket. Silence."
        ],
        threat: "Crunch Advisory"
      },
      {
        id: "moist",
        emoji: "🌧️",
        name: "Unstable Moist Goblin",
        tarot: "The Moistening",
        weather: "Heavy fog with emotional drizzle. Sudden indoor storms likely.",
        translation: "The creature has become damp from overstimulation, tenderness, and one too many thoughts touching each other.",
        protocol: [
          "Cry if required, but hydrate like a professional swamp witch.",
          "Do not text emotionally expensive people.",
          "Acquire warm drink and nest materials.",
          "Postpone all dramatic life choices until sunrise."
        ],
        threat: "Wet Hazard"
      },
      {
        id: "roadkill",
        emoji: "🪦",
        name: "Roadkill Level Crunch",
        tarot: "The Flattened Possum",
        weather: "Apocalyptic. Doom jazz. Executive function found face-down in a ditch.",
        translation: "You have been psychologically run over by the day. We are no longer optimizing. We are preserving the species.",
        protocol: [
          "Cancel everything that is not legally or medically required.",
          "Tiny win only: food, shower, or one reply. Pick one.",
          "Lie down horizontally and let gravity apologize.",
          "Survival mode is not failure. It is forest strategy."
        ],
        threat: "Immediate Goblin Intervention"
      },
      {
        id: "cave",
        emoji: "🕯️",
        name: "Cave Goblin Mode",
        tarot: "The Lantern Under The Rock",
        weather: "Low visibility. Social battery deceased. Hissing possible.",
        translation: "You require solitude, dim lighting, and the sacred right to not explain yourself for several hours.",
        protocol: [
          "Retreat to nest immediately.",
          "Inform one trusted human you are alive but unavailable.",
          "Choose one low-stimulation comfort activity.",
          "Re-enter society only when the claws retract."
        ],
        threat: "Socially Feral"
      },
      {
        id: "employed",
        emoji: "📜",
        name: "Vaguely Employed",
        tarot: "The Timesheet Goblin",
        weather: "Monday-shaped dread with inconvenient competence clearing by noon.",
        translation: "You are participating in capitalism while spiritually lying face-down in moss.",
        protocol: [
          "Make the to-do list insultingly small.",
          "Coffee first. Panic second. Email third.",
          "Complete one visible task for reputation maintenance.",
          "Reward yourself like a woodland creature who survived a tax audit."
        ],
        threat: "Payroll Survivor"
      },
      {
        id: "lashes",
        emoji: "💅",
        name: "Lash Endangerment Protocol",
        tarot: "The Sacred Blink",
        weather: "Wind advisory. One emotional episode away from beauty consequences.",
        translation: "Your self-care maintenance is entering sacred emergency territory. The lashes have requested legal counsel.",
        protocol: [
          "Book the appointment. Do not negotiate with the mirror goblin.",
          "Wash your face respectfully.",
          "No picking, rubbing, or chaos-fidgeting.",
          "Romanticize maintenance as a ritual, because it is."
        ],
        threat: "Beauty Emergency"
      },
      {
        id: "theatre",
        emoji: "🎭",
        name: "Theatre Goblin Possession",
        tarot: "The Dramatic Fern",
        weather: "Cinematic overreaction with orchestral thunder and suspicious symbolism.",
        translation: "Everything feels meaningful because your inner narrator has found a velvet cape and refuses to remove it.",
        protocol: [
          "Put the dramatic playlist on intentionally.",
          "Write the feelings before texting them.",
          "Separate intuition from theatrical flair. They are cousins, not twins.",
          "Touch grass, but poetically."
        ],
        threat: "Excessive Drama Advisory"
      }
    ];

    const symptoms = [
      { id: "sleep", emoji: "🌙", label: "bad sleep" },
      { id: "anxiety", emoji: "✒️", label: "anxiety yelling in cursive" },
      { id: "lashes", emoji: "👁️", label: "fresh lashes" },
      { id: "playlist", emoji: "🎧", label: "haunted playlist" },
      { id: "caffeine", emoji: "☕", label: "too much caffeine" },
      { id: "fictional", emoji: "🐉", label: "attached to fictional men" },
      { id: "doom", emoji: "🕳️", label: "doom scrolling" },
      { id: "overstim", emoji: "⚡", label: "overstimulated" },
      { id: "crying", emoji: "💧", label: "crying for unknown reasons" },
      { id: "grass", emoji: "🌿", label: "touched grass recently" }
    ];

    let selectedState = goblinStates[0];
    let selectedSymptoms = [];

    const stateList = document.getElementById("stateList");
    const symptomList = document.getElementById("symptomList");
    const resultCard = document.getElementById("resultCard");
    const diagnoseBtn = document.getElementById("diagnoseBtn");

    function renderStates() {
      stateList.innerHTML = "";

      goblinStates.forEach((state) => {
        const button = document.createElement("button");
        button.className = `chip ${selectedState.id === state.id ? "active" : ""}`;
        button.innerHTML = `<span>${state.emoji}</span>${state.name}`;
        button.addEventListener("click", () => {
          selectedState = state;
          renderStates();
        });
        stateList.appendChild(button);
      });
    }

    function renderSymptoms() {
      symptomList.innerHTML = "";

      symptoms.forEach((symptom) => {
        const isActive = selectedSymptoms.includes(symptom.id);
        const button = document.createElement("button");
        button.className = `chip ${isActive ? "active" : ""}`;
        button.innerHTML = `<span>${symptom.emoji}</span>${symptom.label}`;
        button.addEventListener("click", () => {
          if (isActive) {
            selectedSymptoms = selectedSymptoms.filter((id) => id !== symptom.id);
          } else {
            selectedSymptoms.push(symptom.id);
          }
          renderSymptoms();
        });
        symptomList.appendChild(button);
      });
    }

    function getSymptomLabels() {
      return selectedSymptoms.map((id) => {
        const found = symptoms.find((symptom) => symptom.id === id);
        return found ? `${found.emoji} ${found.label}` : id;
      });
    }

    function symptomBonusLine() {
      const count = selectedSymptoms.length;

      if (count === 0) {
        return "No symptoms selected. The healer suspects repression or excellent lighting.";
      }

      if (count <= 2) {
        return "Mildly cursed, but still manageable with snacks and one responsible choice.";
      }

      if (count <= 5) {
        return "Moderately haunted. The forest recommends immediate softness and fewer decisions.";
      }

      return "Severely enchanted. Please place the goblin in a blanket-lined containment nest.";
    }

    function renderDiagnosis() {
      const symptomLabels = getSymptomLabels();
      const symptomHTML = symptomLabels.length
        ? symptomLabels.map((label) => `<li>${label}</li>`).join("")
        : "<li>None selected, which is suspicious.</li>";

      const protocolHTML = selectedState.protocol
        .map((step) => `<li>${step}</li>`)
        .join("");

      resultCard.innerHTML = `
        <div class="card-label">Current Diagnosis</div>
        <h3 class="card-title">${selectedState.tarot}</h3>
        <div class="card-subtitle">${selectedState.emoji} ${selectedState.name}</div>

        <div class="divider">✦ ✦ ✦</div>

        <div class="section">
          <strong>Emotional Weather</strong>
          <p>${selectedState.weather}</p>
        </div>

        <div class="section">
          <strong>Forest Translation</strong>
          <p>${selectedState.translation}</p>
        </div>

        <div class="section">
          <strong>Symptoms Detected</strong>
          <ul>${symptomHTML}</ul>
        </div>

        <div class="section">
          <strong>Symptom Reading</strong>
          <p>${symptomBonusLine()}</p>
        </div>

        <div class="section">
          <strong>Emergency Forest Protocol</strong>
          <ul>${protocolHTML}</ul>
        </div>

        <div class="section">
          <strong>Threat Level</strong>
          <p>${selectedState.threat}</p>
        </div>
      `;
    }

    diagnoseBtn.addEventListener("click", renderDiagnosis);

    renderStates();
    renderSymptoms();
  </script></body>
</html>
