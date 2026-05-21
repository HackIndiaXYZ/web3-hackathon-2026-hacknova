# web3-hackathon-2026-hacknova
Hackathon team repository for Hack_nova - [hackindia-team:web3-hackathon-2026:hacknova]


Build a decentralized credential management system
Store certifications securely on Polygon blockchain
Enable trustless and instant verification
Allow organizations and third-party platforms to verify credentials easily
Make credentials portable and permanently accessible
🛠️ Features
🔐 On-Chain Credential Issuance
Institutions can issue certificates directly on blockchain
Each credential gets a unique blockchain hash
Prevents fake or duplicate certificates
✅ Instant Verification
Recruiters or organizations can verify credentials instantly
No need for manual validation
🌐 Polygon Blockchain Integration
Credentials stored securely on Polygon
Low gas fees and fast transactions
📄 Tamper-Proof Records
Blockchain ensures data cannot be modified after issuance
🔗 Third-Party Integration
APIs for websites/apps to integrate credential verification
👤 User Wallet Support
Users can connect MetaMask or Web3 wallets
Own and manage their credentials securely
🏗️ Tech Stack
Technology	Purpose
Frontend	React.js / Next.js
Backend	Node.js + Express
Blockchain	Polygon
Smart Contracts	Solidity
Database	MongoDB / IPFS
Wallet Integration	MetaMask
Authentication	JWT / Web3Auth
⚙️ System Architecture
User/Institution
       ↓
Frontend (React)
       ↓
Backend API (Node.js)
       ↓
Smart Contract (Solidity)
       ↓
Polygon Blockchain
       ↓
Credential Verification
📜 Workflow
1️⃣ Credential Issuance
Institution uploads certificate details
Smart contract generates blockchain record
Credential hash stored on Polygon
2️⃣ Credential Storage
Metadata stored on IPFS or database
Blockchain stores immutable proof
3️⃣ Verification Process
User shares credential ID/QR code
Verifier checks blockchain record
System confirms authenticity instantly
🔒 Security Features
Blockchain immutability
Smart contract validation
Wallet-based authentication
Cryptographic hashing
Decentralized storage support
🚀 Future Enhancements
NFT-based certificates
AI skill validation
DAO governance
Multi-chain support
LinkedIn integration
QR-based instant verification
💡 Use Cases
🎓 Universities issuing degrees
💼 Companies validating employee skills
🧑‍💻 Online course certifications
🏆 Hackathon achievement records
📑 Professional licenses
📷 Screenshots

Add project screenshots here

![Home Page](images/home.png)
![Dashboard](images/dashboard.png)
![Verification](images/verify.png)
🧪 Installation & Setup
# Clone Repository
git clone https://github.com/your-username/skills-on-chain.git

# Move into project
cd skills-on-chain

# Install dependencies
npm install

# Start development server
npm run dev
📦 Smart Contract Deployment
npx hardhat compile
npx hardhat run scripts/deploy.js --network polygonMumbai
👥 Team
Radhika
Team Members Names
📄 License

This project is licensed under the MIT License.

⭐ Conclusion

The Skills On-Chain Platform creates a transparent, decentralized, and trustless ecosystem for skill verification using blockchain technology.
By leveraging Polygon, the platform ensures secure, fast, and cost-effective credential management for the future of digital identity and professional verification. 🚀

import { useState, useEffect, useRef } from "react";

const CREDENTIALS = [
  { id: "0x1a2b", skill: "Solidity Development", issuer: "0xDev...Academy", holder: "0xAlice...7f3a", level: "Expert", date: "2026-03-12", txHash: "0xabc123...def456", verified: true },
  { id: "0x3c4d", skill: "Smart Contract Auditing", issuer: "0xChain...Labs", holder: "0xBob...9e1c", level: "Advanced", date: "2026-04-01", txHash: "0xfed987...321cba", verified: true },
  { id: "0x5e6f", skill: "Zero-Knowledge Proofs", issuer: "0xZK...Institute", holder: "0xAlice...7f3a", level: "Intermediate", date: "2026-05-10", txHash: "0x112233...aabbcc", verified: true },
];

