# 🖼️ Image Encoder & Decoder

Ferramenta web que converte imagens para texto **Base64** e reconverte o texto de volta para imagem. Criada como solução emergencial quando um cluster de CDN do Discord caiu e as imagens pararam de carregar — em vez de depender de um servidor de imagens, dava pra compartilhar a imagem diretamente como texto e reconstruí-la no outro lado.

🔗 **[Usar a ferramenta](https://ultimatestrength.github.io/image-coder/)**

## 💡 O problema que resolveu

Quando o Discord derruba um cluster de imagens, links de anexo quebram. Com essa ferramenta, você codifica a imagem localmente em Base64, copia o texto gerado, e quem receber cola no decoder para ver a imagem — sem depender de nenhum servidor externo.

## ⚙️ Como funciona

**Codificar (imagem → texto):**
1. Selecione uma imagem pelo input de arquivo
2. Clique em **Codificar Imagem**
3. A imagem aparece na tela e o campo de texto é preenchido com o Base64
4. Copie o texto e compartilhe onde quiser

**Decodificar (texto → imagem):**
1. Cole o código Base64 no campo de texto
2. Clique em **Descodificar Imagem**
3. A imagem é reconstruída e exibida na tela

## 🧠 Como a lógica funciona

Usa a API nativa `FileReader` do browser para ler o arquivo de imagem e convertê-lo para `data URL` (formato `data:image/...;base64,...`). No processo inverso, basta usar o próprio Base64 como `src` de uma tag `<img>` — o browser renderiza diretamente, sem precisar de nenhuma requisição externa.

```js
// Encode
reader.readAsDataURL(file); // → "data:image/png;base64,iVBORw0KGgo..."

// Decode
output.innerHTML = `<img src="${base64}">`;
```

## 🛠️ Tecnologias

- HTML5 / CSS3 / JavaScript (vanilla)
- API `FileReader` nativa do browser
- Projeto inteiro em **um único arquivo** (`index.html`) — zero dependências

## 📌 Contexto

Feito rapidamente durante uma queda do Discord. O projeto inteiro cabe em 54 linhas de HTML — a ideia era ter algo funcional no ar o mais rápido possível, e funcionou.
