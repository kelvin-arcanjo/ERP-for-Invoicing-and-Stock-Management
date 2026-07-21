# Notas de desenvolvimento — Millennes ERP

Registo de melhorias identificadas durante o trabalho nos layouts de 
impressão/PDF, para tratar em fases futuras. Não são bugs bloqueantes — 
o sistema funciona corretamente sem estas correções.

## Duplicação de lógica

- A mesma regra de negócio (ex: "só mostrar bancos se pagamento = 
  Transferência") está escrita em dois sítios separados: `buildPrintHTML` 
  (impressão via navegador) e `pdfFromDraft` (exportação PDF via jsPDF). 
  Qualquer mudança de regra futura precisa de ser feita nos dois sítios — 
  risco de esquecimento. Possível solução futura: centralizar as regras de 
  negócio numa função só, chamada pelos dois sistemas.

## Robustez / proteção contra falhas

- `initCharts()` ainda não tem proteção `typeof Chart !== "undefined"` 
  internamente — só as duas linhas soltas fora da função (`Chart.defaults...`) 
  foram protegidas. Se o Chart.js falhar ao carregar, `initCharts()` continua 
  a lançar erro (não bloqueia o resto do sistema, mas os gráficos falham).
- O bloco `isCompacto` da tabela de produtos no PDF (POS/A6) não tem 
  proteção de nova página (`doc.addPage()`) como o bloco A4 tem. Faturas 
  com muitos itens podem sair cortadas fora da página em formatos pequenos.

## Impressão HTML (buildPrintHTML) em formatos POS

- Testado em POS 58mm/80mm: legível, mas ainda usa layout de colunas 
  apertadas em vez do layout empilhado (igual ao que já existe no PDF). 
  Foi considerado "aceitável" por agora, mas poderia ganhar consistência 
  visual com o PDF se reescrito com a mesma filosofia (empilhado, 
  centralizado, condicional por formato).

## Dados bancários

- O SWIFT/BIC dos bancos nunca foi implementado no PDF (`pdfFromDraft`), 
  só existe na versão de impressão HTML (`buildPrintHTML`). Adicionar por 
  consistência, se for considerado necessário.

## Responsividade mobile

- Testado o ERP num ecrã de telemóvel: existe rolagem lateral (scroll 
  horizontal), o que é mau UX — o layout não está a adaptar-se corretamente 
  a ecrãs pequenos. Precisa de revisão de CSS (media queries, larguras 
  fixas que podem estar a forçar overflow, grids que não colapsam bem). 
  Não investigado a fundo ainda — só reportado como observação.

## Formatos já testados e validados

| Formato | PDF | Impressão HTML |
|---|---|---|
| A4 | ✅ | ✅ |
| A5 | ✅ | ✅ |
| A6 | ✅ | Não testado |
| POS 58mm | ✅ | ✅ (aceitável) |
| POS 80mm | ✅ | ✅ (aceitável) |
| Carta | Não testado (fórmula proporcional devia cobrir) | Não testado |