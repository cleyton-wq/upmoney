# 🚀 Sistema de Fluxo Automatizado UP Money

## 📋 Visão Geral

O sistema UP Money foi configurado com um fluxo automatizado que integra a Landing Page de Vendas com o aplicativo completo, permitindo acesso automático após confirmação de pagamento da Hotmart.

## 🔄 Como Funciona o Fluxo

### 1. **Experiência Inicial - Landing Page**
- Usuários novos veem a Landing Page de Vendas completa
- Botões de compra redirecionam para checkout da Hotmart
- Botão "Já comprei" permite acesso direto via email

### 2. **Processo de Pagamento**
- Cliente clica em um dos planos (Mensal, Semestral, Anual)
- Redirecionamento para Hotmart com links específicos:
  - **Mensal**: `https://pay.hotmart.com/J102711621S?off=c0c94yc8`
  - **Semestral**: `https://pay.hotmart.com/J102711621S?off=hknpdaks`
  - **Anual**: `https://pay.hotmart.com/J102711621S?off=dijt8g94`

### 3. **Confirmação Automática via Webhook**
- Hotmart envia webhook para: `/api/webhook/hotmart`
- Sistema processa automaticamente:
  - Extrai dados do comprador (email, nome, transaction ID)
  - Determina tipo de plano baseado no valor pago
  - Cria/atualiza registro do usuário no Supabase
  - Define data de expiração baseada no plano

### 4. **Liberação de Acesso**
- **Opção 1**: Cliente volta ao site e clica "Já comprei"
- **Opção 2**: Sistema detecta automaticamente usuário logado
- Verificação de acesso baseada no email
- Redirecionamento automático para o aplicativo completo

## 🗄️ Estrutura do Banco de Dados

### Tabela `users`
```sql
- id (UUID, Primary Key)
- email (String, Unique)
- name (String)
- plan_type ('monthly' | 'semester' | 'annual')
- plan_status ('active' | 'inactive' | 'cancelled')
- plan_expires_at (DateTime)
- hotmart_transaction_id (String)
- created_at (DateTime)
- updated_at (DateTime)
```

### Tabela `transactions`
```sql
- id (UUID, Primary Key)
- user_id (UUID, Foreign Key)
- hotmart_transaction_id (String)
- product_id (String)
- plan_type ('monthly' | 'semester' | 'annual')
- amount (Number)
- status ('completed' | 'cancelled' | 'refunded')
- webhook_data (JSON)
- created_at (DateTime)
```

## 🔧 Configurações dos Planos

### Durações
- **Mensal**: 30 dias
- **Semestral**: 180 dias (6 meses)
- **Anual**: 365 dias (12 meses)

### Detecção Automática por Preço
- Valor >= R$ 140,00 → Plano Anual
- Valor >= R$ 90,00 → Plano Semestral
- Valor < R$ 90,00 → Plano Mensal

## 🛡️ Sistema de Verificação de Acesso

### Verificação por Email
```typescript
// Endpoint: /api/check-access
// Método: GET ou POST
// Parâmetros: email ou transactionId
```

### Critérios de Acesso
1. ✅ Usuário existe no banco
2. ✅ `plan_status = 'active'`
3. ✅ `plan_expires_at > data_atual`

### Renovação Automática
- Sistema verifica expiração automaticamente
- Atualiza status para 'inactive' se expirado
- Webhook da Hotmart pode reativar automaticamente

## 🔗 Endpoints da API

### Webhook Hotmart
- **URL**: `/api/webhook/hotmart`
- **Método**: POST
- **Função**: Processar pagamentos e liberar acesso

### Verificação de Acesso
- **URL**: `/api/check-access`
- **Método**: GET/POST
- **Função**: Verificar se usuário tem acesso ativo

## 🎯 Fluxo de Usuário Completo

1. **Visitante** → Vê Landing Page
2. **Interessado** → Clica em plano e vai para Hotmart
3. **Comprador** → Efetua pagamento na Hotmart
4. **Sistema** → Recebe webhook e processa automaticamente
5. **Cliente** → Volta ao site e clica "Já comprei"
6. **Sistema** → Verifica email e libera acesso
7. **Usuário** → Acessa aplicativo UP Money completo

## 🔄 Estados da Aplicação

### Landing Page (Estado Inicial)
- Usuário não autenticado
- Sem acesso ativo
- Mostra página de vendas completa

### Verificação de Acesso
- Usuário informa email da compra
- Sistema verifica no banco de dados
- Redireciona para app se válido

### Aplicativo Completo
- Usuário com acesso ativo
- Todas as funcionalidades liberadas
- Dashboard, ferramentas, calculadoras

## 🛠️ Manutenção e Monitoramento

### Logs do Webhook
- Todos os webhooks são logados no console
- Dados salvos na tabela `transactions`
- Facilita debug e auditoria

### Verificação de Status
- Sistema verifica expiração automaticamente
- Atualiza status conforme necessário
- Permite renovações via novos webhooks

## 🔒 Segurança

### Validação de Webhook
- Sistema aceita webhooks da Hotmart
- Processa dados com validação robusta
- Retorna sempre status 200 para evitar reenvios

### Controle de Acesso
- Verificação baseada em email + status ativo
- Expiração automática por data
- Sem necessidade de senhas complexas

## 📱 Responsividade

- Sistema funciona em desktop e mobile
- Interface adaptativa
- Experiência consistente em todos os dispositivos

## ✅ Status do Sistema

- ✅ Landing Page configurada
- ✅ Webhook Hotmart integrado
- ✅ Banco de dados estruturado
- ✅ Sistema de verificação de acesso
- ✅ Aplicativo UP Money preservado
- ✅ Fluxo automatizado funcionando

## 🎉 Resultado Final

O sistema está **100% funcional** e permite:

1. **Experiência contínua**: Mesma URL para vendas e aplicativo
2. **Acesso automático**: Liberação imediata após pagamento
3. **Sem redirecionamentos**: Tudo na mesma plataforma
4. **Dados preservados**: Histórico e tabelas do Supabase mantidos
5. **Integração completa**: Hotmart + Supabase + Vercel sincronizados

O usuário compra, o pagamento é aprovado, e o acesso é liberado automaticamente na mesma URL, exatamente como solicitado! 🚀