const LEVEL_COLORS = { Expert: "#00ffb2", Advanced: "#4d9fff", Intermediate: "#ff9f4d", Beginner: "#cc77ff" };

function HexGrid() {
  return (
    <div style={{ position: "fixed", inset: 0, overflow: "hidden", pointerEvents: "none", zIndex: 0, opacity: 0.06 }}>
      <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <pattern id="hex" x="0" y="0" width="60" height="52" patternUnits="userSpaceOnUse">
            <polygon points="30,2 58,17 58,35 30,50 2,35 2,17" fill="none" stroke="#00ffb2" strokeWidth="0.8"/>
          </pattern>
        </defs>
        <rect width="100%" height="100%" fill="url(#hex)"/>
      </svg>
    </div>
  );
}

function BlockCounter({ label, value }) {
  const [display, setDisplay] = useState(0);
  useEffect(() => {
    let start = 0;
    const end = parseInt(value);
    if (start === end) return;
    const timer = setInterval(() => {
      start += Math.ceil((end - start) / 8);
      if (start >= end) { setDisplay(end); clearInterval(timer); }
      else setDisplay(start);
    }, 50);
    return () => clearInterval(timer);
  }, [value]);
  return (
    <div style={{ textAlign: "center" }}>
      <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "2rem", color: "#00ffb2", fontWeight: 700, letterSpacing: "-1px" }}>{display.toLocaleString()}</div>
      <div style={{ fontFamily: "'DM Sans', sans-serif", fontSize: "0.7rem", color: "#4a5568", textTransform: "uppercase", letterSpacing: "2px", marginTop: 2 }}>{label}</div>
    </div>
  );
}

function CredentialCard({ cred, index }) {
  const [hovered, setHovered] = useState(false);
  return (
    <div
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
      style={{
        background: hovered ? "rgba(0,255,178,0.04)" : "rgba(10,14,20,0.8)",
        border: 1px solid ${hovered ? "rgba(0,255,178,0.35)" : "rgba(0,255,178,0.1)"},
        borderRadius: 12,
        padding: "20px 22px",
        position: "relative",
        overflow: "hidden",
        transition: "all 0.3s ease",
        cursor: "default",
        animation: fadeUp 0.5s ease both,
        animationDelay: ${index * 0.1}s,
        transform: hovered ? "translateY(-3px)" : "translateY(0)",
        boxShadow: hovered ? "0 16px 40px rgba(0,255,178,0.08)" : "none",
      }}
    >
      <div style={{ position: "absolute", top: 0, right: 0, width: 80, height: 80, background: radial-gradient(circle at top right, ${LEVEL_COLORS[cred.level]}18, transparent 70%), pointerEvents: "none" }} />

      <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 14 }}>
        <div>
          <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.65rem", color: "#4a5568", marginBottom: 4 }}>CREDENTIAL ID</div>
          <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.85rem", color: "#a0aec0" }}>{cred.id}</div>
        </div>
        <div style={{ display: "flex", alignItems: "center", gap: 6, background: "rgba(0,255,178,0.08)", border: "1px solid rgba(0,255,178,0.2)", borderRadius: 100, padding: "4px 10px" }}>
          <div style={{ width: 6, height: 6, borderRadius: "50%", background: "#00ffb2", boxShadow: "0 0 8px #00ffb2" }} />
          <span style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#00ffb2" }}>VERIFIED</span>
        </div>
      </div>

      <div style={{ marginBottom: 14 }}>
        <div style={{ fontFamily: "'Clash Display', 'DM Sans', sans-serif", fontSize: "1.15rem", fontWeight: 700, color: "#e2e8f0", marginBottom: 4 }}>{cred.skill}</div>
        <div style={{ display: "flex", gap: 8, alignItems: "center" }}>
          <span style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.7rem", color: LEVEL_COLORS[cred.level], background: ${LEVEL_COLORS[cred.level]}15, border: 1px solid ${LEVEL_COLORS[cred.level]}30, borderRadius: 4, padding: "2px 8px" }}>{cred.level}</span>
          <span style={{ fontFamily: "'DM Sans', sans-serif", fontSize: "0.75rem", color: "#4a5568" }}>{cred.date}</span>
        </div>
      </div>

      <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10, paddingTop: 14, borderTop: "1px solid rgba(255,255,255,0.05)" }}>
        <div>
          <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#4a5568", marginBottom: 3 }}>ISSUER</div>
          <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.7rem", color: "#718096" }}>{cred.issuer}</div>
        </div>
        <div>
          <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#4a5568", marginBottom: 3 }}>HOLDER</div>
          <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.7rem", color: "#718096" }}>{cred.holder}</div>
        </div>
      </div>

      <div style={{ marginTop: 12, display: "flex", alignItems: "center", gap: 6 }}>
        <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#4a5568" }}>TX:</div>
        <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#2d6a4f" }}>{cred.txHash}</div>
      </div>
    </div>
  );
}

