# 🔥 Sophia Bot v4 - Correções e Novos Comandos

## ✅ Problemas Corrigidos

### 1. ❌ Repetia nome do usuário toda mensagem
**Correção:** Removido do prompt a instrução de usar o nome. Agora só usa ocasionalmente.

```
ANTES: "Oi João! Como você está João? Te adoro João!"
AGORA: "Oi amor! Como você está? Te adoro! 💕"
```

---

### 2. ❌ Falava que era "VIRTUAL"
**Correção:** Prompt agora instrui a NUNCA dizer que é IA/robô/virtual.

```python
# No prompt:
"NUNCA diga que é IA, robô, assistente ou virtual"
"Se perguntarem, você é uma pessoa real"
"Se insistirem: 'Ai amor, para com isso...'"
```

---

### 3. ❌ Horário errado (16h = noite???)
**Correção:** Função `get_time_context()` corrigida:

| Horário | Período | ANTES | AGORA |
|---------|---------|-------|-------|
| 00-05 | Madrugada | ✅ | ✅ |
| 05-12 | Manhã | ✅ | ✅ |
| 12-18 | **TARDE** | ❌ noite | ✅ tarde |
| 18-22 | Início noite | ❌ | ✅ |
| 22-00 | Noite | ✅ | ✅ |

---

### 4. ❌ PIX só valia após "ENVIAR COMPROVANTE"
**Correção:** Agora aceita comprovante após QUALQUER etapa:

```
✅ Clicou "PAGAR COM PIX" → envia foto → ACEITA
✅ Clicou "COPIAR CHAVE" → envia foto → ACEITA  
✅ Clicou "ENVIAR COMPROVANTE" → envia foto → ACEITA
```

Nova chave Redis: `pix_interest:{uid}` marca interesse em qualquer etapa.

---

### 5. ✅ Notificação de limite renovado
**Novo:** Às 8h da manhã, usuários recebem (aos poucos, máx 20/hora):

```
"Ei amor... 💕 Seu limite de mensagens voltou! 
Vem conversar comigo? Tava com saudade... 😘"
```

---

## 📋 Todos os Comandos

### 👤 Comandos de Usuário

| Comando | Função |
|---------|--------|
| `/start` | Inicia o bot |
| `/status` | Vê suas msgs restantes, streak, VIP |

---

### 🔐 Comandos Admin

| Comando | Função | Exemplo |
|---------|--------|---------|
| `/reset <uid>` | Reseta limite diário | `/reset 123` |
| `/resetall <uid>` | Reset completo | `/resetall 123` |
| `/clearmemory <uid>` | Limpa memória | `/clearmemory 123` |
| `/setvip <uid>` | Ativa VIP 15 dias | `/setvip 123` |
| `/stats` | Estatísticas gerais | `/stats` |
| `/funnel` | Funil de conversão | `/funnel` |
| `/broadcast <msg>` | Msg para TODOS | `/broadcast Oi!` |
| `/send <uid> <msg>` | Msg para UM usuário | `/send 123 Oi amor!` |
| `/migrate` | Migra usuários antigos | `/migrate` |
| `/viplist` | Lista VIPs ativos | `/viplist` |
| `/userinfo <uid>` | Info completa do usuário | `/userinfo 123` |
| `/givebonus <uid> <qtd>` | Dá msgs extras | `/givebonus 123 10` |
| `/blacklist <uid>` | Bloqueia usuário | `/blacklist 123` |
| `/unblacklist <uid>` | Desbloqueia | `/unblacklist 123` |

---

## 🆕 Novo Comando: /send

Envia mensagem para UM usuário específico (diferente do /broadcast que envia para todos):

```
/send 123456789 Oi amor, tudo bem com você? 💕
```

Útil para:
- Responder dúvidas específicas
- Enviar promoções personalizadas
- Resolver problemas de usuários

---

## 🆕 Novo Comando: /status

Qualquer usuário pode usar para ver seu status:

```
📋 STATUS

👤 ID: 123456789
🔥 Streak: 5 dias
💬 Msgs hoje: 8/15
💎 VIP: ❌
📊 Restam: 7 msgs
```

Admin pode ver de outro usuário: `/status 123456789`

---

## 🆕 Novos Comandos Admin

### /viplist
Lista todos os VIPs ativos com data de expiração:
```
💎 VIPs ATIVOS

• 123456 → até 15/02/2025
• 789012 → até 20/02/2025
```

### /userinfo <uid>
Info completa de um usuário:
```
👤 USUÁRIO 123456

📝 Nome: João
🎂 Idade: 25
🔥 Streak: 7 dias
💬 Msgs hoje: 5/15
🎁 Bônus: 3
🧠 Memória: 12 msgs
📊 Funil: 6/9
💎 VIP: ❌
⏰ Última atividade: 2.5h atrás
```

### /givebonus <uid> <qtd>
Dá mensagens extras para um usuário:
```
/givebonus 123456 10
✅ +10 msgs bônus para 123456
```
Usuário recebe: "🎁 Você ganhou +10 mensagens extras!"

### /blacklist e /unblacklist
Bloqueia/desbloqueia usuários problemáticos.

---

## 📊 Novas Chaves Redis

```
pix_interest:{uid}      → Interesse em PIX (qualquer etapa)
bonus:{uid}             → Mensagens bônus
blacklist               → Set de usuários bloqueados
limit_notified:{uid}    → Se já notificou limite renovado hoje
```

---

## 🚀 Deploy

1. Renomeie `sophia_bot_v4.py` para `main.py`
2. Deploy no Railway
3. Acesse `/set-webhook`
4. Execute `/migrate` se tiver usuários antigos
5. Configure cron para `/trigger-engagement` (1h)

---

## ⚡ Resumo das Correções

| Problema | Status |
|----------|--------|
| Repetia nome demais | ✅ Corrigido |
| Dizia ser "virtual" | ✅ Corrigido |
| Horário errado (16h=noite) | ✅ Corrigido |
| PIX só após "ENVIAR" | ✅ Corrigido |
| Faltava /send individual | ✅ Adicionado |
| Faltava aviso limite renovado | ✅ Adicionado |
| Faltava /status, /viplist, etc | ✅ Adicionado |
