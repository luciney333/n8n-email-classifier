# Email Classifier Agent

Automated email classification system built with n8n and Claude (Anthropic API).

## What it does
Receives an email (subject, body, sender) via webhook and returns:
- Category: support / sales / spam / billing / other
- Urgency: high / medium / low
- Summary of the issue
- Recommended action for the team

All executions (success and error) are logged to a Supabase database.

## Tech stack
- n8n (workflow orchestration)
- Claude Haiku (Anthropic API) — classification and reasoning
- Supabase (PostgreSQL) — execution logs

## Architecture
Webhook → Validate input → Claude (classify) → Parse JSON → Log to Supabase → Response

## How to use
1. Import `workflow.json` into your n8n instance
2. Add your Anthropic and Supabase credentials
3. Activate the workflow
4. Send a POST request to `/webhook/clasificar-email`

## Example request
```json
{
  "asunto": "Cannot access my account",
  "cuerpo": "I have been trying to log in for two days and it keeps saying wrong password.",
  "remitente": "customer@gmail.com"
}
```

## Example response
```json
{
  "clasificacion": {
    "categoria": "soporte",
    "urgencia": "alta",
    "resumen": "User cannot access account due to password error",
    "accion_recomendada": "Verify identity and reset password"
  }
}
```
