# Student Guide: AI Service Configuration for Lab 8

## Overview
Azure for Students subscriptions do not include access to Azure OpenAI resources. For this lab, a shared OpenAI API key has been provisioned by your instructor. This replaces **Step 3** in the lab instructions — you do **not** need to create any Azure OpenAI resources.

---

## Step 3 (Revised): Configure the AI Backing Services

### 1. Download the `secrets.yaml` File
- Download the `secrets.yaml` file from **Brightspace**
- Save it in your `Deployment Files` folder
- **Do not modify this file** — it contains the shared API key and is ready to use as-is
- **Do not push this file to any public GitHub repository** — add `secrets.yaml` to your `.gitignore`

### 2. Skip the Rest of Step 3
You do **not** need to:
- Create an Azure OpenAI resource
- Deploy GPT-4 or DALL-E 3 models
- Retrieve or Base64-encode any API keys
- Modify the `aps-all-in-one.yaml` file for AI configuration

The `aps-all-in-one.yaml` file is already configured to use the direct OpenAI API with the following models:
- **gpt-4o-mini** for product description generation
- **DALL-E 3** for product image generation

### 3. Continue with Step 4
Proceed with **Step 4** in the lab instructions as normal:
```bash
kubectl apply -f config-maps.yaml
kubectl apply -f secrets.yaml
```

All other lab steps (Step 5 through Step 8) remain unchanged.

---

## Troubleshooting

| Issue | Solution |
| ----- | -------- |
| `401 Unauthorized` error from AI service | Make sure you are using the `secrets.yaml` downloaded from Brightspace, not the template from the repo. |
| `429 Rate limit exceeded` | The shared API has rate limits. Wait a few seconds and retry. |
| `402 Insufficient quota` | The shared credit has been exhausted. Contact your instructor. |
| AI descriptions work but image generation does not | Check the ai-service pod logs: `kubectl logs deployment/ai-service`. Report the error to your instructor. |
| AI service pod is in `CrashLoopBackOff` | Verify the secrets were applied: `kubectl get secrets`. You should see `openai-gpt-api-secret` and `openai-dalle-api-secret`. If not, re-run `kubectl apply -f secrets.yaml`. |

---

## Important Notes
- **Do not modify the `secrets.yaml` file** — it contains the shared API key and is ready to use as-is
- **Do not push `secrets.yaml` to any public GitHub repository** — this would expose the shared API key and compromise it for the entire class
- **Do not share this file** outside of this class
- The shared API key has **rate limits** — if you get a `429` error, wait a moment and try again
- The key will be revoked after the lab deadline
