### Phase 1: Zero-to-Low-Cost Launch (Right Now)

Get your game services running using a cheap or free DNS setup.

* **Primary DNS / Game Services:** Buy **`aetheria.zone`** (~$2–$4 for Year 1) or **`aetheria.xyz`** (~$1.50–$2 for Year 1) on budget-friendly registrars like **Porkbun** or **Spaceship**.
* **Backend Infrastructure:** Route subdomains to your free backend providers:
* `api.aetheria.zone` $\rightarrow$ Vercel / Render (Handles game auth and master server API with free SSL)
* `play.aetheria.zone` $\rightarrow$ Points to your game server host or dynamic DNS (e.g., DuckDNS)


* **Public Storefront:** Use `aetheria.itch.io` for game downloads, community updates, and player feedback. It carries high credibility with indie gamers and costs $0.

---

### Phase 2: Building Community (Pre-Revenue)

Once your game builds initial momentum, anchor player identity on free community channels rather than paid web real estate:

* **Community Hub:** Rely heavily on Discord (`discord.gg/yourgame`) to handle voice chat, community building, and player support.
* **Developer Log:** Keep hosting patch notes and documentation via **GitHub Pages** (`aetheria.github.io`) or Itch.io.

---

### Phase 3: Brand Upgrade (Post-Revenue)

Once players start buying in-game cosmetics, supporter packs, or subscriptions, invest in long-term brand assets:

1. **Acquire a Premium TLD:** Purchase `aetheria.gg` or a modified `.com` domain (e.g., `playaetheria.com` or `aetheriavr.com`) for roughly $10–$30/year.
2. **Setup 301 Redirects:** Point all old URLs (`aetheria.zone`) straight to the new primary domain (`playaetheria.com`).
3. **Keep `aetheria.zone` Active:** Maintain the `.zone` domain purely for backend server routing so existing game clients don't drop connections when you switch your main marketing website.

---

### Long-Term Architecture Map

```
                     ┌─────────────────────────────────────────────────────────┐
                     │                Player-Facing Front End                  │
                     │   playaetheria.com  (or aetheria.gg when profitable)    │
                     └────────────────────────────┬────────────────────────────┘
                                                  │
                                                  ▼
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│                                Persistent Game Backend                                  │
├─────────────────────────────────────────┬────────────────────────────────────────────────┤
│ Subdomain Routing                       │ Target Service                                 │
├─────────────────────────────────────────┼────────────────────────────────────────────────┤
│ `api.aetheria.zone`                     │ Vercel / Render (Auth & Master API)            │
│ `server.aetheria.zone`                  │ Dedicated VR Instance / DuckDNS Dynamic IP     │
│ `aetheria.itch.io`                      │ Free Game Host & Indie Downloads               │
└─────────────────────────────────────────┴────────────────────────────────────────────────┘

```
