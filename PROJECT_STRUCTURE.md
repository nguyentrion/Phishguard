# 📁 PhishGuard Project Structure

This file provides a concise map of the repository and the purpose of key files and folders. The layout below matches the actual code in the repository.

---

## Root (selected files)

```
Phishing URL Detection/
├── app.py                  # Main Flask application (API routes + web views). Lazy-loads ML model on first request.
├── config.py               # Optional configuration helpers
├── requirements.txt        # Exact Python packages used by the project
├── README.md               # This file — install/run instructions
├── PROJECT_STRUCTURE.md    # This file — overview of repository layout
└── URL Phishing Detection System Synopsis.txt  # Project synopsis / notes
```

---

## Documentation (/docs)

```
docs/
├── API.md                  # API reference for endpoints: auth, detect, history, admin
├── SETUP.md                # Setup & deployment instructions
├── AUDIT_COMPLETION.md     # Audit summary
├── AUDIT_REPORT.md         # Detailed audit findings
└── archive/                # Legacy documents and change notes
```

---

## Machine Learning (/ml)

```
ml/
├── features.py             # Feature extraction for URLs (used by training and detection)
├── train_model.py          # Training script: reads dataset/*, trains RandomForest, writes model/phishing_model.pkl
├── quick_train.py          # Smaller utility for quick iterations
└── model_loader.py         # (if present) helper for loading models safely
```

Notes: training writes `model/phishing_model.pkl` by default. Training auto-detects URL and label columns in the dataset CSV/XLSX.

---

## Utilities (/utils)

```
utils/
├── database.py             # SQLAlchemy models and DB init (User, URLCheck, SystemLog)
├── security.py             # Input sanitization, URL validation, auth decorators
```

---

## Web templates & static

```
templates/                  # Jinja2 templates: index, login, dashboard, admin, result
static/                     # CSS, JS, images used by the UI
```

---

## Data, model, and logs

```
dataset/                    # Place training CSV/XLSX files here
data/                       # Additional sample data (e.g., commoncrawl_sample.csv)
model/                      # Trained models (phishing_model.pkl)
instance/                   # Local SQLite instance file (instance/phishguard.db)
logs/                       # Application logs (logs/app.log)
```

If you'd like, I can expand this file with file sizes, sample commands, or a visual tree. Next I will update `docs/SETUP.md` to reflect the exact install and environment steps.

---

## Tools & Testing (/tools)

```
tools/
├── test_api.py                             # API endpoint testing
├── test_admin_dashboard.py                 # Admin panel tests
├── test_admin_pagination.py                # Pagination functionality tests
├── test_history_api.py                     # History endpoint tests
├── test_stats_endpoint.py                  # Statistics API tests
├── batch_test.py                           # Batch URL testing
├── huge_batch_test.py                      # Large-scale batch testing
├── verbose_batch_test.py                   # Detailed batch test output
├── check_history.py                        # History verification
├── check_requirements.py                   # Dependencies check
├── check_schema.py                         # Database schema validation
├── check_tables.py                         # Table structure check
├── show_test_users.py                      # Display test user data
├── verify_app.py                           # Application health check
├── verify_all_fixes.py                     # Verify all fixes applied
├── verify_history.py                       # History system validation
├── verify_navbar.py                        # Navigation verification
├── verify_home_navbar.py                   # Home button check
├── fetch_and_test_commoncrawl.py          # External dataset testing
├── predict_from_file.py                    # Batch predictions from file
├── summarize_results.py                    # Result aggregation
├── inspect_model.py                        # Model inspection utility
└── debug_predict.py                        # Prediction debugging
```

---

## Data & Datasets

```
data/
└── commoncrawl_sample.csv                  # Sample URLs for testing

dataset/
└── URL Dataset.xlsx                        # Training dataset

model/
├── phishing_model.pkl                      # Trained ML model
└── model.pkl                               # Alternative model file

results/
├── batch_results.csv                       # Batch test outputs
├── commoncrawl_results.csv                 # External dataset results
├── huge_batch_results_100000.csv           # Large-scale test results
└── summary.txt                             # Results summary
```

---

## Database & Logs

```
instance/ (local only)
└── phishguard.db                           # SQLite database file (local development)

# On Vercel deployments the app uses `/tmp/phishguard.db` (ephemeral)
# The app also supports `DATABASE_URL` / `SQLALCHEMY_DATABASE_URI` env var for managed DBs

logs/
└── app.log                                 # Application activity logs
```

---

## Unused/Legacy Frontend (Not Active)

```
Frontend/                                   # Legacy frontend (replaced by templates/)
├── admin.html                              # Old admin page
├── dashboard.html                          # Old dashboard
├── index.html                              # Old homepage
├── login.html                              # Old login page
└── static/                                 # Old static files
    ├── css/
    ├── js/
    └── img/
```

---

## Directory Purpose Summary

| Directory | Purpose | Files |
|-----------|---------|-------|
| **Root** | Core application files | 7 essential files |
| **/docs** | All documentation | 4 active + archive |
| **/ml** | Machine learning code | 4 files |
| **/utils** | Shared utilities | 2 modules |
| **/templates** | Active HTML templates | 5 pages |
| **/static** | Active CSS/JS/images | 4 JS + 1 CSS |
| **/tools** | Testing & utilities | 20+ scripts |
| **/data** | Sample datasets | 1 CSV |
| **/dataset** | Training data | 1 XLSX |
| **/model** | Trained models | 2 PKL files |
| **/results** | Test outputs | 3 CSV + summary |
| **/instance** | Database storage | 1 DB file |
| **/logs** | Application logs | 1 log file |
| **/Frontend** | Legacy (unused) | Archived |

---

## File Organization Benefits

✅ **Clean Root Directory** - Only essential configuration and main app files
✅ **Organized Documentation** - All docs in `/docs`, old files archived
✅ **Centralized Testing** - All test scripts in `/tools` folder
✅ **Clear Separation** - Code, data, templates, and docs properly separated
✅ **Easy Navigation** - Logical structure for developers
✅ **Professional Appearance** - Industry-standard organization

---

## Quick Navigation

- **Start Here:** README.md
- **API Docs:** docs/API.md
- **Setup Guide:** docs/SETUP.md
- **Main App:** app.py
- **Train Model:** ml/train_model.py
- **Run Tests:** tools/verify_app.py
- **View Logs:** logs/app.log
- **Database:** instance/phishguard.db

Note: The application chooses the database path at startup. Locally it creates `instance/phishguard.db`; on Vercel it uses `/tmp/phishguard.db`. If you provide a `DATABASE_URL` or `SQLALCHEMY_DATABASE_URI` environment variable the app will use that instead.

---

**Project Structure Version:** 1.0.0  
**Last Updated:** March 07, 2026  
**Status:** ✅ Organized and Semi-Production Ready (Vercel)
