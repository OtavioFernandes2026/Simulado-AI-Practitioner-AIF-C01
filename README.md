# Simulado AWS Certified AI Practitioner (AIF-C01)

Simulado gratuito e em português para quem está se preparando para a certificação **AWS Certified AI Practitioner (AIF-C01)**.

**Autor:** Otavio Fernandes

> Material de estudo **não oficial**, sem vínculo com a AWS ou com a Amazon. As questões são originais e seguem o estilo da prova real, mas não são questões da prova.

## Funcionalidades

- **60 questões por tentativa**, sorteadas de um banco de **82 questões**, respeitando o peso de cada domínio do exame.
- **Questões de uma ou duas respostas** ("Escolha duas"), como na prova real. A questão só conta como certa se todas as respostas estiverem corretas.
- **Embaralhamento** das questões sorteadas e das alternativas a cada tentativa.
- **Cadastro** (nome, e-mail e WhatsApp opcional) antes de iniciar.
- **Cronômetro** de 90 minutos.
- **Resultado final** com a média geral. A aprovação exige no mínimo **70%** de acertos.
- **Desempenho por domínio**, com a porcentagem de acertos e a indicação dos domínios que precisam ser estudados (abaixo de 70%).
- **Revisão** das questões erradas, com a resposta correta.
- **QR Code PIX** fixo no canto da tela, para quem quiser contribuir com o projeto.
- Funciona no celular e no computador, com tema claro e escuro.

## Domínios cobertos

| Domínio | Peso na prova |
|---|---|
| 1. Fundamentos de IA e ML | 20% |
| 2. Fundamentos de IA Generativa | 24% |
| 3. Aplicações de Modelos de Fundação | 28% |
| 4. Diretrizes para IA Responsável | 14% |
| 5. Segurança, Conformidade e Governança para Soluções de IA | 14% |

Na prova oficial a nota vai de 100 a 1000, com mínimo de 700. Neste simulado, usamos porcentagem simples (mínimo de 70%).

## Estrutura do projeto

```
.
├── index.html       # aplicação completa (HTML, CSS e JavaScript)
├── pix-qrcode.png   # QR Code PIX exibido no canto da tela
├── capa-simulado.webp # imagem da tela inicial (o botão "Iniciar simulado" é clicável)
└── README.md
```

Não há dependências, build nem servidor. É um site estático.

## Como rodar localmente

Abra o arquivo `index.html` no navegador. Se preferir um servidor local:

```bash
python3 -m http.server 8000
# acesse http://localhost:8000
```

## Como publicar

### GitHub

1. Crie um repositório e envie os arquivos `index.html`, `pix-qrcode.png` e `README.md`.

### Vercel

1. Acesse a Vercel e clique em **Add New > Project**.
2. Importe o repositório do GitHub.
3. Clique em **Deploy**. Não é necessária nenhuma configuração (projeto estático).

A cada novo commit no GitHub, a Vercel publica a atualização automaticamente.

## Receber os cadastros gratuitamente (Google Planilhas)

Os cadastros e os resultados podem ser enviados para uma planilha do Google, sem custo.

1. Crie uma planilha no Google Planilhas e, na primeira linha, escreva: `Data | Tipo | Nome | E-mail | WhatsApp | Nota`.
2. Vá em **Extensões > Apps Script**, apague o conteúdo e cole:

   ```js
   function doPost(e) {
     const s = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
     const d = JSON.parse(e.postData.contents);
     s.appendRow([new Date(), d.tipo, d.nome, d.email, d.whats, d.nota || ""]);
     return ContentService.createTextOutput("ok");
   }
   ```

3. Clique em **Implantar > Nova implantação**, tipo **App da Web**, com **Executar como: Eu** e **Quem pode acessar: Qualquer pessoa**.
4. Copie a URL gerada e cole na constante `SHEET_URL` do `index.html`:

   ```js
   const SHEET_URL = "https://script.google.com/macros/s/SEU_ID/exec";
   ```

5. Faça o commit. Enquanto `SHEET_URL` estiver vazio, nenhum dado é enviado.

**Atenção:** como você passa a armazenar dados pessoais de outras pessoas, a LGPD se aplica. Mantenha a planilha privada e use os dados apenas para a finalidade informada no consentimento do cadastro.

## Como editar o simulado

### Trocar o QR Code PIX

Substitua o arquivo `pix-qrcode.png` por outro com o mesmo nome.

### Alterar a nota mínima ou o tempo

No início do script do `index.html`:

```js
const MIN = 70, MINUTOS = 90;
```

### Adicionar questões

Inclua novos objetos no array `BANK`:

```js
{
  d: 3,                       // domínio (1 a 5)
  q: "Enunciado da questão…",
  o: ["Alternativa correta", "Alternativa B", "Alternativa C", "Alternativa D"],
  a: 0                        // índice da alternativa correta (começa em 0)
}
```

Para questões de duas respostas, use 5 alternativas e `a: [0, 1]`, com "(Escolha duas.)" no enunciado.

O sorteio usa a cota por domínio definida em `QUOTA` (12, 14, 17, 8 e 9 questões). Mantenha, em cada domínio, mais questões no banco do que a cota para que as tentativas variem.

Como as alternativas são embaralhadas a cada tentativa, a posição da resposta correta no código não importa.

## Autor

Criado por **Otavio Fernandes**.

Gostou do projeto? Escaneie o QR Code PIX exibido no site para contribuir.
