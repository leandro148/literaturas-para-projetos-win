# literaturas-para-projetos-win

Repositório de literaturas e estratégias automatizadas para o **WIN (Mini Ibovespa Futuro)** na B3, usando a linguagem **NTSL** (Nelogica Trading System Language) na plataforma **Profit Chart**.

---

## 📚 Literaturas de Referência

| Arquivo | Conteúdo |
|---|---|
| `Volume Price Analysis.pdf` | Anna Coulling — fundamentos de VPA: como interpretar volume e preço juntos para identificar ação do *smart money* |
| `VP - Market in Profile - James Dalton42.docx` | James Dalton — Market Profile, Value Area, POC, tipos de abertura e comportamento do OTF (Outros Participantes de Prazo) |

---

## 📈 Estratégias NTSL

### `estrategia_vpa_win.nts` — Estratégia VPA para WIN

Estratégia de reversão baseada em **Volume Price Analysis (VPA)** para o Mini Ibovespa Futuro (WIN) na B3.

#### Como funciona

O VPA parte do princípio de que o **volume é a pegada do dinheiro inteligente**. Barras com volume anormalmente alto indicam que grandes players (institucional / *smart money*) estão atuando — seja absorvendo oferta ou distribuindo posições.

**Sinal de COMPRA — Clímax de Venda (Selling Climax):**
1. Barra anterior: volume ≥ `LimiarVolumeSpike` × média + fechamento **abaixo** da abertura (barra de baixa)
2. Barra atual: confirmação com fechamento **acima** da abertura (barra de alta)
3. Ação: `BuyAtMarket`

**Sinal de VENDA — Clímax de Compra (Buying Climax):**
1. Barra anterior: volume ≥ `LimiarVolumeSpike` × média + fechamento **acima** da abertura (barra de alta)
2. Barra atual: confirmação com fechamento **abaixo** da abertura (barra de baixa)
3. Ação: `SellShortAtMarket`

#### Parâmetros

| Parâmetro | Padrão | Descrição |
|---|---|---|
| `LimiarVolumeSpike` | `1.5` | Multiplicador acima da média para detectar clímax (1.5 = 50% acima) |
| `PeriodoLookback` | `20` | Número de barras para calcular a média de volume |
| `QuantidadeContratos` | `1` | Contratos WIN por operação |
| `StopLossPontos` | `500` | Stop loss em pontos do WIN (500 pts = R$ 100/contrato) |
| `TakeProfitPontos` | `1000` | Take profit em pontos do WIN (1000 pts = R$ 200/contrato) |

#### Como usar no Profit Chart

1. Abra o **Editor de Estratégias** no Profit Chart.
2. Cole o conteúdo do arquivo `estrategia_vpa_win.nts`.
3. Compile (F5 ou botão Compilar).
4. Aplique ao gráfico do WIN no timeframe desejado (5 ou 15 minutos recomendado).
5. Ajuste os parâmetros conforme seu perfil de risco e faça backtesting antes de operar ao vivo.

---

## ⚠️ Aviso

Este código é fornecido apenas para fins educacionais e de estudo. Faça sempre backtesting extenso e teste em conta simulada antes de operar com capital real.