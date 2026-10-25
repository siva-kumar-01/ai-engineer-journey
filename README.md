# AI Engineer Journey

A personal tracker for your 32-week roadmap from SAP to AI Engineer at top tech companies. It shows each week's tasks with their resource links, a daily study log, your consistency over time, monthly checkpoints and weekly reviews. Your data is stored in your own database, and you sign in with your email and password from any device.

It's a single `index.html` file with no build step.

## Files

```
index.html            The whole app: design, roadmap data and logic
supabase/schema.sql   Database tables and security rules
README.md             This guide
```

## Setup overview (about 15 minutes)

1. Create the database (Supabase, free).
2. Put your database details into `index.html`.
3. Host the site (GitHub Pages, free).
4. Create your account, then lock sign-ups so nobody else can register.

### 1. Create the database

1. Create a free account and project at [supabase.com](https://supabase.com).
2. In the project, open **SQL Editor**, paste the contents of `supabase/schema.sql`, and click **Run**.
3. Open the project's API settings and copy the **Project URL** and the **anon** or **publishable** key.

**Never use the `service_role` or secret key** in this site. The app refuses it if you paste one.

### 2. Add your database details to the site

Open `index.html` in a text editor and find this line near the top of the script:

```js
const CLOUD_CONFIG = { url: "", key: "" };
```

Fill it in:

```js
const CLOUD_CONFIG = { url: "https://your-project.supabase.co", key: "your-anon-or-publishable-key" };
```

With this filled in, every device that opens your site shows the sign-in screen first. The anon or publishable key is designed to be public; Row Level Security in `schema.sql` means only your signed-in account can read or change your rows.

(You can also paste these details in **Settings > Login and sync** on each device instead, but putting them in the file is simpler.)

### 3. Host it on GitHub Pages

1. Create a new repository on GitHub, for example `ai-engineer-journey`.
2. Upload `index.html`, `README.md` and the `supabase` folder.
3. Go to **Settings > Pages**, choose **Deploy from a branch**, pick `main` and `/ (root)`, and save.
4. After a minute or two, your site is live at `https://<your-username>.github.io/ai-engineer-journey/`.

Netlify, Vercel and Cloudflare Pages also work: drag the folder into their dashboard.

Back in Supabase, go to **Authentication > URL Configuration** and set **Site URL** to your site's address. Email confirmation and password reset links then return to your site.

### 4. Create your account and lock sign-ups

1. Open your site, choose **First time here? Create your account**, and enter your email and a password of at least 8 characters.
2. If Supabase sends a confirmation email, open the link, then sign in.
3. In Supabase, open the **Authentication** settings and turn off **Allow new users to sign up**. Since only you use the site, this stops anyone else from creating an account on your database.

Sign in once on each device. You stay signed in until you sign out.

## Everyday use

- **Signing in:** your email and password. If you forget the password, use **Forgot your password?** on the sign-in screen, then open the emailed link to choose a new one.
- **Changing your password:** Settings > Login and sync.
- **Signing out:** removes your progress from that device only. It stays safe in your database and comes back when you sign in again. Useful on shared computers.
- **Sign out everywhere:** signs out every device at once, for example if you lose your phone. It's in Settings > Login and sync.
- **Auto sign-out:** each device signs out after a period without activity (1 day by default). Change it per device in Settings > Login and sync, for example 15 minutes on an office computer. Changes that haven't uploaded yet are never thrown away; they upload when you sign in again.
- **Offline:** changes are saved on the device first and upload automatically when you're back online. If the database can't be reached at sign-in, you can choose to work offline on that device.
- **Sync status:** the pill at the top right shows whether everything is synced.

**Note:** Supabase pauses free projects after about a week with no activity. If sign-in stops working after a long break, open your Supabase dashboard and restore the project. Your data is kept.

## Backups

**Settings > Backup > Download backup** saves everything as a JSON file, and **Restore from backup** brings it back. Doing this once a month is a good habit.

## About the roadmap

The plan runs for 32 weeks (8 months) and targets AI Engineer, Software Engineer (AI/ML) and Applied AI roles at top tech companies such as Google, Microsoft, Amazon, Meta, Apple and NVIDIA. It merges the best parts of several published roadmaps with the interview preparation those roadmaps leave out.

| Months | Focus |
|---|---|
| 1 | Python engineering, Python for AI (NumPy, Pandas, plots), Git, SQL, APIs, your first raw LLM call |
| 2 | ML fundamentals, a classic ML project with honest evaluation, and your flagship's backend |
| 3 | Deep learning basics, transformers, and RAG built from scratch with an eval set from day one |
| 4 | Structured extraction, agents from primitives, LangGraph, MCP and human approvals |
| 5 | Production AI: tracing, experiment tracking, evals in CI, safety tests, caching, fine-tuning, deployment |
| 6 | System design, ML system design, GenAI design, packaging, and the first applications |
| 7 | Timed DSA, mock interviews, behavioral stories, company-specific prep |
| 8 | Interview mode, offers, and planning the next phase |

DSA (Striver's A2Z in C++, then LeetCode Top Interview 150) runs every week throughout, because coding rounds are the first gate at top companies.

**Projects.** One flagship, Procurement Copilot, grows layer by layer: backend and data, grounded RAG with role-based access, invoice extraction, a bounded agent with approvals and MCP tools, then production hardening. A second, smaller classic ML project (supplier-email triage) is later used for a fine-tuning comparison. Every project shows a number, admits a failure, and has a demo someone can try.

**Skipped on purpose, for now:** computer vision models, classic NLP (POS tagging, parsing), RNN/LSTM depth, Kubernetes, GraphQL, web servers like Nginx, deep NoSQL and Elasticsearch work, Kubeflow, Airflow, KServe, Terraform, and extra agent frameworks. Learn the concepts later if a role needs them.

For top companies, 20 to 25 study hours a week works well. If you fall behind, the plan stretches; keep going.

**If you used an earlier version of this tracker:** tasks now have new ids, so earlier ticks won't show against the new plan. If you already ran an older `schema.sql`, run the new one again; it safely widens the week limit for weekly reviews.

## Customize the roadmap

Everything is in the `<script>` section of `index.html`:

- `RES` holds every resource link. If a link breaks, change its URL here and it updates everywhere.
- `WEEKS` holds the 32 weeks. Each task looks like `["w3-b", "swe", "Task title", ["fastapi_tut"], { tip: "...", opt: true }]`.
- `MONTHS` holds month goals, checkpoints and DSA targets.
- `DECISIONS` is the "decisions you've already made" card on the dashboard.

Keep existing task ids such as `"w3-b"` unchanged, because your saved progress uses them. To add a task, append it with a new id.

## About the resources

- DSA: Striver's A2Z sheet, Logic First Tamil for concepts, LeetCode Top Interview 150 for timed practice.
- Python for AI: NumPy quickstart and 100 NumPy exercises, Kaggle's Pandas and visualization courses.
- ML and deep learning: Google's Machine Learning Crash Course, Andrew Ng's courses on DeepLearning.AI, Karpathy's Zero to Hero, PyTorch tutorials.
- AI engineering: DeepLearning.AI short courses, official docs, Anthropic's engineering articles, Hamel Husain on evals, LLM Zoomcamp, Maxime Labonne's LLM course.
- Production and safety: Langfuse, MLflow, Ragas, OWASP's prompt injection cheat sheet.
- System design: Hello Interview, the System Design Primer, ByteByteGo, Chip Huyen's ML interviews book.
- DeepLearning.AI videos are usually free; certificates, graded labs and the full RAG course need PRO.
- CS fundamentals use the GeeksforGeeks CIP tracks you already own (sign in to GeeksforGeeks to open them).
- Some links are YouTube searches rather than single videos, so they keep working if a playlist moves.

If a link doesn't open, search for the resource's title and update it in `RES`.
