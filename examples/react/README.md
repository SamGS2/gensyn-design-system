# React / Vite example

In your Vite app:

```bash
# Option A: copy folder
cp -r ../../css src/styles/gensyn/
cp ../../assets/gensyn-logo.svg public/

# Option B: submodule at packages/gensyn-design-system
```

`src/main.jsx` or `src/index.css`:

```css
@import './styles/gensyn/gensyn-tokens.css';
@import './styles/gensyn/gensyn-components.css';
```

Root layout:

```jsx
export default function Layout({ children }) {
  return (
    <div className="gensyn-page" style={{ minHeight: '100vh', display: 'flex', flexDirection: 'column', alignItems: 'center', padding: '2rem' }}>
      <div className="gensyn-container">
        {children}
      </div>
    </div>
  )
}
```

Example card page:

```jsx
export default function Home() {
  return (
    <>
      <img src="/gensyn-logo.svg" alt="Gensyn" className="gensyn-logo gensyn-logo--intake" />
      <div className="gensyn-card gensyn-card--intake">
        <h1 className="gensyn-h1">Your product name</h1>
        <p className="gensyn-subtitle">Short description here.</p>
        <button type="button" className="gensyn-btn-primary">Get started</button>
      </div>
    </>
  )
}
```

Copy `CLAUDE.md.template` from the design-system root to your project as `CLAUDE.md` and update the style guide URL.
