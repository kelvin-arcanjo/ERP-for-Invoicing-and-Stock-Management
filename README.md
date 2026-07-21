# Millennes ERP

ERP de faturação e stock com módulos de financeiro, CRM, compras e 
conformidade fiscal (AGT/SAF-T), desenvolvido em HTML, CSS e JavaScript.

## Sobre o projeto

Este repositório contém o código-fonte de um ERP (Enterprise Resource 
Planning) para pequenas e médias empresas, adaptado ao contexto fiscal 
angolano — faturação, inventário, financeiro, CRM, compras e contabilidade 
integrados num único sistema.

O código original foi cedido pelo CEO da Millennes como ponto de partida 
para fins de aprendizagem e desenvolvimento prático.

**Estado atual:** protótipo funcional em fase de desenvolvimento. Não tem 
backend nem base de dados — os dados (clientes, produtos, faturas) existem 
apenas em memória, no navegador, e são perdidos ao recarregar a página.

## Tecnologias

- HTML5, CSS3, JavaScript (vanilla, sem frameworks)
- [Chart.js](https://www.chartjs.org/) — gráficos do dashboard
- [jsPDF](https://github.com/parallax/jsPDF) — geração de faturas em PDF

## O que foi feito nesta fase

Trabalho focado nos layouts de impressão e exportação de faturas, para os 
formatos de papel A4, A5, A6 e POS térmico (58mm/80mm):

- Corrigido bug fatal que impedia carregamento de clientes/produtos quando 
  a biblioteca Chart.js falhava (proteção `typeof`)
- Dados bancários condicionais ao método de pagamento (Transferência)
- Layout de impressão empilhado e centralizado para formatos térmicos 
  (POS 58mm/80mm) no PDF
- Correção de sobreposição de colunas em A5/A6, usando cálculo proporcional 
  em vez de coordenadas fixas
- Layout dedicado para A6 (formato compacto)

Ver `NOTAS.md` para melhorias identificadas e ainda por implementar.

## Como correr o projeto localmente

1. Clonar o repositório
2. Abrir a pasta no VS Code
3. Usar a extensão Live Server (botão "Go Live") para abrir `index.html` 
   no navegador