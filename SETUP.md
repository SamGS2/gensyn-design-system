# Setup checklist (print this)

- [ ] Create GitHub repo `gensyn-design-system`
- [ ] `cd design-system` → `git init` → add → commit → push to `main`
- [ ] Settings → Pages → source **GitHub Actions**
- [ ] Wait for workflow green; open Pages URL
- [ ] Share URL with boss
- [ ] Copy `CLAUDE.md.template` into first new project as `CLAUDE.md`
- [ ] Tag `v1.0.0` when stable

**Copy command (from FitFinderC root):**

```powershell
cd C:\Developer\FitFinderC\design-system
git init
git add .
git commit -m "Initial Gensyn design system"
git remote add origin https://github.com/YOUR_ORG/gensyn-design-system.git
git push -u origin main
```

**Preview without GitHub:**

```powershell
cd C:\Developer\FitFinderC\design-system
Copy-Item -Recurse -Force css docs\css
Copy-Item -Recurse -Force assets docs\assets
cd docs
python -m http.server 8765
```

Open http://localhost:8765
