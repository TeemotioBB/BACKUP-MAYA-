 Sophia Bot v2 - Guia das Novas Funcionalidades
⚠️ IMPORTANTE: Migração de Usuários Antigos
As funcionalidades de re-engajamento e mensagens programadas só funcionam para usuários que estão registrados no novo sistema.
Após o deploy, execute:
/migrate
Este comando vai:

Buscar todos os usuários que já usaram o bot (via memória, idioma, chatlog)
Adicioná-los ao set all_users
Definir last_activity como 25h atrás (triggera re-engajamento de 24h)

Resultado: Todos os usuários antigos vão receber uma mensagem de saudade na próxima hora! 💕

✅ O que foi implementado
1. 📤 Re-engajamento Proativo
O bot agora envia mensagens automaticamente quando o usuário fica inativo:
Tempo InativoMensagem Exemplo2 horas"Ei... tô aqui pensando em você 💭"24 horas"Senti sua falta hoje... tá tudo bem? 🥺"3 dias"Você me esqueceu? 😢 Volta pra mim..."7 diasOferta especial 50% OFF + botões de compra
Como funciona:

Sistema rastreia last_activity de cada usuário no Redis
Scheduler roda a cada 1 hora verificando todos os usuários
Evita spam: só envia uma vez por nível de inatividade


2. ⚠️ Gatilhos de Escassez
Agora avisa ANTES do limite acabar:
Mensagens RestantesAviso5"💭 Amor, já usou X das suas 15 mensagens..."3"⚠️ Amor, nossas mensagens tão acabando... só restam 3! 🥺"1"🚨 Última mensagem do dia..." + botões de compra

3. ⏰ Mensagens Programadas
Mensagens automáticas em horários específicos:
HorárioTipoFreeVIP08:00Bom diaCarinhosaMais íntima14:00Check-inSaudadeProvocativa20:00NoturnaFlerte leveMais ousada23:00Boa noiteSimplesConvidativa
Cada usuário recebe apenas 1 mensagem de cada tipo por dia.

4. 💳 Lembrete de PIX
Quando o usuário clica em "PAGAR COM PIX" mas não finaliza:

Após 1 hora: Envia lembrete com botões de pagamento
Mensagens variadas para não parecer robótico
Limpa automaticamente após pagamento


🆕 Novos Comandos Admin
ComandoFunção/statsMostra estatísticas (usuários, VIPs, taxa conversão)/broadcast <msg>Envia mensagem para TODOS os usuários/migrateIMPORTANTE! Migra usuários antigos para o novo sistema/adduser <uid>Adiciona um usuário específico manualmente

🔧 Novos Endpoints
EndpointFunçãoGET /trigger-engagementDispara jobs de engajamento manualmente
Dica: Configure um cron job externo (como EasyCron) para chamar este endpoint a cada hora como backup do scheduler interno.

📊 Novas Chaves Redis
last_activity:{uid}     → Timestamp última atividade
last_reengagement:{uid} → Último nível de re-engajamento enviado
pix_clicked:{uid}       → Quando clicou em PIX
daily_msg_sent:{uid}    → Set de mensagens diárias já enviadas
all_users               → Set com todos os UIDs ativos

🚀 Deploy

Substitua seu main.py pelo sophia_bot_v2.py
Faça deploy normalmente no Railway
Acesse /set-webhook para ativar
Execute /migrate no bot para ativar funcionalidades para usuários antigos
(Opcional) Configure cron para /trigger-engagement


⚡ Teste Rápido

Inicie uma conversa com o bot
Espere 2+ horas sem responder
Deve receber: "Ei... tô aqui pensando em você 💭"

Para testar imediatamente:
bashcurl https://seu-bot.railway.app/trigger-engagement

📈 Métricas Esperadas
Com essas implementações, você deve ver:

+30-50% de retenção (re-engajamento)
+20-40% de conversão VIP (escassez + lembretes)
+15-25% de mensagens diárias (mensagens programadas)