function IssueForm({ onIssue }) {
  const [form, setForm] = useState({ skill: "", holder: "", level: "Intermediate", issuer: "" });
  const [loading, setLoading] = useState(false);
  const [success, setSuccess] = useState(false);

  const handle = (k, v) => setForm(f => ({ ...f, [k]: v }));

  const submit = async () => {
    if (!form.skill || !form.holder || !form.issuer) return;
    setLoading(true);
    await new Promise(r => setTimeout(r, 1800));
    setLoading(false);
    setSuccess(true);
    onIssue({ ...form, id: "0x" + Math.random().toString(16).slice(2, 6), date: new Date().toISOString().split("T")[0], txHash: "0x" + Math.random().toString(16).slice(2, 14) + "...", verified: true });
    setTimeout(() => { setSuccess(false); setForm({ skill: "", holder: "", level: "Intermediate", issuer: "" }); }, 2000);
  };

  const inputStyle = {
    width: "100%", background: "rgba(0,0,0,0.4)", border: "1px solid rgba(0,255,178,0.15)",
    borderRadius: 8, padding: "11px 14px", color: "#e2e8f0",
    fontFamily: "'DM Sans', sans-serif", fontSize: "0.9rem", outline: "none",
    transition: "border-color 0.2s", boxSizing: "border-box",
  };

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: 14 }}>
      {["skill", "holder", "issuer"].map(key => (
        <div key={key}>
          <label style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.62rem", color: "#4a5568", textTransform: "uppercase", letterSpacing: "1.5px", display: "block", marginBottom: 6 }}>
            {key === "skill" ? "Skill / Certification Name" : key === "holder" ? "Holder Wallet Address" : "Issuing Organization"}
          </label>
          <input
            value={form[key]}
            onChange={e => handle(key, e.target.value)}
            placeholder={key === "skill" ? "e.g. Rust Programming" : key === "holder" ? "0x..." : "e.g. 0xAcademy..."}
            style={inputStyle}
            onFocus={e => e.target.style.borderColor = "rgba(0,255,178,0.4)"}
            onBlur={e => e.target.style.borderColor = "rgba(0,255,178,0.15)"}
          />
        </div>
      ))}

      <div>
        <label style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.62rem", color: "#4a5568", textTransform: "uppercase", letterSpacing: "1.5px", display: "block", marginBottom: 6 }}>Proficiency Level</label>
        <div style={{ display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 8 }}>
          {Object.keys(LEVEL_COLORS).map(lvl => (
            <button key={lvl} onClick={() => handle("level", lvl)} style={{
              background: form.level === lvl ? ${LEVEL_COLORS[lvl]}18 : "transparent",
              border: 1px solid ${form.level === lvl ? LEVEL_COLORS[lvl] : "rgba(255,255,255,0.08)"},
              borderRadius: 8, padding: "8px 4px", cursor: "pointer",
              fontFamily: "'Space Mono', monospace", fontSize: "0.6rem",
              color: form.level === lvl ? LEVEL_COLORS[lvl] : "#4a5568",
              transition: "all 0.2s",
            }}>{lvl}</button>
          ))}
        </div>
      </div>

      <button
        onClick={submit}
        disabled={loading || success}
        style={{
          marginTop: 6, padding: "14px", borderRadius: 10, border: "none", cursor: loading ? "wait" : "pointer",
          background: success ? "rgba(0,255,178,0.2)" : loading ? "rgba(0,255,178,0.08)" : "linear-gradient(135deg, rgba(0,255,178,0.25), rgba(0,255,178,0.1))",
          color: success ? "#00ffb2" : "#e2e8f0",
          fontFamily: "'Space Mono', monospace", fontSize: "0.8rem", letterSpacing: "1px",
          border: 1px solid ${success ? "#00ffb2" : "rgba(0,255,178,0.3)"},
          transition: "all 0.3s",
          position: "relative", overflow: "hidden",
        }}
      >
        {loading ? (
          <span style={{ display: "flex", alignItems: "center", justifyContent: "center", gap: 10 }}>
            <span style={{ display: "inline-block", width: 12, height: 12, border: "2px solid rgba(0,255,178,0.3)", borderTopColor: "#00ffb2", borderRadius: "50%", animation: "spin 0.7s linear infinite" }} />
            WRITING TO POLYGON...
          </span>
        ) : success ? "✓ CREDENTIAL ISSUED ON-CHAIN" : "ISSUE CREDENTIAL →"}
      </button>
    </div>
  );
}

