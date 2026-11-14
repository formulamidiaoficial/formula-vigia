# Vigia de fora

Testa, a cada 5 minutos e **de fora** do servidor, se os sistemas da Fórmula Mídia
respondem: `app.formulamidia.com.br`, `chat.formulamidia.com.br` e
`crm.formulamidia.com.br`. Roda no GitHub Actions, então continua funcionando
quando o próprio servidor cai, que é justamente quando o alarme de dentro dele
não consegue avisar.

## Como avisa

| Situação | O que acontece |
|---|---|
| Caiu | A rodada fica vermelha e o GitHub manda e-mail ao dono do repositório (e notificação no app do GitHub). |
| Continua fora | Uma nova rodada vermelha por hora, como lembrete. |
| Voltou | O estado volta a "ok". Com o ntfy ligado (abaixo), chega o aviso de volta. |

Um endereço só conta como fora depois de 3 tentativas com 40 s entre elas.
Pedir login (401/403) conta como estar de pé.

## Ligar o aviso no celular (ntfy), opcional

Em **Settings › Secrets and variables › Actions › New repository secret**, crie
`NTFY_URL` com o mesmo endereço do canal da sentinela. Esse endereço funciona
como senha: ele vai do arquivo direto para a caixa do site, nunca para chat,
terminal ou código.

## Testar

**Actions › vigia › Run workflow**, marcando "Simular uma queda": a rodada fica
vermelha e o e-mail chega. Rode de novo sem marcar para voltar ao "ok".

## Por que este repositório é público

Repositório público tem minutos de GitHub Actions ilimitados. Um vigia a cada
5 minutos gastaria ~8.600 minutos por mês num repositório privado. Aqui só
há os três endereços públicos e o estado (`estado.txt`), nenhum segredo.
