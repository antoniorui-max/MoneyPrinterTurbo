# Guia em português: criar vídeos virais com o MoneyPrinterTurbo

O MoneyPrinterTurbo cria vídeos curtos automaticamente: escreve (ou usa) um roteiro, grava a narração com voz de IA, procura imagens de fundo, põe legendas e música, e junta tudo num vídeo vertical pronto para o TikTok.

## 1. O que precisas

- Um computador (Windows, Mac ou Linux). Não funciona no telemóvel.
- **Python 3.11** ou mais recente: https://www.python.org/downloads/ (no Windows, marca "Add Python to PATH" durante a instalação).
- **Chave da Pexels** (grátis, para os vídeos de fundo): cria conta em https://www.pexels.com/api/ e copia a "API Key".
- **Chave de IA** para escrever roteiros sozinho (opcional se fores tu a escrever o roteiro). A mais fácil e com plano grátis é a do **Google Gemini**: https://aistudio.google.com/app/apikey
- A voz (Edge TTS) é grátis e não precisa de chave.

## 2. Instalar

Abre o Terminal (Mac/Linux) ou o PowerShell (Windows) e corre:

```shell
git clone https://github.com/antoniorui-max/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
python -m pip install uv
uv python install 3.11
uv sync --frozen
```

Se não tens o `git`, carrega em **Code → Download ZIP** na página do repositório, extrai a pasta e abre o terminal dentro dela.

## 3. Abrir o programa

- Windows: dá duplo clique em `webui.bat`
- Mac/Linux: `sh webui.sh`

Abre-se uma página no navegador. Na primeira vez:

1. Em cima, muda o idioma da interface (se aparecer em chinês, procura o menu de idioma e escolhe English).
2. Abre as **definições básicas** e:
   - em **LLM Provider** escolhe **Gemini** e cola a tua chave;
   - em **Pexels API Key** cola a chave da Pexels;
   - guarda.

## 4. Definições recomendadas para o teu perfil (autossuperação)

| Opção | Valor |
|---|---|
| Video aspect | **9:16** (vertical) |
| Video language | **pt-PT** (ou pt-BR se o público for do Brasil) |
| Voz (Azure TTS V1) | **pt-PT-DuarteNeural-Male** (voz masculina calma) ou **pt-BR-AntonioNeural-Male** |
| Velocidade da voz | 0.9 a 1.0 (mais calma = mais emoção) |
| Legendas | ligadas, modo **word_by_word**, animação **pop_spring** |
| Fonte | **BeVietnamPro-Bold.ttf** (aceita acentos portugueses) |
| Tamanho da fonte | 70 a 80 |
| Posição das legendas | **center** |
| Música | random, volume 0.2 |
| Duração de cada clipe | 3 segundos (cortes rápidos prendem a atenção) |

**Importante:** a fonte padrão é chinesa e pode falhar nos acentos (ã, ç, é). Usa sempre a BeVietnamPro.

## 5. Criar um vídeo

- **Automático:** escreve só o tema, por exemplo *"Nunca desistas dos teus sonhos"*, e carrega em **Generate Video**. A IA escreve o roteiro em português.
- **Com o teu roteiro:** cola o texto completo na caixa do roteiro. Assim controlas cada palavra (recomendado para começar).

Para a IA escrever no teu estilo, cola isto no campo de prompt personalizado:

> Escreve um roteiro de 30 segundos em português para TikTok sobre autossuperação. Começa com uma frase-gancho forte nos primeiros 2 segundos. Frases curtas, tom calmo e verdadeiro, fala direto para quem está a ver ("tu"). Termina pedindo para guardar o vídeo e marcar alguém.

O vídeo pronto fica na pasta `storage/tasks/`.

## 6. Criar 5 vídeos de uma vez

O ficheiro [`exemplos/autossuperacao.json`](exemplos/autossuperacao.json) tem 5 roteiros de autossuperação prontos ("Ninguém acreditava em mim", "Se estás a pensar em desistir…", "3 coisas que aprendi quando perdi tudo", etc.). Com a chave da Pexels configurada, corre:

```shell
uv run python cli.py --batch-file exemplos/autossuperacao.json --video-language pt-PT --voice-name pt-PT-DuarteNeural-Male --font-name BeVietnamPro-Bold.ttf --font-size 75 --subtitle-position center --subtitle-display-mode word_by_word --subtitle-animation pop_spring --video-clip-duration 3
```

Como os roteiros já estão escritos, isto nem precisa da chave de IA. Podes editar o ficheiro e trocar os textos pelos teus.

## 7. Dicas para viralizar

- Os primeiros 2 segundos decidem tudo: começa com a frase mais forte.
- No TikTok, troca a música por um som em alta (piano ou épico).
- Publica 1 a 3 vídeos por dia e repete os temas que tiverem mais visualizações.
- Termina sempre com uma chamada: "guarda este vídeo", "marca quem precisa ouvir isto".

## Problemas comuns

- **"Pexels API key" em falta:** volta às definições básicas e cola a chave.
- **Letras estranhas nas legendas:** muda a fonte para BeVietnamPro-Bold.ttf.
- **Erro de LLM:** confirma a chave do Gemini, ou cola o roteiro tu mesmo.
- Ficheiro `config.toml`: é onde ficam as tuas chaves. **Nunca o envies para o GitHub.** (já está protegido no `.gitignore`)
