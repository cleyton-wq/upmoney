# 🚀 Integração Hotmart - UP Money

## ✅ Configurações Implementadas

### 1. **Parâmetros de Tracking**
- ✅ Sistema automático de captura de parâmetros UTM
- ✅ Tracking de origem do tráfego (Google, Facebook, Instagram, etc.)
- ✅ Parâmetros personalizados para campanhas
- ✅ Persistência de dados de conversão no localStorage

### 2. **URLs de Checkout com Tracking**
- ✅ Todos os botões CTA agora incluem parâmetros de tracking
- ✅ URLs específicas para cada plano (Mensal, Semestral, Anual)
- ✅ Timestamp único para cada clique
- ✅ Abertura em nova aba para melhor experiência

### 3. **API Webhook para Notificações de Vendas**
- ✅ Endpoint: `/api/hotmart/webhook`
- ✅ Processamento de eventos: PURCHASE_COMPLETE, PURCHASE_CANCELED, PURCHASE_REFUNDED
- ✅ Logs detalhados de todas as transações
- ✅ Estrutura preparada para integração com banco de dados

## 🔗 URL do Webhook

**Após publicar seu app, a URL do webhook será:**
```
https://seu-dominio.vercel.app/api/hotmart/webhook
```

**Esta é a URL que você deve configurar na Hotmart no campo "URL para envio de dados".**

## 📊 Parâmetros de Tracking Disponíveis

O sistema captura automaticamente:
- `utm_source` - Origem do tráfego
- `utm_medium` - Meio de marketing
- `utm_campaign` - Campanha específica
- `utm_content` - Conteúdo do anúncio
- `utm_term` - Termo de pesquisa
- `affiliate_id` - ID do afiliado
- `referrer` - Site de origem
- `timestamp` - Momento do clique

## 🎯 Como Usar

### Para Campanhas de Marketing:
```
https://seu-dominio.vercel.app/?utm_source=facebook&utm_medium=cpc&utm_campaign=lancamento2024
```

### Para Afiliados:
```
https://seu-dominio.vercel.app/?affiliate_id=AFILIADO123&utm_source=afiliado
```

## 🔧 Configuração na Hotmart

1. **Acesse o painel da Hotmart**
2. **Vá em Configurações > Webhooks**
3. **Adicione a URL do webhook:** `https://seu-dominio.vercel.app/api/hotmart/webhook`
4. **Selecione os eventos:** PURCHASE_COMPLETE, PURCHASE_CANCELED, PURCHASE_REFUNDED
5. **Salve as configurações**

## 📈 Monitoramento

O sistema registra automaticamente:
- ✅ Todas as conversões com parâmetros de origem
- ✅ Dados de vendas recebidos da Hotmart
- ✅ Logs detalhados no console do servidor
- ✅ Histórico de cliques nos botões CTA

## 🚀 Próximos Passos

1. **Publique o app** para obter a URL pública
2. **Configure o webhook na Hotmart** com a URL gerada
3. **Teste uma compra** para verificar se as notificações estão chegando
4. **Monitore os logs** para acompanhar as vendas em tempo real

## 💡 Recursos Adicionais

- **Sistema de garantia** integrado nos cards de preços
- **Timer de urgência** para aumentar conversões
- **Múltiplos CTAs** estrategicamente posicionados
- **Tracking completo** da jornada do usuário
- **Design responsivo** otimizado para conversão

---

**🎉 Sua integração com a Hotmart está completa e pronta para uso!**