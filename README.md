
# 📈 CryptoMonitor

**CryptoMonitor** é um aplicativo Android simples que exibe o preço atual do Bitcoin (BTC) utilizando a [API pública do Mercado Bitcoin](https://www.mercadobitcoin.com.br/api-doc/). O app permite atualizar o valor do BTC manualmente através de um botão e exibe a última cotação com data e hora.

## 🛠 Tecnologias Utilizadas

- **Kotlin**
- **Retrofit** – para chamadas REST
- **Gson** – para serialização JSON
- **Coroutines** – para chamadas assíncronas
- **AndroidX AppCompat** – para compatibilidade com várias versões do Android

---

## 📱 Funcionalidades

- Exibe a última cotação do BTC em reais (R$)
- Mostra a data e hora da última atualização
- Botão "Refresh" para atualizar manualmente os dados
- Toasts para exibir mensagens de erro ao usuário

---

## 🧩 Estrutura do Projeto

```
carreiras.com.github.cryptomonitor
├── MainActivity.kt                  # Tela principal do app
│
├── model/
│   └── TickerResponse.kt           # Modelos de dados para o JSON da API
│
├── service/
│   ├── MercadoBitcoinService.kt    # Interface Retrofit para a API
│   └── MercadoBitcoinServiceFactory.kt # Classe factory que configura o Retrofit
```

---

## 🔌 Como Funciona

### 1. `MainActivity.kt`

- Configura a `Toolbar` personalizada.
- Associa o botão "Refresh" para disparar uma chamada à API usando `Retrofit`.
- Usa coroutines para executar a chamada de forma assíncrona.
- Formata e exibe o valor em reais (BRL) e a data da última atualização.

### 2. `MercadoBitcoinService.kt`

Define a interface da API para buscar o ticker de BTC:

```kotlin
@GET("api/BTC/ticker/")
suspend fun getTicker(): Response<TickerResponse>
```

### 3. `MercadoBitcoinServiceFactory.kt`

Cria e configura uma instância do `Retrofit` com a base URL da API:

```kotlin
Retrofit.Builder()
    .baseUrl("https://www.mercadobitcoin.net/")
    .addConverterFactory(GsonConverterFactory.create())
```

### 4. `TickerResponse.kt`

Modela a estrutura da resposta JSON da API:

```json
{
  "ticker": {
    "high": "valor",
    "low": "valor",
    ...
    "date": 1700000000
  }
}
```

---

## 🔄 Exemplo de Funcionamento

- O usuário clica em **"Refresh"**.
- O app chama a URL `https://www.mercadobitcoin.net/api/BTC/ticker/`.
- Se a resposta for bem-sucedida, exibe o valor `last` e a data.
- Se houver erro, exibe uma mensagem correspondente (`404: Not Found`, por exemplo).

---

## 📌 Requisitos

- Android 5.0 (API 21) ou superior
- Conexão com a internet

---

## 🚀 Como Rodar

1. Clone o repositório
2. Abra no Android Studio
3. Execute o projeto em um emulador ou dispositivo real

---

## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
