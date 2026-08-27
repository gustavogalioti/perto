# Perto

Ferramenta simples pra achar seu grupo em eventos lotados (shows, festas, festivais) —
sem cadastro, sem senha, sem app pra baixar.

## Como funciona

1. Alguém abre o site e cria uma sala (ou você abre um link de sala já existente).
2. Digita o nome — só isso, nada de senha ou e-mail.
3. O site pede permissão de localização.
4. Todo mundo que está na mesma sala aparece como uma bolinha colorida num radar,
   indicando a direção e a distância até cada pessoa.
5. Tem um chat dentro da sala pra combinar o encontro. Nada fica salvo: fechou a
   página, a sessão acaba.

## Rodando localmente

É um único arquivo estático (`index.html`), sem build. Basta abrir num servidor
HTTP local (navegadores bloqueiam geolocalização em `file://`):

```bash
python3 -m http.server 8000
```

Depois acesse `http://localhost:8000`.

> Localização exige HTTPS (ou `localhost`) para funcionar — em produção, use GitHub
> Pages, Vercel, Netlify ou qualquer host com HTTPS.

## Como está feito

- HTML/CSS/JS puro, sem framework, sem build step.
- Sincronização de localização e chat entre os participantes da sala usa um
  armazenamento chave-valor efêmero e compartilhado por sala — não é um banco de
  dados permanente nem fica ligado a qualquer identidade.
- Direção calculada com fórmulas de bearing/distância (haversine) entre as
  coordenadas de cada participante.
- Bússola do aparelho (quando disponível) gira o radar; sem ela, o radar fica
  fixo com o norte para cima.

## Próximos passos (ideias em aberto)

- Backend próprio com WebSocket para sincronização em tempo real mais robusta.
- Precisão/robustez de localização em ambientes muito populosos (GPS ruim em
  estádios, por exemplo).
- Expiração/latência do "sinal" de cada participante mais inteligente.
- Personalização de cor/avatar por usuário.
