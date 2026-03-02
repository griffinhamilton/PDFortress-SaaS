# 🔒 PDFortress

**Your documents. Your rules. Your fortress.**

PDFortress is a secure, cloud-hosted PDF document viewer built for creators, educators, consultants, and businesses who distribute premium or confidential content to controlled audiences — without the risk of casual downloading, sharing, screenshotting, or redistribution.

🚀 *Designed, built, and deployed in under 40 hours — from first commit to production — by a **solo non-engineer** in February 2026 as a complete multi-tenant SaaS platform in a single sprint, **demonstrating rapid delivery of complex, security-focused web applications for clients requiring unique technical solutions.***

Unlike traditional PDF viewers, flipbook tools, or basic DRM plugins, PDFortress combines **document security, access control, identity-tagged watermarking, and a premium flipbook reading experience** into a single platform. No other solution on the market does all of this in one go.

---

## 🧬 How It Works

PDFortress never exposes a downloadable PDF to the end user.

1. Authenticated members receive a **short-lived signed URL** (60-second expiry) that fetches the PDF from private storage
2. The PDF is loaded via Mozilla's pdf.js and **rendered page-by-page onto HTML5 canvas elements**
3. **Identity-tagged watermarks** are drawn onto each canvas in real time — displaying the viewer's email, name, and licensing info on every page
4. The watermarked canvases are displayed inside an **interactive flipbook viewer** with realistic page-turning animations

There is no download button, no "Save As" option, and no persistent PDF URL. The signed URL expires before most users could even find it in their network tab.

> **Roadmap note:** Server-side watermark baking (burning watermarks into the PDF binary before delivery) is planned for a future hardened release. The current architecture provides strong deterrence and traceability for the vast majority of use cases.

---

## ✨ Core Features

### 🔐 Security & Access Control
- **Magic link authentication** — passwordless, single-use, time-limited email verification via Resend
- **Multi-tenant architecture** — fully isolated organizations, each with their own admins, courses, members, and configurations
- **Cross-course session poisoning protection** — tokens are scoped per-document; mismatched access attempts destroy the session and force re-authentication
- **Row-Level Security (RLS)** on all database tables — even exposed Supabase API keys can't query unauthorized data
- **60-second signed URLs** for PDF delivery — short-lived and useless if shared

### 🎨 Multi-Layer Canvas Watermarking
Every rendered page displays **five watermark layers** drawn onto the canvas in real time:
1. **Diagonal tiled text** — member email + name repeated across the full page (configurable opacity, scale, rotation, density)
2. **Center watermark** — large, semi-transparent visual deterrent
3. **Header attribution bar** — document title and licensing info
4. **Footer attribution bar** — "Protected Document – Licensed to [member email]"
5. **Custom organization logo** (optional) — branded overlay for instant leak identification

Any screenshot, screen recording, or photo of the screen will contain the viewer's identity embedded across every visible page.

### 📖 Interactive Flipbook Viewer
Documents are presented as beautiful, interactive flipbooks — not static PDF embeds:
- **Realistic page-turning animations** with click, drag, swipe, and keyboard navigation
- **Two-page spread** on desktop (landscape); **single-page portrait** on mobile
- **Pinch-to-zoom** and double-tap reset on touch devices
- **Fullscreen mode** for immersive, distraction-free reading
- **Viewport-locked sizing algorithm** — mathematically calculated to fit any screen perfectly with no overflow or scrolling

### 📸 Screenshot Detection & Deterrence
- Monitors for PrintScreen, Cmd+Shift+3/4, Ctrl+Shift+S, and other common screenshot key combinations
- Detects browser tab visibility changes during screenshot workflows
- Triggers a **full-screen red warning overlay** with an intimidation message
- All screenshot events are **logged server-side** with session ID and document ID for audit trails
- Combined with per-user watermarking: even successful screenshots are traceable back to the specific viewer

### ⏱️ Access Scheduling & Permissions
- Set **live access windows** (start date / end date) per course — documents become inaccessible outside the window
- Grant **special override permissions** for individual users to bypass time restrictions when needed
- Access schedule is displayed to members on the login page for full transparency

### 👥 Member Management & Automation
- Add members individually by email or via **bulk CSV upload**
- **Webhook integrations** for automated member provisioning from external platforms (Skool, Zapier, Make, etc.)
- Members can belong to multiple courses across multiple organizations

### 🏢 Multi-Organization Admin Dashboard
- Role-based access control (owner / admin)
- **Organization switcher** for admins managing multiple tenants
- Per-organization watermark configuration, branding, and team management
- Custom logo upload for branded watermark overlays
- Course management with document upload, member lists, and scheduling controls

### 🧩 Embeddable Viewer
- **Iframe-ready** — embed the secure flipbook viewer directly into any third-party platform, LMS, or website
- All security features (watermarking, session scoping, screenshot detection) remain fully active in embedded mode

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18 + Vite (TypeScript) |
| Styling | Tailwind CSS |
| Backend / Database | Supabase (PostgreSQL + Row-Level Security) |
| Serverless Functions | Supabase Edge Functions (Deno) |
| PDF Rendering | pdf.js (Mozilla) |
| Flipbook Engine | react-pageflip |
| Pinch-to-Zoom | react-zoom-pan-pinch |
| Email Delivery | Resend |
| Hosting | Vercel |

---

## 🚫 What PDFortress Is NOT

- ❌ A file-sharing tool
- ❌ A standard PDF viewer with a disabled right-click
- ❌ A wrapper or plugin that depends on someone else's platform to function
- ❌ A solution that relies solely on HTML overlays removable with DevTools

PDFortress is a **purpose-built document security platform** where every architectural decision — from canvas rendering to session management to identity-tagged watermarking — exists to protect your content and trace any leaks back to their source.

---

## 🗺️ Potential Roadmap

- [ ] Server-side watermark baking (pdf-lib) — burn watermarks into the PDF binary before delivery for hardened security
- [ ] Analytics dashboard — view-counts, session duration, and access heatmaps per document
- [ ] Device limit enforcement — per-device session fingerprinting to restrict concurrent access
- [ ] Granular page-level permissions — restrict access to specific pages within a document
- [ ] Custom expiry per magic link
- [ ] **Your feature here** — PDFortress was built for clients with unique problems. The roadmap is driven by what you need.

---

## 📬 Contact

Source code is private. For demos, licensing inquiries, or partnership opportunities:

**Griffin A. Hamilton** — [GitHub](https://github.com/griffinhamilton) — [LinkedIn®](https://www.linkedin.com/in/griffinahamilton/)

---

*From first commit to production in under 40 hours. Solo.*
