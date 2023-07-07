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
git switch main && git fetch
git branch ${SLIDE_NAME}
```

```bash
mkdir ${SLIDE_NAME}

cd ${SLIDE_NAME}

cat << EOS > package.json
{
  "scripts": {
    "build": "slidev build",
    "dev": "slidev --open",
    "export": "slidev export"
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

Presentation slides for developers

---

# Page 2

- abc
- def
- ghi
EOS
```

```bash
npm run build
```

```bash
npx servor dist index.html 8080
```

## Configure deployment to Cloudflare

```bash
SLIDE_NAME=<slide_name>
```

```bash
ACCOUNT_IDENTIFIER=<account_identifier>
```

```bash
API_TOKEN=<api_token>
```

```bash
X_AUTH_EMAIL=<x_auth_email>
```

```bash
DATA=`cat << EOS
{
  "source": {
  "type": "github",
  "config": {
    "owner": "high-u",
    "repo_name": "slides",
    "production_branch": "main",
    "pr_comments_enabled": true,
    "deployments_enabled": true,
    "production_deployments_enabled": true,
    "preview_deployment_setting": "all",
    "preview_branch_includes": [
      "*"
    ],
    "preview_branch_excludes": []
  }
  },
  "build_config": {
    "build_command": "npm run build",
    "destination_dir": "dist",
    "root_dir": "${SLIDE_NAME}"
  },
  "canonical_deployment": null,
  "deployment_configs": {
    "preview": {
      "env_vars": {
        "NODE_VERSION": {
          "type": "plain_text",
          "value": "v16.18.1"
        }
      },
      "fail_open": true,
      "always_use_latest_compatibility_date": false,
      "usage_model": "bundled"
    },
    "production": {
      "env_vars": {
        "NODE_VERSION": {
          "type": "plain_text",
          "value": "v16.18.1"
        }
      },
      "fail_open": true,
      "always_use_latest_compatibility_date": false,
      "usage_model": "bundled"
    }
  },
  "name": "slides-${SLIDE_NAME}",
  "production_branch": "main"
}
EOS`

curl --request POST \
--url https://api.cloudflare.com/client/v4/accounts/${ACCOUNT_IDENTIFIER}/pages/projects \
--header 'Content-Type: application/json' \
--header 'X-Auth-Email: ${X_AUTH_EMAIL}' \
--header "Authorization: Bearer ${API_TOKEN}" \
--data ${DATA}
```