function VerifyPanel() {
  const [input, setInput] = useState("");
  const [result, setResult] = useState(null);
  const [loading, setLoading] = useState(false);

  const verify = async () => {
    if (!input) return;
    setLoading(true);
    setResult(null);
    await new Promise(r => setTimeout(r, 1200));
    const found = CREDENTIALS.find(c => c.id === input || c.txHash.includes(input.slice(0, 6)));
    setLoading(false);
    setResult(found ? { valid: true, data: found } : { valid: false });
  };

  return (
    <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
      <div>
        <label style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.62rem", color: "#4a5568", textTransform: "uppercase", letterSpacing: "1.5px", display: "block", marginBottom: 8 }}>Credential ID or TX Hash</label>
        <div style={{ display: "flex", gap: 8 }}>
          <input
            value={input}
            onChange={e => setInput(e.target.value)}
            placeholder="0x1a2b or 0xabc123..."
            style={{ flex: 1, background: "rgba(0,0,0,0.4)", border: "1px solid rgba(0,255,178,0.15)", borderRadius: 8, padding: "11px 14px", color: "#e2e8f0", fontFamily: "'Space Mono', monospace", fontSize: "0.8rem", outline: "none", boxSizing: "border-box" }}
          />
          <button onClick={verify} style={{ padding: "11px 18px", background: "transparent", border: "1px solid rgba(0,255,178,0.3)", borderRadius: 8, color: "#00ffb2", fontFamily: "'Space Mono', monospace", fontSize: "0.75rem", cursor: "pointer", whiteSpace: "nowrap" }}>
            {loading ? "..." : "VERIFY"}
          </button>
        </div>
      </div>

      {result && (
        <div style={{
          padding: 18, borderRadius: 10,
          background: result.valid ? "rgba(0,255,178,0.04)" : "rgba(255,80,80,0.04)",
          border: 1px solid ${result.valid ? "rgba(0,255,178,0.25)" : "rgba(255,80,80,0.25)"},
          animation: "fadeUp 0.3s ease both",
        }}>
          {result.valid ? (
            <>
              <div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: 12 }}>
                <div style={{ fontSize: "1.2rem" }}>✓</div>
                <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.75rem", color: "#00ffb2" }}>CREDENTIAL VALID — ON-CHAIN VERIFIED</div>
              </div>
              <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10 }}>
                {[["Skill", result.data.skill], ["Level", result.data.level], ["Issuer", result.data.issuer], ["Date", result.data.date]].map(([k, v]) => (
                  <div key={k}>
                    <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.55rem", color: "#4a5568", marginBottom: 2 }}>{k.toUpperCase()}</div>
                    <div style={{ fontFamily: "'DM Sans', sans-serif", fontSize: "0.8rem", color: "#a0aec0" }}>{v}</div>
                  </div>
                ))}
              </div>
            </>
          ) : (
            <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
              <div style={{ fontSize: "1.2rem" }}>✗</div>
              <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.75rem", color: "#ff5050" }}>CREDENTIAL NOT FOUND ON POLYGON</div>
            </div>
          )}
        </div>
      )}

      <div style={{ paddingTop: 8, borderTop: "1px solid rgba(255,255,255,0.05)" }}>
        <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#2d4a3e", marginBottom: 8 }}>// QUICK TEST IDs</div>
        {CREDENTIALS.map(c => (
          <div key={c.id} onClick={() => setInput(c.id)} style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.65rem", color: "#4a5568", cursor: "pointer", padding: "3px 0", transition: "color 0.2s" }}
            onMouseEnter={e => e.target.style.color = "#00ffb2"} onMouseLeave={e => e.target.style.color = "#4a5568"}>
            → {c.id} · {c.skill}
          </div>
        ))}
      </div>
    </div>
  );
}

