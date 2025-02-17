# Iugu

Gem para acesso a API da Iugu

## Features / Diferenças para a gem oficial

* Adicionado método para verificar conta (marketplace);
* Adicionado método para capturar fatura em pagamento de duas etapas;
* Contém solução proposta na PR <https://github.com/iugu/iugu-ruby/pull/29>

## Instalação

Adicione essa linha ao Gemfile de sua aplicação:

```ruby
gem "iugu-api-sdk", "~> 1.0.0"
```

Depois execute:

```ruby
bundle install
```

Ou instale você mesmo com:

```ruby
gem install iugu-api-sdk
```

## Exemplos de Uso

```ruby
# Configure seu api key
Iugu.api_key = SEU_TOKEN_DE_API

Iugu::Charge.create(token: "TOKEN DO IUGU.JS ou LIB",
                    email: "endereço do email do cliente",
                    months: "quantidade de parcelas",
                    items: [
                      {
                        description: "Item Teste",
                        quantity: "1",
                        price_cents: "1000"
                      }
                    ])

# Exemplo de Gestão de Assinaturas em meia dúzia de linhas.
# Com direito a pagamento recorrente via Cartão ou Boleto.
# No caso de Cartão, recomenda-se vincular um token ao customer (Default Payment Method).
customer = Iugu::Customer.create(email: "EMAIL DO CLIENTE", name: "NOME DO CLIENTE")

subscription = Iugu::Subscription.create(plan_identifier: "basic_plan", customer_id: customer.id)

# Exemplo de Downgrade/Upgrade de Conta
# (Com cálculo automático de diferença de valores entre planos, créditos, etc)
subscription.change_plan("novo_plano")

# Histórico de Pagamentos do Cliente
customer.invoices
```

## Documentação

A API da Iugu tem uma documentação pública e disponível no [link](https://dev.iugu.com/v1.0/reference).
