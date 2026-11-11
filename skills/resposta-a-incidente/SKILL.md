---
name: resposta-a-incidente
description: Conter, erradicar, recuperar e aprender — com registro do que aconteceu e do que mudou para nao repetir.
---

# Resposta a incidente

## Quando usar

Suspeita ou confirmacao de acesso indevido, vazamento, indisponibilidade causada por terceiro,
credencial exposta.

## Fases

### 1. Detectar e classificar

| Gravidade | Criterio | Resposta |
|---|---|---|
| Critica | dado pessoal vazado, acesso de terceiro confirmado, perda de dado | imediata, interrompe tudo |
| Alta | credencial exposta, vulnerabilidade exploravel em producao | mesmo dia |
| Media | exposicao sem evidencia de uso, configuracao incorreta | prazo curto |
| Baixa | achado teorico, defesa em profundidade ausente | fila normal |

Registre desde o inicio: quando comecou, como foi descoberto, o que se sabe e o que **nao** se sabe.

### 2. Conter

Primeiro parar o sangramento, depois entender. Contencao tipica: revogar credencial exposta,
bloquear origem, desabilitar conta comprometida, retirar o recurso afetado do ar.

Contencao preserva evidencia: **antes** de limpar, guarde registro de log, estado e artefatos. Quem
apaga para "resolver rapido" perde a chance de saber o que aconteceu.

### 3. Erradicar

Encontre a causa raiz, nao o sintoma. Credencial vazou **como**? Acesso entrou por **onde**?
Corrija a causa e procure o mesmo padrao em outros lugares: a mesma falha costuma existir em mais de
um ponto.

### 4. Recuperar

Restaure a partir de copia confiavel, rotacione tudo que possa ter sido exposto, reverifique os
controles e observe com atencao redobrada por alguns dias.

### 5. Aprender

Analise sem culpabilizacao, focada no sistema:

```
Incidente: <titulo>        Periodo: <inicio> a <fim>
Impacto: <o que foi afetado, quantos, por quanto tempo>
Cronologia: <horario> <fato observado>
Causa raiz: <a condicao que permitiu, nao a pessoa>
Por que nao foi detectado antes: <lacuna de observabilidade>
O que funcionou: <o que limitou o dano>
Acoes: <item> — <dono> — <prazo>
```

Acao sem dono e sem prazo nao e acao.

## Diagnostico: nao adivinhe

- Processo que morre sem registro de log: procure evidencia **externa** (registro de eventos do
  sistema, ferramentas de protecao do ambiente) e correlacione pelo horario exato. Hipotese
  plausivel sem evidencia consome tentativas e credibilidade.
- Servico que parece ativo mas nao trabalha: compare o horario da ultima linha de log com o horario
  de inicio do processo. Indicador auto-reportado ("esta rodando") e sinal fraco.
- Processo reiniciando em laco pode nunca aparecer como falho: observe o contador de reinicios e o
  conteudo do registro, nao apenas o estado.
- Conexao recusada: teste a porta corretamente. Verificacao que apenas confirma que a tentativa
  **terminou** devolve resultado positivo mesmo quando a conexao foi recusada — confirme o estado
  conectado.
- Antes de concluir que algo esta exposto, teste **sem seguir redirecionamento**: um provedor que
  responde com redirecionamento para uma pagina publica faz a verificacao parecer acesso
  autorizado.

## Comunicacao

Informe o que se sabe, o que nao se sabe e o proximo passo, com horario de atualizacao. Nunca
minimize. Quando ha dado pessoal envolvido, siga a obrigacao de notificacao aplicavel.

## Checklist

- [ ] Gravidade classificada
- [ ] Evidencia preservada antes de qualquer limpeza
- [ ] Contencao aplicada e verificada
- [ ] Causa raiz identificada, nao apenas o sintoma
- [ ] Mesmo padrao procurado em outros pontos
- [ ] Credenciais possivelmente expostas rotacionadas
- [ ] Analise com acoes, donos e prazos
- [ ] Lacuna de deteccao endereçada

## Pronto quando

A causa raiz esta corrigida, as credenciais rotacionadas, a lacuna de deteccao fechada, e existe
registro com acoes atribuidas.
