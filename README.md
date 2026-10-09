# Reprodutor de frequências sonoras

Aplicação responsiva para gerar sinais sonoros de comandos respiratórios, com calibração de frequência e painel de operação. Implementada em um único `index.html`, com CSS, JavaScript e Web Audio API, sem dependências externas.

**Abrir o aplicativo:** https://rleiteoliveira.github.io/reprodutor-frequencias-sonoras/

## Uso

1. Na aba **Ajuste**, selecione uma frequência entre 100 e 800 Hz ou use os presets. Mantenha **Testar som** pressionado para ouvir.
2. Confirme a percepção pelo caminho de áudio que será usado e clique em **Salvar frequência base**.
3. Na aba **Operação**, escolha **Manter pressionado** ou **Alternar / Travar**. O guia opcional sobe o volume durante 1 a 6 segundos antes da sustentação.
4. **PUXAR E SEGURAR** gera o tom base. O cronômetro começa na sustentação. Encerrar esse botão apenas silencia.
5. **SOLTAR / RESPIRAR** interrompe o tom anterior e emite dois pulsos em 1,4 vezes a frequência base.
6. **Parar som** ou a tecla **Escape** interrompe a reprodução.

Os controles momentâneos também funcionam mantendo **Espaço** ou **Enter** pressionado. O áudio começa somente após uma ação do usuário. Sair da página ou perder o foco encerra o som; retornar não retoma a reprodução automaticamente.

A frequência confirmada fica salva no navegador quando o armazenamento local está disponível. A aplicação não coleta nem transmite dados da paciente.

## Executar localmente

Na pasta do projeto:

```sh
python -m http.server 8080
```

Abra `http://localhost:8080`. Para usar no celular com VS Code Port Forwarding, encaminhe a porta **8080** e abra a URL encaminhada.

## Publicação

O GitHub Pages serve a raiz da branch `main`. O arquivo `.nojekyll` permite a publicação estática sem processamento pelo Jekyll. Atualizações enviadas para `main` são republicadas pelo GitHub Pages.

## Validação e uso no exame

Foram verificados em Chromium os controles, envelopes e pulsos de áudio, persistência, teclado, toque/multitouch emulado, interrupções e layouts entre 320 e 844 px, incluindo ampliação de 200%.

A validação em aparelhos físicos Android/iOS e a audibilidade pelo interfone da ressonância ainda precisam ser confirmadas. Os sinais e tempos devem seguir a orientação da equipe responsável. As referências de 10 e 15 segundos são apenas visuais; não há encerramento automático ou recomendação de duração de apneia. A porcentagem de volume não mede pressão sonora.
