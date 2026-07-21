# PREÇO INTELIGENTE

Ferramenta simples para precificação de diárias em pousadas e pequenos hotéis.

## ✨ Funcionalidades

- **Cálculo automático de tarifas** por número de hóspedes
- **Parâmetros configuráveis**: custo fixo, café, ar-condicionado, margem de lucro, desconto
- **Tabela dinâmica** com até 10 hóspedes por quarto
- **Visão geral** com estatísticas médias
- **Interface responsiva** e acessível
- **Funciona offline** — apenas HTML/CSS/JavaScript puro

## 📊 Como usar

1. **Ajuste os parâmetros** na seção "Parâmetros Base":
   - **Custo Fixo**: custos operacionais fixos por quarto (energia, limpeza, manutenção)
   - **Café p/ Hóspede**: custo do café da manhã por pessoa
   - **Ar-Condicionado**: custo fixo do uso do ar-condicionado
   - **Margem de Lucro**: valor em R$ que você quer lucrar por hóspede
   - **Máx. de Hóspedes**: capacidade máxima do quarto
   - **Desconto (%)**: percentual de desconto sobre a tarifa bruta

2. **Veja a tabela atualizar** automaticamente com custos e lucros por hóspede

3. **Use o manual** para entender cada parâmetro em detalhes

## 📐 Fórmulas

Para cada número de hóspedes (pax):

```
Custo Total = Custo Fixo + (Café × pax) + Ar-Condicionado
Tarifa Bruta = Custo Total + (Margem × pax)
Desconto = Tarifa Bruta × (percentual/100)
Tarifa Final = Tarifa Bruta - Desconto
Lucro Líquido = Tarifa Final - Custo Total
% Lucro = (Lucro Líquido / Tarifa Final) × 100
```

### Cores do % Lucro

| Cor | Faixa | Significado |
|-----|-------|-------------|
| 🟢 Verde | ≥ 45% | Ótimo |
| 🟡 Amarelo | 35% - 44% | Aceitável |
| 🟠 Laranja | < 35% | Atenção |
| 🔴 Vermelho | < 0% | Prejuízo |

## 📋 Exemplo

Usando os valores do `tarifa minima.csv`:

| pax | custo | café | ar | margem | bruto | 15% desc | c/desc | lucro líq | % lucro |
|-----|-------|------|----|--------|-------|----------|--------|-----------|---------|
| 1 | R$ 50 | R$ 33 | R$ 50 | R$ 67 | R$ 200 | -R$ 30 | R$ 170 | R$ 37 | 22% |
| 2 | R$ 50 | R$ 67 | R$ 50 | R$ 133 | R$ 300 | -R$ 45 | R$ 255 | R$ 88 | 35% |
| 3 | R$ 50 | R$ 100 | R$ 50 | R$ 200 | R$ 400 | -R$ 60 | R$ 340 | R$ 140 | 41% |
| 4 | R$ 50 | R$ 133 | R$ 50 | R$ 267 | R$ 500 | -R$ 75 | R$ 425 | R$ 192 | 45% |
| 5 | R$ 50 | R$ 167 | R$ 50 | R$ 333 | R$ 600 | -R$ 90 | R$ 510 | R$ 243 | 48% |

## 🛠️ Stack Técnica

- **HTML5** semântico (`<main>`, `<h1>`, `<h2>`)
- **CSS3** com Grid e variáveis
- **JavaScript ES6** puro (vanilla)
- **Tipografia**: Playfair Display + Source Sans 3
- **Acessibilidade**: skip link, ARIA labels, contraste WCAG

## 🚀 Deploy

### GitHub Pages

1. Acesse as **Settings** do repositório
2. Em **Pages**, selecione **Source**: `main` branch
3. O site será publicado em `https://jasonbralli.github.io/preco_inteligente/`

### Local

Basta abrir o `index.html` no navegador — não requer servidor web.

## 📁 Estrutura

```
.
├── index.html          # Aplicação principal
├── test.html           # Testes unitários
├── RELATORIO.md        # Relatório técnico
├── .gitignore          # Arquivos ignorados pelo Git
├── tarifa minima.csv   # Dados de exemplo
└── README.md           # Esta documentação
```

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch (`git checkout -b feature/nova-funcionalidade`)
3. Commit suas mudanças (`git commit -m 'feat: nova funcionalidade'`)
4. Push para a branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

## 📄 Licença

MIT — use livremente em seus projetos.