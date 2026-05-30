import { useState, useEffect, useRef } from "react";

const skills = [
  { name: "TypeScript", icon: "TS", color: "#3178C6", type: "lang" },
  { name: "Flutter/Dart", icon: "Fl", color: "#54C5F8", type: "lang" },
  { name: "React", icon: "Re", color: "#61DAFB", type: "frontend" },
  { name: "Next.js", icon: "Nx", color: "#ffffff", type: "frontend" },
  { name: "Nuxt.js", icon: "Nu", color: "#00DC82", type: "frontend" },
  { name: "PostgreSQL", icon: "Pg", color: "#336791", type: "db" },
  { name: "MongoDB", icon: "Mo", color: "#47A248", type: "db" },
  { name: "Figma", icon: "Fi", color: "#F24E1E", type: "tool" },
  { name: "Git", icon: "Gt", color: "#F05032", type: "tool" },
];

const modes = ["solo", "team", "ai"];

const modeData = {
  solo: {
    label: "Solo Mode",
    description: "Self-directed. Deep work. No blockers, just shipping.",
    traits: ["Self-taught discipline", "Offline-first thinking", "Full ownership"],
    accent: "#ffffff",
  },
  team: {
    label: "Collab Mode",
    description: "Open to contributions, clear communicator, async-friendly.",
    traits: ["Version control fluency", "Readable code first", "Docs matter"],
    accent: "#00DC82",
  },
  ai: {
    label: "AI/ML Mode",
    description: "Enthusiast building at the intersection of UI and intelligence.",
    traits: ["Model-aware design", "Data intuition", "Prompt engineering"],
    accent: "#54C5F8",
  },
};

const projects = [
  {
    name: "Todo App",
    desc: "CRUD fundamentals. Where it started.",
    tag: "Public",
    tagColor: "#00DC82",
  },
  {
    name: "YEMS",
    desc: "Offline-first school management system. Real constraints, real solutions.",
    tag: "Private",
    tagColor: "#888",
  },
];

const terminalLines = [
  { text: "> loading persona...", delay: 0 },
  { text: "> name: Fawehinmi Erioluwa", delay: 400 },
  { text: "> age: 17", delay: 700 },
  { text: "> role: Frontend Engineer (+ backend instincts)", delay: 1000 },
  { text: "> status: self-learning // always", delay: 1400 },
  { text: "> open_to: collaborations = true", delay: 1800 },
  { text: "> ready.", delay: 2200 },
];

