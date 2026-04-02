# 🐞 Bug Report

## Título
Cupom cumulativo de desconto (PROMO10) não recalculou ao aumentar a quantidade do mesmo produto

---

## Ambiente
- Browser: Chrome 123  
- Sistema Operacional: Windows 11  
- Dispositivo: Desktop  
- URL: TBD  
- Versão do App: TBD  
- Estado da Conta: TBD  

---

## Passos para Reproduzir
1. Logar no site da Zara  
2. Adicionar o item "Vestido" no carrinho  
3. Adicionar o cupom cumulativo **PROMO10 - R$ 30,00**  
4. Aumentar a quantidade do item de **1 para 2**  
5. Observar o valor total do produto e do desconto  

---

## Resultado Obtido
O desconto do segundo produto no valor de **R$30,00** não foi adicionado.

---

## Resultado Esperado
O desconto é cumulativo e deverá ser considerado a cada quantidade de produto adicionada.  
Neste caso, o valor total do desconto deveria ser **R$60,00**.

---

## Severidade
**TBD**

---

## Prioridade
**Alta (P1)**  
Justificativa: Impacta diretamente o cálculo de desconto e experiência do usuário, podendo gerar perda financeira e inconsistência na compra.

---

## Evidência
- `calculo-desconto.png`