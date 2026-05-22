
<style>
.profile-card {
  background: rgba(100,100,100,0.1);
  border: 1px solid #4f46e5;
  border-radius: 10px;
  padding: 10px 24px;
  text-align: center;
}
.feature-card {
  display: block;
  border: 1px solid #4f46e5;
  border-radius: 12px;
  padding: 20px 24px;
  text-decoration: none;
  color: inherit;
  background: rgba(79, 70, 229, 0.08);
  transition: background 0.2s;
}
.feature-card:hover {
  background: rgba(79, 70, 229, 0.18);
}
.feature-card p { margin: 0; }
.feature-title { font-weight: 700; font-size: 1rem; margin-bottom: 4px !important; }
.feature-sub { opacity: 0.6; font-size: 0.9rem; }
</style>

<div style="display: flex; align-items: flex-start; gap: 48px; padding: 60px 24px 40px 24px; max-width: 1100px; margin: 0 auto; flex-wrap: wrap;">

  <div style="display: flex; flex-direction: column; align-items: center; gap: 16px; min-width: 180px;">
    <div style="width: 200px; height: 200px; border-radius: 12px; border: 3px solid #4f46e5; overflow: hidden;">
      <img src="/images/avatar.jpg" alt="Eric Antonecchia" style="width: 100%; height: 100%; object-fit: cover; transform: scale(1.38); transform-origin: center 75%;">
    </div>
    <div class="profile-card">
      <p style="margin: 0; font-weight: 700; font-size: 1.1rem; letter-spacing: 0.5px;">Eric Antonecchia</p>
      <p style="margin: 4px 0 0 0; font-size: 0.8rem; opacity: 0.6;">Cybersecurity & Homelab</p>
    </div>
    <div style="display: flex; gap: 10px; flex-wrap: wrap; justify-content: center;">
      <a href="https://linkedin.com/in/yourusername" target="_blank" style="background: #0077b5; color: white; padding: 8px 16px; border-radius: 8px; text-decoration: none; font-size: 0.85rem; font-weight: 600;">LinkedIn</a>
      <a href="/posts" style="background: #4f46e5; color: white; padding: 8px 16px; border-radius: 8px; text-decoration: none; font-size: 0.85rem; font-weight: 600;">Posts</a>
    </div>
  </div>

  <div style="flex: 1; min-width: 280px;">
    <h1 style="font-size: 2rem; font-weight: 700; margin: 0 0 8px 0;">Hey, I'm Eric 👋</h1>
    <p style="opacity: 0.65; font-size: 1rem; line-height: 1.6; margin: 0 0 28px 0;">Documenting my journey through cybersecurity research, homelab builds, and technical deep-dives.</p>
    <div style="display: flex; flex-direction: column; gap: 16px;">
      <a href="/posts" class="feature-card">
        <p class="feature-title">🔐 Cybersecurity</p>
        <p class="feature-sub">Writeups, tools, CTF notes, and security research from my own exploration.</p>
      </a>
      <a href="/projects" class="feature-card">
        <p class="feature-title">🖥️ Homelab</p>
        <p class="feature-sub">Building and breaking things at home — servers, networking, self-hosted services.</p>
      </a>
      <a href="/projects" class="feature-card">
        <p class="feature-title">💻 Projects</p>
        <p class="feature-sub">Personal projects, experiments, and things I'm currently working on.</p>
      </a>
    </div>
  </div>

</div>