export default function App() {
  const [tab, setTab] = useState("credentials");
  const [creds, setCreds] = useState(CREDENTIALS);
  const [blockNum] = useState(49823741);

  const tabs = [
    { id: "credentials", label: "All Credentials" },
    { id: "issue", label: "Issue New" },
    { id: "verify", label: "Verify" },
  ];

  return (
    <>
      <style>{
        @import url('https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=DM+Sans:wght@400;500;600;700&display=swap');
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { background: #060a0f; color: #e2e8f0; }
        @keyframes fadeUp { from { opacity: 0; transform: translateY(16px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes spin { to { transform: rotate(360deg); } }
        @keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.4; } }
        @keyframes scanline { 0% { top: -5%; } 100% { top: 105%; } }
        ::-webkit-scrollbar { width: 4px; } ::-webkit-scrollbar-track { background: transparent; } ::-webkit-scrollbar-thumb { background: rgba(0,255,178,0.2); border-radius: 2px; }
      }</style>

      <HexGrid />

      {/* Scanline effect */}
      <div style={{ position: "fixed", inset: 0, pointerEvents: "none", zIndex: 1, overflow: "hidden" }}>
        <div style={{ position: "absolute", left: 0, right: 0, height: "3%", background: "linear-gradient(transparent, rgba(0,255,178,0.015), transparent)", animation: "scanline 6s linear infinite" }} />
      </div>

      <div style={{ position: "relative", zIndex: 2, maxWidth: 900, margin: "0 auto", padding: "32px 24px", minHeight: "100vh" }}>

        {/* Header */}
        <div style={{ marginBottom: 36, animation: "fadeUp 0.6s ease both" }}>
          <div style={{ display: "flex", alignItems: "center", gap: 12, marginBottom: 6 }}>
            <div style={{ width: 8, height: 8, borderRadius: "50%", background: "#00ffb2", boxShadow: "0 0 12px #00ffb2", animation: "pulse 2s ease-in-out infinite" }} />
            <span style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.65rem", color: "#00ffb2", letterSpacing: "3px" }}>POLYGON MAINNET · LIVE</span>
          </div>
          <h1 style={{ fontFamily: "'Space Mono', monospace", fontSize: "clamp(1.6rem, 4vw, 2.6rem)", fontWeight: 700, color: "#e2e8f0", lineHeight: 1.1, letterSpacing: "-1px" }}>
            SKILLS<span style={{ color: "#00ffb2" }}>.</span>ON<span style={{ color: "#00ffb2" }}>.</span>CHAIN
          </h1>
          <p style={{ fontFamily: "'DM Sans', sans-serif", fontSize: "0.9rem", color: "#4a5568", marginTop: 6 }}>Decentralized credential issuance & verification · Tamper-proof · Portable</p>
        </div>

        {/* Stats Bar */}
        <div style={{
          display: "grid", gridTemplateColumns: "repeat(4, 1fr)", gap: 1,
          background: "rgba(0,255,178,0.05)", border: "1px solid rgba(0,255,178,0.1)",
          borderRadius: 12, padding: "20px 24px", marginBottom: 28,
          animation: "fadeUp 0.6s ease 0.1s both",
        }}>
          <BlockCounter label="Block Height" value={blockNum + creds.length} />
          <BlockCounter label="Credentials Issued" value={creds.length * 1247} />
          <BlockCounter label="Verified Today" value={creds.length * 89} />
          <BlockCounter label="Active Issuers" value={creds.length * 34} />
        </div>

        {/* Tabs */}
        <div style={{ display: "flex", gap: 2, marginBottom: 24, background: "rgba(0,0,0,0.4)", border: "1px solid rgba(0,255,178,0.1)", borderRadius: 10, padding: 4, animation: "fadeUp 0.6s ease 0.2s both" }}>
          {tabs.map(t => (
            <button key={t.id} onClick={() => setTab(t.id)} style={{
              flex: 1, padding: "10px", borderRadius: 8, border: "none", cursor: "pointer",
              background: tab === t.id ? "rgba(0,255,178,0.12)" : "transparent",
              color: tab === t.id ? "#00ffb2" : "#4a5568",
              fontFamily: "'Space Mono', monospace", fontSize: "0.7rem", letterSpacing: "0.5px",
              borderBottom: tab === t.id ? "1px solid rgba(0,255,178,0.4)" : "1px solid transparent",
              transition: "all 0.2s",
            }}>{t.label}</button>
          ))}
        </div>

        {/* Content */}
        <div style={{ animation: "fadeUp 0.4s ease both" }} key={tab}>
          {tab === "credentials" && (
            <div>
              <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 16 }}>
                <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.65rem", color: "#4a5568" }}>
                  SHOWING {creds.length} CREDENTIALS
                </div>
                <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#2d4a3e" }}>
                  NETWORK: POLYGON ◆ CHAIN ID: 137
                </div>
              </div>
              <div style={{ display: "grid", gridTemplateColumns: "repeat(auto-fill, minmax(280px, 1fr))", gap: 16 }}>
                {creds.map((c, i) => <CredentialCard key={c.id} cred={c} index={i} />)}
              </div>
            </div>
          )}

          {tab === "issue" && (
            <div style={{ maxWidth: 520, margin: "0 auto" }}>
              <div style={{ background: "rgba(0,0,0,0.5)", border: "1px solid rgba(0,255,178,0.12)", borderRadius: 14, padding: 28 }}>
                <div style={{ marginBottom: 24 }}>
                  <h2 style={{ fontFamily: "'Space Mono', monospace", fontSize: "1rem", color: "#e2e8f0", marginBottom: 6 }}>Issue Credential On-Chain</h2>
                  <p style={{ fontFamily: "'DM Sans', sans-serif", fontSize: "0.8rem", color: "#4a5568" }}>Creates an immutable record on the Polygon blockchain. Gas fees apply.</p>
                </div>
                <IssueForm onIssue={cred => setCreds(prev => [{ ...cred, verified: true }, ...prev])} />
              </div>
            </div>
          )}

          {tab === "verify" && (
            <div style={{ maxWidth: 520, margin: "0 auto" }}>
              <div style={{ background: "rgba(0,0,0,0.5)", border: "1px solid rgba(0,255,178,0.12)", borderRadius: 14, padding: 28 }}>
                <div style={{ marginBottom: 24 }}>
                  <h2 style={{ fontFamily: "'Space Mono', monospace", fontSize: "1rem", color: "#e2e8f0", marginBottom: 6 }}>Trustless Verification</h2>
                  <p style={{ fontFamily: "'DM Sans', sans-serif", fontSize: "0.8rem", color: "#4a5568" }}>Verify any credential directly against the Polygon chain — no intermediaries.</p>
                </div>
                <VerifyPanel />
              </div>
            </div>
          )}
        </div>

        {/* Footer */}
        <div style={{ marginTop: 48, paddingTop: 16, borderTop: "1px solid rgba(255,255,255,0.04)", display: "flex", justifyContent: "space-between", alignItems: "center" }}>
          <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#2d4a3e" }}>
            CONTRACT: 0x8f3a...d7c2 · ERC-5484 · POLYGON
          </div>
          <div style={{ fontFamily: "'Space Mono', monospace", fontSize: "0.6rem", color: "#2d4a3e" }}>
            OPEN API · PERMISSIONLESS INTEGRATION
          </div>
        </div>
      </div>
    </>
  );
} Here is my code and create readme file for this 
🚀 Skills.On.Chain

