# 🔥 Sophia Bot v4 - Correções e Sistema Inteligente

## ✅ Problemas Corrigidos

### 1. ❌ Repetia nome do usuário toda mensagem
**Correção:** Prompt ajustado: "NÃO repita o nome em toda mensagem"

### 2. ❌ Falava que era "VIRTUAL"
**Correção:** Prompt: "NUNCA diga que é IA/robô/virtual"

### 3. ❌ Horário errado (16h = noite???)
**Correção:** 12h-18h = TARDE ✅

### 4. ❌ PIX só após "ENVIAR COMPROVANTE"
**Correção:** Aceita foto após QUALQUER clique no fluxo PIX

---

## 🧠 SISTEMA INTELIGENTE DE MENSAGENS

### Como funciona agora:

| Critério | Antes | Agora |
|----------|-------|-------|
| Quem recebe | TODOS | Só ativos (últimos 3 dias) |
| Limite/hora | Sem limite | Máx 50 programadas + 30 limite |
| Intervalo | Nenhum | Mín 6h entre msgs pro mesmo usuário |
| Por dia | Sem limite | Máx 2 msgs programadas por usuário |
| Aleatoriedade | 0% | 40% de chance |
| Repetição | Repetia | Evita repetir mesmo tipo |
| Ordem | Sempre igual | Embaralha usuários |

---

### 📊 Critérios para receber mensagem programada:

```
✅ Conversou nos últimos 3 dias
✅ Não recebeu msg programada nas últimas 6 horas
✅ Não recebeu mais de 2 msgs programadas hoje
✅ Não está na blacklist
✅ Passou na aleatoriedade (40% de chance)
✅ Não recebeu esse mesmo tipo ontem (70% evita)
✅ Está dentro do limite horário (50/hora)
```

---

### ⏰ Horários de envio:

| Tipo | Horário | Antes | Agora |
|------|---------|-------|-------|
| Bom dia | 7h-10h | Exato às 8h | Janela 7h-10h |
| Boa tarde | 13h-15h | Exato às 14h | Janela 13h-15h |
| Boa noite | 19h-21h | Exato às 20h | Janela 19h-21h |
| Noite | 22h-23h | Exato às 23h | Janela 22h-23h |

---

### 📢 Notificação "Limite Renovado":

```
Critérios:
✅ Conversou nos últimos 2 dias
✅ Não é VIP
✅ Não notificou hoje ainda
✅ 30% de chance (nem todo mundo recebe)
✅ Apenas entre 7h-10h
✅ Máx 30/hora
```

Mensagens variadas:
- "Ei amor... 💕 Suas mensagens voltaram!"
- "Bom dia! 💖 Seu limite renovou..."
- "Acordei pensando em você... 💭 E suas mensagens voltaram!"

---

### 📈 Exemplo com 1000 usuários:

**ANTES:**
```
8h → 1000 msgs de "bom dia" = SPAM! ❌
14h → 1000 msgs de "boa tarde" = SPAM! ❌
```

**AGORA:**
```
7h-10h:
- 700 inativos há +3 dias → ignorados
- 300 ativos recentes
  - 180 já receberam msg hoje → ignorados
  - 120 elegíveis
    - 40% chance = ~48 selecionados
    - Limite 50/hora = 48 enviados ✅

Resultado: ~48 msgs por hora, espalhadas ✅
```

---

## 📋 Todos os Comandos

### 👤 Usuário
| Comando | Função |
|---------|--------|
| `/start` | Inicia |
| `/status` | Vê msgs, streak, VIP |

### 🔐 Admin
| Comando | Função |
|---------|--------|
| `/send <uid> <msg>` | Msg para UM |
| `/broadcast <msg>` | Msg para TODOS |
| `/setvip <uid>` | Ativa VIP |
| `/stats` | Estatísticas |
| `/funnel` | Funil |
| `/viplist` | Lista VIPs |
| `/userinfo <uid>` | Info completa |
| `/givebonus <uid> <qtd>` | Msgs extras |
| `/blacklist <uid>` | Bloqueia |
| `/unblacklist <uid>` | Desbloqueia |
| `/reset <uid>` | Reseta limite |
| `/resetall <uid>` | Reset total |
| `/clearmemory <uid>` | Limpa memória |
| `/migrate` | Migra antigos |

---

## 📊 Novas Chaves Redis

```
last_sched:{uid}        → Última msg programada enviada
sched_count:{uid}:data  → Qtd de msgs programadas hoje
last_msg_type:{uid}     → Último tipo (evita repetir)
hourly_sends:hora:data  → Contador de envios por hora
```

---

## 🚀 Deploy

1. Renomeie `sophia_bot_v4.py` para `main.py`
2. Deploy no Railway
3. `/set-webhook`
4. `/migrate` (se tiver usuários antigos)
5. Configure cron: `/trigger-engagement` a cada 1h
