# 🔗 Configuração do Webhook Hotmart - UP Money

## 📋 Resumo da Integração

A integração com o webhook da Hotmart está **100% COMPLETA** e pronta para uso! O sistema automaticamente:

✅ Recebe notificações de pagamento da Hotmart  
✅ Cria/atualiza usuários no banco de dados  
✅ Libera acesso ao app baseado no plano adquirido  
✅ Registra todas as transações para controle  
✅ Calcula automaticamente a data de expiração do plano  

---

## 🌐 URL do Webhook

**URL para configurar na Hotmart:**
```
https://[SEU_DOMINIO]/api/webhook/hotmart
```

> ⚠️ **IMPORTANTE**: Substitua `[SEU_DOMINIO]` pela URL pública do seu projeto.

---

## ⚙️ Como Configurar na Hotmart

### 1. Acesse o Painel da Hotmart
- Entre na sua conta Hotmart
- Vá em **"Meus Produtos"**
- Selecione o produto UP Money

### 2. Configure o Webhook
- Clique em **"Configurações"**
- Vá na aba **"Integração"** ou **"Webhooks"**
- Adicione a URL: `https://[SEU_DOMINIO]/api/webhook/hotmart`
- Selecione os eventos:
  - ✅ `PURCHASE_APPROVED` (Compra Aprovada)
  - ✅ `PURCHASE_COMPLETE` (Compra Finalizada)

### 3. Teste a Integração
- Faça uma compra de teste
- Verifique se o usuário foi criado no Supabase
- Confirme se o acesso foi liberado

---

## 🎯 Mapeamento de Planos

O sistema identifica automaticamente o plano baseado no valor da compra:

| Valor da Compra | Plano Identificado | Duração |
|-----------------|-------------------|---------|
| R$ 47,90 | Mensal | 30 dias |
| R$ 97,90 | Semestral | 180 dias |
| R$ 147,90 | Anual | 365 dias |

---

## 📊 O que Acontece Após o Pagamento

1. **Hotmart envia webhook** → Seu servidor
2. **Sistema processa dados** → Extrai informações do comprador
3. **Usuário é criado/atualizado** → No banco Supabase
4. **Acesso é liberado** → Baseado no plano adquirido
5. **Transação é registrada** → Para controle e auditoria

---

## 🗄️ Estrutura do Banco de Dados

### Tabela `users`
- `email` - Email do comprador
- `name` - Nome do comprador
- `plan_type` - Tipo do plano (monthly/semester/annual)
- `plan_status` - Status do plano (active/inactive)
- `plan_expires_at` - Data de expiração
- `hotmart_transaction_id` - ID da transação Hotmart

### Tabela `transactions`
- `user_id` - Referência ao usuário
- `hotmart_transaction_id` - ID da transação
- `product_id` - ID do produto
- `plan_type` - Tipo do plano
- `amount` - Valor pago
- `status` - Status da transação
- `webhook_data` - Dados completos do webhook

---

## 🔍 Logs e Monitoramento

O webhook registra logs detalhados para facilitar o debug:

```javascript
console.log('Webhook recebido da Hotmart:', webhookData)
console.log(`✅ Acesso liberado para ${buyer_email} - Plano: ${planType}`)
```

---

## 🛡️ Segurança

- ✅ Validação de estrutura do webhook
- ✅ Tratamento de erros robusto
- ✅ Logs para auditoria
- ✅ Transações atômicas no banco
- ✅ Suporte a validação de assinatura (opcional)

---

## 🚀 Status da Integração

| Componente | Status |
|------------|--------|
| Endpoint do Webhook | ✅ Implementado |
| Processamento de Pagamentos | ✅ Funcionando |
| Criação de Usuários | ✅ Funcionando |
| Liberação de Acesso | ✅ Funcionando |
| Registro de Transações | ✅ Funcionando |
| Banco de Dados | ✅ Configurado |
| Links de Pagamento | ✅ Atualizados |

---

## 📞 Suporte

Se precisar de ajuda ou encontrar algum problema:

1. Verifique os logs do servidor
2. Confirme se a URL do webhook está correta
3. Teste com uma compra real
4. Verifique se o Supabase está conectado

**A integração está 100% pronta para produção!** 🎉