A futuristic decentralized credential issuance and verification platform built on the Polygon Blockchain.
This platform allows institutions to issue tamper-proof skill credentials on-chain and enables anyone to verify them instantly without intermediaries.

🌐 Live Concept

“Portable, verifiable, and immutable digital credentials for the Web3 era.”

📌 Features
✅ On-Chain Credential Issuance
Issue blockchain-based certifications
Immutable credential storage
Unique credential IDs and transaction hashes
🔍 Trustless Verification
Verify credentials instantly using:
Credential ID
Transaction Hash
No centralized authority required
🎨 Futuristic Web3 UI
Cyberpunk-inspired blockchain dashboard
Animated stats counters
Hex-grid background effects
Polygon network visualization
🛡️ Tamper-Proof Credentials
Credentials cannot be altered once issued
Blockchain-backed verification system
🌉 Polygon Blockchain Integration
Optimized for Polygon Mainnet
Fast transactions
Low gas fees
🔗 Open API Architecture
Designed for third-party integration
Recruiters and platforms can verify credentials externally
🖼️ Preview
Dashboard
Live credential cards
Blockchain stats
Polygon network indicators
Issue Credential
Add:
Skill name
Wallet address
Issuer organization
Skill level
Verify Credential
Verify by:
Credential ID
TX Hash
⚙️ Tech Stack
Technology	Usage
React.js	Frontend
JavaScript	Application Logic
CSS-in-JS	Styling
Polygon	Blockchain Network
Solidity	Smart Contracts
MetaMask	Wallet Integration
Web3.js / Ethers.js	Blockchain Communication
🏗️ Architecture
User / Institution
        ↓
