---
name: review-gate
description: Confere a entrega contra a spec e a Definição de Pronto antes de abrir PR. Use ao terminar uma feature.
---
1. Releia a spec e liste cada critério Dado/Quando/Então com ✅ ou ❌ e onde foi atendido (arquivo:linha ou teste).
2. Rode lint e testes e mostre o resultado.
3. Procure no diff: segredos, dados reais, `console.log`, código morto, mudanças fora do escopo.
4. Só declare pronto com tudo ✅; caso contrário, liste o que falta.