export default function ErioluwaPersona() {
  const [activeMode, setActiveMode] = useState("solo");
  const [visibleLines, setVisibleLines] = useState([]);
  const [selectedSkill, setSelectedSkill] = useState(null);
  const [tick, setTick] = useState(true);
  const termDone = useRef(false);

  useEffect(() => {
    if (termDone.current) return;
    termDone.current = true;
    terminalLines.forEach(({ text, delay }) => {
      setTimeout(() => {
        setVisibleLines((prev) => [...prev, text]);
      }, delay);
    });
  }, []);

  useEffect(() => {
    const t = setInterval(() => setTick((v) => !v), 530);
    return () => clearInterval(t);
  }, []);

  const mode = modeData[activeMode];

  return (
    <div style={{
      minHeight: "100vh",
      background: "#0a0a0a",
      fontFamily: "'Courier New', 'Lucida Console', monospace",
      color: "#e0e0e0",
      padding: "0",
      margin: "0",
      overflow: "hidden",
    }}>
      {/* scanline overlay */}
      <div style={{
        position: "fixed", inset: 0, pointerEvents: "none", zIndex: 10,
        background: "repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.08) 2px, rgba(0,0,0,0.08) 4px)",
      }} />

      <div style={{
        maxWidth: 860,
        margin: "0 auto",
        padding: "2.5rem 1.5rem 4rem",
        position: "relative",
        zIndex: 1,
      }}>

        {/* Header stripe */}
        <div style={{
          display: "flex", alignItems: "center", gap: "0.7rem",
          marginBottom: "2.2rem",
        }}>
          <div style={{ display: "flex", gap: 6 }}>
            {["#ff5f57","#febc2e","#28c840"].map(c => (
              <div key={c} style={{ width:11, height:11, borderRadius:"50%", background:c }} />
            ))}
          </div>
          <div style={{
            flex: 1, height: 1, background: "rgba(255,255,255,0.08)",
          }} />
          <span style={{ fontSize: "0.65rem", color: "#444", letterSpacing: 2 }}>PERSONA.SH</span>
        </div>

        {/* Terminal block */}
        <div style={{
          background: "#0d0d0d",
          border: "1px solid #1e1e1e",
          borderRadius: 4,
          padding: "1.2rem 1.5rem",
          marginBottom: "2rem",
          minHeight: 170,
        }}>
          {visibleLines.map((line, i) => (
            <div key={i} style={{
              fontSize: "0.8rem",
              lineHeight: 2,
              color: line.startsWith("> ready") ? "#00DC82"
                : line.startsWith("> name") ? "#54C5F8"
                : line.startsWith("> role") ? "#ffffff"
                : "#aaa",
              animation: "fadeIn 0.2s ease",
            }}>
              {line}
            </div>
          ))}
          {visibleLines.length < terminalLines.length && (
            <span style={{ color: "#fff", opacity: tick ? 1 : 0 }}>█</span>
          )}
          {visibleLines.length >= terminalLines.length && (
            <span style={{ color: "#00DC82", opacity: tick ? 1 : 0 }}>█</span>
          )}
        </div>

        {/* Name + tagline */}
        <div style={{ marginBottom: "2.4rem" }}>
          <h1 style={{
            fontSize: "clamp(1.8rem, 5vw, 2.8rem)",
            fontWeight: 800,
            letterSpacing: -1,
            margin: 0,
            color: "#fff",
            lineHeight: 1.1,
            fontFamily: "Georgia, 'Times New Roman', serif",
          }}>
            Fawehinmi<br />
            <span style={{ color: "#444" }}>Erioluwa</span>
          </h1>
          <p style={{
            margin: "0.8rem 0 0",
            fontSize: "0.78rem",
            color: "#555",
            letterSpacing: 3,
            textTransform: "uppercase",
          }}>
            The first step to greatness is taking action
          </p>
        </div>

        {/* Mode switcher */}
        <div style={{ marginBottom: "2rem" }}>
          <div style={{
            fontSize: "0.6rem", color: "#333", letterSpacing: 3,
            textTransform: "uppercase", marginBottom: "0.6rem",
          }}>// operating mode</div>
          <div style={{ display: "flex", gap: "0.5rem", flexWrap: "wrap" }}>
            {modes.map((m) => (
              <button
                key={m}
                onClick={() => setActiveMode(m)}
                style={{
                  background: activeMode === m ? modeData[m].accent : "transparent",
                  color: activeMode === m ? "#000" : "#555",
                  border: `1px solid ${activeMode === m ? modeData[m].accent : "#222"}`,
                  borderRadius: 2,
                  padding: "0.3rem 0.8rem",
                  fontSize: "0.7rem",
                  cursor: "pointer",
                  letterSpacing: 2,
                  textTransform: "uppercase",
                  fontFamily: "inherit",
                  transition: "all 0.18s ease",
                  fontWeight: activeMode === m ? 700 : 400,
                }}
              >
                {m}
              </button>
            ))}
          </div>
        </div>

        {/* Mode card */}
        <div style={{
          border: `1px solid ${mode.accent}22`,
          borderLeft: `3px solid ${mode.accent}`,
          padding: "1.2rem 1.4rem",
          marginBottom: "2.4rem",
          background: `${mode.accent}06`,
          borderRadius: "0 3px 3px 0",
          transition: "all 0.3s ease",
        }}>
          <div style={{
            fontSize: "0.65rem", color: mode.accent,
            letterSpacing: 3, textTransform: "uppercase", marginBottom: "0.5rem",
          }}>{mode.label}</div>
          <p style={{ margin: "0 0 1rem", fontSize: "0.85rem", color: "#bbb", lineHeight: 1.7 }}>
            {mode.description}
          </p>
          <div style={{ display: "flex", gap: "0.5rem", flexWrap: "wrap" }}>
            {mode.traits.map(t => (
              <span key={t} style={{
                fontSize: "0.65rem",
                color: mode.accent,
                border: `1px solid ${mode.accent}40`,
                padding: "0.2rem 0.5rem",
                borderRadius: 2,
                letterSpacing: 1,
              }}>{t}</span>
            ))}
          </div>
        </div>

        {/* Skills grid */}
        <div style={{ marginBottom: "2.4rem" }}>
          <div style={{
            fontSize: "0.6rem", color: "#333", letterSpacing: 3,
            textTransform: "uppercase", marginBottom: "0.8rem",
          }}>// tech stack</div>
          <div style={{
            display: "grid",
            gridTemplateColumns: "repeat(auto-fill, minmax(80px, 1fr))",
            gap: "0.5rem",
          }}>
            {skills.map((s) => (
              <div
                key={s.name}
                onClick={() => setSelectedSkill(selectedSkill === s.name ? null : s.name)}
                style={{
                  border: selectedSkill === s.name
                    ? `1px solid ${s.color}`
                    : "1px solid #1a1a1a",
                  padding: "0.7rem 0.5rem",
                  borderRadius: 3,
                  textAlign: "center",
                  cursor: "pointer",
                  background: selectedSkill === s.name ? `${s.color}15` : "#0d0d0d",
                  transition: "all 0.18s ease",
                }}
              >
                <div style={{
                  width: 28, height: 28,
                  background: `${s.color}20`,
                  border: `1px solid ${s.color}40`,
                  borderRadius: 3,
                  display: "flex", alignItems: "center", justifyContent: "center",
                  margin: "0 auto 0.4rem",
                  fontSize: "0.65rem",
                  color: s.color,
                  fontWeight: 700,
                }}>
                  {s.icon}
                </div>
                <div style={{
                  fontSize: "0.55rem", color: selectedSkill === s.name ? s.color : "#444",
                  letterSpacing: 1,
                }}>{s.name}</div>
              </div>
            ))}
          </div>
        </div>

        {/* Projects */}
        <div style={{ marginBottom: "2.4rem" }}>
          <div style={{
            fontSize: "0.6rem", color: "#333", letterSpacing: 3,
            textTransform: "uppercase", marginBottom: "0.8rem",
          }}>// projects</div>
          <div style={{ display: "flex", flexDirection: "column", gap: "0.6rem" }}>
            {projects.map((p) => (
              <div key={p.name} style={{
                display: "flex",
                alignItems: "flex-start",
                gap: "1rem",
                border: "1px solid #1a1a1a",
                padding: "0.9rem 1.1rem",
                borderRadius: 3,
                background: "#0d0d0d",
              }}>
                <div style={{ flex: 1 }}>
                  <div style={{
                    fontSize: "0.8rem", color: "#ddd", fontWeight: 600, marginBottom: "0.2rem",
                  }}>{p.name}</div>
                  <div style={{ fontSize: "0.7rem", color: "#555", lineHeight: 1.5 }}>{p.desc}</div>
                </div>
                <span style={{
                  fontSize: "0.55rem",
                  color: p.tagColor,
                  border: `1px solid ${p.tagColor}50`,
                  padding: "0.15rem 0.4rem",
                  borderRadius: 2,
                  letterSpacing: 1,
                  textTransform: "uppercase",
                  whiteSpace: "nowrap",
                  flexShrink: 0,
                }}>{p.tag}</span>
              </div>
            ))}
          </div>
        </div>

        {/* Footer / contact */}
        <div style={{
          borderTop: "1px solid #1a1a1a",
          paddingTop: "1.4rem",
          display: "flex",
          alignItems: "center",
          justifyContent: "space-between",
          flexWrap: "wrap",
          gap: "1rem",
        }}>
          <div style={{ fontSize: "0.65rem", color: "#333", letterSpacing: 2 }}>
            17 · open to collabs · self-taught
          </div>
          <a
            href="mailto:erioluwafawehinmi@gmail.com"
            style={{
              fontSize: "0.65rem",
              color: "#fff",
              background: "#111",
              border: "1px solid #2a2a2a",
              padding: "0.4rem 0.8rem",
              borderRadius: 2,
              textDecoration: "none",
              letterSpacing: 2,
              textTransform: "uppercase",
              transition: "border-color 0.2s",
            }}
          >
            → email
          </a>
        </div>

      </div>

      <style>{`
        @keyframes fadeIn { from { opacity:0; transform:translateY(2px); } to { opacity:1; transform:none; } }
        * { box-sizing: border-box; }
        ::-webkit-scrollbar { width: 4px; background: #0a0a0a; }
        ::-webkit-scrollbar-thumb { background: #1e1e1e; }
      `}</style>
    </div>
  );
}
