# slides

## New slide

```bash
SLIDE_NAME=<slide_name>
```

```bash
if [ -e ${SLIDE_NAME} ]; then
  echo "\033[1;37;41m NG \033[0m"
else
  echo "\033[1;37;44m OK \033[0m"
fi
```

```bash
git switch main && git pull
git branch ${SLIDE_NAME}
git switch ${SLIDE_NAME}
```

```bash
mkdir -p ./draft/${SLIDE_NAME}

cd ./draft/${SLIDE_NAME}

cat << EOS > package.json
{
  "scripts": {
    "build": "slidev build",
    "dev": "slidev --open",
    "export": "slidev export",
    "publish": "slidev build --base /foobar/ --out ../../public/foobar"
  }
}
EOS

npm install @slidev/cli @slidev/theme-default

cat << EOS > slides.md
---
theme: default
transition: slide-left
title: ${SLIDE_NAME}
---

# Title

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

---

# Lorem ipsum

- Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
- Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
- Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
- Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
EOS
```

```bash
npm run dev
```

## Publish slide

1. Output to public directory. `npm run publish`
1. Merge to main branch.
