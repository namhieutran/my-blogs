## Setting Up a New Terminal Environment: From Zero to <30 Minutes

### The story

After 20+ years in software engineering, I realized my terminal setup was still an undocumented infrastructure. Every time I got a new machine, or wiped an old one, I did almost the same thing:

- Install some tools.
- Copy some dotfiles.
- Configure the shell.
- Fix a few things.
- Install something I forgot.
- Then realize there was another configuration on my old machine that I hadn't copied yet.

It worked, but not reproducible. And then, that started to bother me.

So I decided to treat my terminal environment like a small software project.

### The problem

My old setup process was basically a collection of notes, commands, dotfiles, and memory. When reviewing the process, I realized that the problem wasn't really the installation. It was the **state**:

- What exactly did I have installed?
- Which configuration was the latest?
- Which machine had the correct version?
- What did I change six months ago?
- What would happen if I had to start from an empty machine?

I wanted to remove those questions, not by writing another checklist, but by making the environment reproducible.

### Define the constraints

Before choosing the tools, I defined a few constraints for this project:

- **Setup time: <30m** — From an empty macOS machine to a fully working terminal environment.
- **Shell startup: <150ms** — The prompt should be fast enough that I don't notice the shell initialization.
- **Update time: <2m** — Adding a tool or changing a configuration should be a small, repeatable operation.
- **Version-controlled** — If I wipe the machine and run the setup again, I should get the same environment back.

These numbers are intentionally specific: "Fast" is a nice feeling. "<150ms" is something I can measure.

### The stack

I wanted the stack to stay small, with each layer having one clear responsibility. So I chose:

- **[Homebrew](https://brew.sh)** for software and package management.
- **[chezmoi](https://chezmoi.io)** for configuration (dotfiles).
- **[Git](https://git-scm.com)** for the desired state, hosted by **[GitHub](https://github.com)**.
- **[zsh](https://zsh.org)** for the shell.
- **[Ghostty](https://ghostty.org)** for the terminal emulator.
- **[Starship](https://starship.rs)** for the prompt.

That's basically the architecture. The important part is not the individual tools; it is how they fit together:

- Homebrew owns the installed software.
- The `Brewfile` becomes the source of truth for applications and CLI tools.
- chezmoi owns the configuration files.
- zsh and Starship help me interact with the terminal.
- Git stores the desired state.
- The machine itself becomes the output.

That distinction is important: I don't want my machine to be the source of truth. I want my repository to be the source of truth.

Worth to be mentioned, I personally chose the **[JetBrains Mono](https://www.jetbrains.com/lp/mono/)**, with its Nerd Font (**JetBrains Mono Nerd Font**), for rendering the terminal UI since I like the way it looks.

### The decisions

#### Start from blank

One decision I made deliberately was to start configurations from scratch: No preset; no giant configuration framework; no "recommended setup" that enables 30 things I may never use. A preset can look great in a screenshot, but every additional module is another piece of behavior that I need to understand, maintain, and potentially pay for in startup time.

Starting from blank means every configuration option has a reason to exist. If I don't need it, it doesn't go in.

#### Why no Oh My Zsh?

This is not an argument that Oh My Zsh is bad. It simply wasn't the right trade-off for this project.

My requirement was a lightweight shell with a startup time below 150ms. So I kept zsh simple and added only the plugins I actually use:

- **zsh-autosuggestions**
- **zsh-history-substring-search**
- **zsh-syntax-highlighting**
- **zsh-completions**

Even those plugins are loaded explicitly. Less magic, less dependency, less startup work.

#### One source of truth

Another design decision was to use Homebrew for both applications and zsh plugins. Another tool may be added here, but why? Homebrew manages the apps really well, including my required plugins. Adding another tool (e.g., `Zinit`) just to manage four zsh plugins would introduce another layer without solving a problem I actually had.

So the rule became simple:

> If it is installed on this machine, it's in the `Brewfile`.

No exceptions; no "I installed that manually once". That sounds like a small rule, but it makes the environment much easier to reason about.

### The interesting part: performance

Having the environment set up with my dotfiles repository, I measured the shell startup time after the initial setup on a new machine, or when I made changes to the environment configuration. The command is simple:

```bash
time zsh -i -c exit
```

On a clean environment, it was comfortably below the 150ms target. That's one of the goals. Good. But that wasn't the end of the story.

On one of my machines, I noted the startup time seemed slower, so I measured again. The problem turned out to be the zsh completions.

On a fresh environment, completion initialization was fast enough. But as I installed more CLI tools, the completion setup became more expensive. Eventually, it added more than 100ms to shell startup. That was enough to break my original constraint.

So I disabled it. Not because completions are bad, but because they were no longer worth the cost for this particular environment.

This was probably the most useful discovery from the whole exercise: **Performance is not a feature you configure once**. It can regress as the environment grows, and the only reliable way to know is to measure it.

### Rebuild the machine

Having an environment that was described by a Brewfile, some chezmoi-managed dotfiles, and a Git repository, the machine became disposable. That's the part I like most.

I can wipe the machine. Then, after a few steps, I get the environment back:

- Install the bootstrap tools.
- Pull the repository.
- Run the setup.
- Apply the configuration.

The machine is no longer the configuration; it's just an instance of the configuration. That's a much better mental model.

### What I learned

This small project started as a way to make my terminal setup easier. But the more interesting lessons were not about the tools, like Ghostty, zsh, or Homebrew; they were about engineering.

- **Automate the things you have already done many times**. If I have to repeat the same setup process every time I get a new machine, it is probably a good candidate for automation.
- **Define measurable constraints**. "Fast" is subjective; "<150ms" gives me something I can test.
- **Prefer a small number of clear responsibilities**. Each tool has a job: Homebrew installs; chezmoi manages configuration; Git stores the desired state.
- **Minimize unnecessary layers**. A new tool should solve a real problem, not just because everyone else uses it.
- **Measure after changes**. A configuration that is fast today may not be fast six months from now.

### What's next?

The first version of this project is intentionally small. It's primarily designed for macOS and lacks a terminal multiplexer, AI agent CLIs, or multi-platform support. Those are interesting features, but they are different problems.

For now, I want the foundation to stay simple and stick to the core goal:

> **A reproducible terminal environment that can go from zero to working in under 30 minutes**

I'm not building the "perfect" terminal. I build one that I can understand, measure, reproduce, and rebuild. And, most importantly, one that doesn't depend on my memory.
