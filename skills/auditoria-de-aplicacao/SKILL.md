---
name: auditoria-de-aplicacao
description: Revisar codigo e comportamento em busca das falhas mais exploradas, confirmando cada achado antes de classificar.
---

# Auditoria de aplicacao

## Quando usar

Antes de publicar pela primeira vez, periodicamente, depois de alteracao em autenticacao ou
autorizacao, e sempre que um relatorio automatizado apontar algo.

## Confirme antes de corrigir

Relatorio automatizado produz falso positivo com severidade alta. Antes de aceitar um achado:

1. **Confirme a rota real no codigo.** Achado que cita um caminho por convencao (um endpoint de
   login "padrao") pode nao existir no projeto; corrigir as cegas desperdica esforco sem reduzir
   risco.
2. **Reproduza o comportamento.** Se nao reproduz, o achado nao e achado.
3. **Compare a data do registro com a data da ultima correcao.** Registro antigo nunca
   reexaminado e causa comum de alarme falso.
4. **Prefira o sintoma observavel ao palpite pelo nome.** Proteger por prefixo de nome de
   subdominio e fragil; usar o codigo de status observado e robusto.

## Falhas que mais aparecem

### Autorizacao por recurso
O defeito mais comum e mais grave. Para cada endpoint que recebe identificador, teste com **duas
contas reais**: ler, listar, alterar, excluir, revelar e renovar o recurso da outra conta.
Inspecao de codigo nao e prova.

Confira tambem a origem da decisao: comparar o dono copiado no registro filho em vez do vinculo
canonico nega acesso ao responsavel atual depois de uma transferencia.

### Injecao
Toda consulta parametrizada. Nenhuma concatenacao de entrada do usuario em comando. Expressao
regular montada com texto do usuario alem de fragil e insegura; e expressao com quantificador
aninhado permite travamento por retrocesso catastrofico — limite o tempo de validacao.

### Atribuicao em massa
Objeto de entrada que o codigo copia inteiro para a entidade permite ao cliente alterar campo que
nao deveria (perfil, situacao, saldo). Use objeto de entrada proprio com apenas os campos
editaveis, e zere os campos de plataforma ao reaproveitar um servico interno num endpoint de
cliente.

### Execucao de script no navegador
Nenhuma insercao de HTML cru vindo do usuario. Conteudo vindo de fonte externa e **dado**, nunca
instrucao. Politica de conteudo restritiva no servidor.

### Requisicao forjada do lado do servidor
Endpoint que busca uma URL informada pelo usuario precisa de lista de destinos permitidos.

### Exposicao de dado
- Listagem administrativa nunca devolve a entidade de usuario (traz o resumo da senha): use objeto
  de resposta proprio.
- Mapa de codigo-fonte publicado expoe o fonte: remova do pacote.
- Documentacao interativa da API habilitada em producao: desabilite fora de desenvolvimento.
- Mensagem de erro com identificador interno ou detalhe tecnico: traduza para mensagem util.

### Limite de tentativas
Login com limite por identidade **e** por origem, bloqueando na tentativa que atinge o limite.
Nunca persista a senha tentada. Resposta de login mantem ambiguidade (nao revela se o usuario
existe), mas mostra erro claro e nao redireciona em silencio.

## Politica de conteudo

Antes de remover a permissao de estilo em linha, descubra a causa: atributo de estilo fixo no HTML
(corrigivel por resumo criptografico) ou biblioteca que injeta estilo em tempo de execucao
(resumo **nao** cobre). Remover sem testar tela a tela arrisca quebrar a interface.

Resumos sao especificos da construcao: recalcule a partir da **resposta servida**, nao do artefato
local, e republique a politica a cada reconstrucao que mude o bloco em linha.

Atencao: a pagina pode receber politica por cabecalho **e** por marcacao; o navegador aplica a
intersecao. Inspecione as duas.

## Checklist

- [ ] Autorizacao por recurso testada entre duas contas
- [ ] Consultas parametrizadas; nenhuma concatenacao de entrada
- [ ] Objeto de entrada proprio, sem atribuicao em massa
- [ ] Nenhuma insercao de HTML cru
- [ ] Limite de tentativas de login por identidade e origem
- [ ] Nenhum dado sensivel em resposta, registro de log ou pacote servido
- [ ] Documentacao interativa desabilitada em producao
- [ ] Cabecalhos de seguranca presentes; politica de conteudo conferida nas duas fontes
- [ ] Cada achado reproduzido antes de classificar

## Pronto quando

Cada achado tem evidencia de reproducao, os criticos estao corrigidos e reverificados, e os aceitos
como risco tem dono e prazo.
