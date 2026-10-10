# Reprodutor de frequências sonoras

Aplicação responsiva para gerar sinais sonoros de comandos respiratórios, com calibração de frequência e painel de operação. Implementada em um único `index.html`, com CSS, JavaScript e Web Audio API, sem dependências externas.

**Abrir o aplicativo:** https://rleiteoliveira.github.io/reprodutor-frequencias-sonoras/

## Uso

1. Na aba **Ajuste**, selecione uma frequência entre 100 e 800 Hz ou use os presets. Escolha o **Som de puxar e segurar**. Toque em **Testar som** para iniciar o padrão e em **Parar teste** para encerrar.
2. Confirme a percepção pelo caminho de áudio que será usado e clique em **Salvar frequência base**.
3. Na aba **Operação**, o guia opcional sobe o volume durante 1 a 6 segundos antes da sustentação.
4. Um toque em **PUXAR E SEGURAR** inicia o padrão escolhido, repetindo até outro toque no mesmo botão ou outro comando. O cronômetro começa na sustentação.
5. Um toque em **SOLTAR / RESPIRAR** interrompe o comando anterior e reproduz o bip-bip ou, no modo **Áudios gravados**, a gravação de soltar uma vez. Tocar novamente reinicia a reprodução.
6. **Parar som** ou a tecla **Escape** interrompe a reprodução.

Todos os comandos funcionam por clique ou toque, sem manter o botão pressionado. No teclado, use **Espaço** ou **Enter** com o botão em foco. O áudio é desbloqueado no clique; quando disponível, a sessão de áudio é configurada como reprodução de mídia no iOS. Sair da página ou perder o foco encerra o som; retornar não retoma a reprodução automaticamente.

A frequência confirmada e o padrão escolhido ficam salvos no navegador quando o armazenamento local está disponível. As gravações são armazenadas localmente no IndexedDB; não há envio de áudio nem dados da paciente a servidores.

## Áudios personalizados

Na aba **Ajuste**, em **Áudios personalizados**:

1. Toque em **Gravar puxar**, permita o microfone e fale o comando. Toque em **Finalizar** para registrar.
2. Repita com **Gravar soltar**. Cada gravação pode ter até 30 segundos.
3. Use **Ouvir puxar** e **Ouvir soltar** para conferir cada amostra uma vez. Uma nova gravação substitui a anterior somente após ser validada; cancelar mantém a anterior.
4. Toque em **Usar áudios gravados nos comandos**, disponível após registrar os dois áudios.
5. Na operação, **PUXAR E SEGURAR** repete o áudio completo até outro toque ou comando. **SOLTAR / RESPIRAR** interrompe essa repetição e reproduz o outro áudio uma vez. O cronômetro conta desde o início da gravação de puxar; o guia de volume dos tons fica oculto neste modo.

**Excluir puxar** e **Excluir soltar** removem o respectivo áudio deste navegador. Ao excluir um áudio usado pelo modo personalizado, o app volta à sirene. A frequência e os padrões de tom não modificam a voz gravada; o controle de volume continua disponível.

O navegador pede o microfone somente ao gravar, usando HTTPS (como no GitHub Pages) ou localhost. O formato é escolhido entre os suportados pelo navegador, incluindo MP4 ou WebM. O microfone é desligado ao terminar, cancelar ou sair da página. **Parar som** e **Escape** também cancelam uma gravação em andamento.

Os áudios pertencem àquele navegador e aparelho, não ao repositório público. Eles não são sincronizados entre dispositivos e podem desaparecer ao limpar os dados do navegador. Se o armazenamento falhar, o app informa que o áudio vale somente para a sessão atual. Gravações precisam ser testadas no aparelho e interfone usados no exame.

## Padrões sonoros

- **Sirene suave** (opção inicial): varia a frequência em até 15% acima e abaixo da base, em ciclos suaves de 2 segundos. A variação fica entre 100 e 800 Hz; nos extremos, a faixa é limitada. Não aumenta o volume definido.
- **Pulsos espaçados**: um toque de 0,4 segundo seguido de 0,5 segundo de silêncio, repetindo na frequência base. Os ataques e saídas são suaves.
- **Tom contínuo**: sinal constante na frequência base.

O botão **Testar liberação · bip-bip** permite comparar, na aba Ajuste, o sinal de soltar com o de puxar usando a frequência selecionada. A operação usa a frequência base salva. Nos modos de tons, a liberação é uma sequência finita de dois pulsos de 0,25 segundo, separados por 0,18 segundo, em 1,4 vezes a frequência base. No modo **Áudios gravados**, os dois comandos usam suas respectivas gravações.

Esses padrões mudam somente o som dos comandos manuais. Não automatizam a rotina respiratória. A distinção em meio ao ruído da RM precisa ser confirmada com a paciente e a equipe pelo interfone usado no exame.

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