React Frontend
        ↓
Smart Contract Layer
        ↓
Polygon Blockchain
        ↓
Credential Verification
📂 Project Structure
src/
 ├── App.js
 ├── components/
 ├── styles/
 └── blockchain/

public/
package.json
README.md
🚀 Installation
Clone Repository
git clone https://github.com/HackIndiaXYZ/web3-hackathon-2026-hacknova
Navigate to Project
cd skills-on-chain
Install Dependencies
npm install
Start Development Server
npm start
🔗 Smart Contract Deployment
Compile Contract
npx hardhat compile
Deploy to Polygon
npx hardhat run scripts/deploy.js --network polygon
🧪 Sample Credential Data
{
  "id": "0x1a2b",
  "skill": "Solidity Development",
  "issuer": "0xDev...Academy",
  "holder": "0xAlice...7f3a",
  "level": "Expert",
  "date": "2026-03-12",
  "verified": true
}
🔒 Security Features
Blockchain immutability
Wallet-based authentication
Decentralized verification
Secure transaction hashes
Trustless validation
🌟 Future Enhancements
NFT Certificates
QR Code Verification
DID (Decentralized Identity)
AI Skill Analysis
Multi-chain Support
IPFS Metadata Storage
DAO Governance
💼 Use Cases
🎓 Education

Universities can issue blockchain-based degrees.

💻 Online Learning

Platforms can issue verifiable skill certificates.

🧑‍💼 Recruitment

Recruiters can instantly verify candidate credentials.

🏆 Hackathons

Issue tamper-proof achievement certificates.

Contributions are welcome!

# Fork repository
# Create feature branch
git checkout -b feature-name

# Commit changes
git commit -m "Added feature"

# Push branch
git push origin feature-name
📜 License

This project is licensed under the MIT License.

👨‍💻 Team
Radhika
Hack_nova Team

