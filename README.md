cat > README.md <<'EOF'
# 🧰 Automated Backup Script (DevOps Practice Test)

This project is part of the **DevOps Bash Scripting Practice Test**.  
It automates the process of taking backups using configurable options.

## 🚀 Features
- Reads settings from `backup.config`
- Supports `--dry-run` mode
- Excludes unwanted folders like `.git`, `node_modules`, etc.
- Logs all operations automatically

## 🧑‍💻 Usage
```bash
./backup.sh --dry-run /path/to/source


