# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

"Spendly" is a Flask-based expense tracker built incrementally as a learning project, in numbered steps (Step 1: Database Setup, Step 3: Logout, Step 4: Profile, Step 7-9: Expense CRUD, etc.). Many routes and modules are intentionally unimplemented placeholders — see `app.py` and `database/db.py` for "students will implement this" comments marking what step they belong to. When asked to "implement Step N," check the placeholder comments/routes for the expected scope before designing a larger solution.

## Commands

```bash
pip install -r requirements.txt   # install deps (Flask 3.1, Werkzeug 3.1, pytest 8.3, pytest-flask)
python app.py                     # run the dev server on http://localhost:5001 (debug=True)
pytest                            # run tests
pytest path/to/test_file.py::test_name   # run a single test
```

There is no build/lint step configured (no linter config, no frontend build tooling — `static/` is served as-is by Flask).

## Architecture

- **`app.py`** — single Flask app with all routes defined directly on `app` (no blueprints). Implemented routes render templates (`/`, `/register`, `/login`, `/terms`, `/privacy`); unimplemented routes (`/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete`) return placeholder strings and are expected to be built out in later steps.
- **`database/db.py`** — intended to hold `get_db()` (SQLite connection with `row_factory` and foreign keys enabled), `init_db()` (create tables with `CREATE TABLE IF NOT EXISTS`), and `seed_db()` (sample dev data). Not yet implemented — follow this exact contract when filling it in, since `app.py` and future routes will depend on these three function names.
- **`templates/`** — Jinja2 templates extending `base.html`, which defines the shared nav/footer shell and pulls in `static/css/style.css` and `static/js/main.js` via `url_for`. Page templates (`landing.html`, `login.html`, `register.html`, `terms.html`, `privacy.html`) fill the `title`, `head`, `content`, and `scripts` blocks.
- **`static/js/main.js`** and **`static/css/style.css`** — currently minimal/placeholder; features add JS/CSS here as routes are built out.
