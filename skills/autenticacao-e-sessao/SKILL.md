---
name: autenticacao-e-sessao
description: Implementar autenticacao com token de curta duracao, renovacao rotativa, segundo fator e invalidacao confiavel.
---

# Autenticacao e sessao

## Quando usar

Construcao ou revisao de login, segundo fator, recuperacao de senha, sessao administrativa.

## Tokens

- **Acesso:** curto (15 a 30 minutos), com as reivindicacoes minimas.
- **Renovacao:** longo, rotativo, armazenado de forma segura, invalidado ao ser usado.
- Nenhum dado sensivel dentro do token: ele e legivel por quem o possui.
- Auxiliar de leitura de token precisa tratar a codificacao segura para URL (com caracteres
  substituidos e preenchimento ausente) antes de decodificar — senao a saida ocorre de forma
  aparentemente aleatoria.

### Rotacao e janela de tolerancia

Renovacao rotativa precisa de uma janela curta (cerca de um minuto) em que o token recem-usado
devolve o substituto ainda ativo, em vez de disparar revogacao em massa por suspeita de reuso. Sem
isso, duas abas renovando juntas deslogam o usuario em todo lugar.

## Sessao unica e invalidacao

Quando o requisito e uma sessao por usuario:

- Guarde o identificador de sessao em colecao/tabela **propria**, nao num campo da entidade de
  usuario: uma substituicao completa do documento reverteria o valor.
- Inclua o identificador como reivindicacao do token e recuse token que nao o traga.
- Ofereca encerramento no servidor, nao apenas no cliente.

**Regra importante:** ao corrigir um valor de permissao ou perfil no banco, verifique se existe
sessao ativa emitida sob o valor antigo e **invalide-a**. Senao o usuario continua com o acesso
anterior e o sintoma parece defeito de codigo.

## Segundo fator

- Canal secundario com alternativa: se o canal primario falha, o secundario entra.
- Codigo com validade curta, uso unico, limite de tentativas.
- Codigo nunca aparece em registro de log.
- Conta de demonstracao isenta de segundo fator e excecao autorizada caso a caso, nunca padrao.

## Recuperacao de senha

- Desafio em armazenamento temporario no servidor: identificador, resumo do codigo, contador de
  tentativas, validade curta.
- **Nunca reutilize os campos do codigo de login**: um desafio de recuperacao nao pode ser trocado
  por uma sessao.
- Resposta generica de sucesso mesmo para endereco inexistente, para nao revelar cadastro.
- Ao concluir, rotacione o identificador de sessao, matando as sessoes anteriores.

## Sessao administrativa

- Armazenamento por aba, nao persistente entre reinicios do navegador.
- Sem opcao de "lembrar-me".
- Reivindicacao explicita de privilegio administrativo, verificada no servidor em **toda** rota
  administrativa.
- Teto de duracao e expiracao por inatividade.

Ao verificar um controle administrativo, confirme qual item de contexto o intermediario preenche
para o **tipo de token que a interface realmente envia**. Copiar a verificacao de um endpoint
vizinho nao e prova: valide com um token real do fluxo de login.

## Redirecionamento

Rota que redireciona usuario autenticado com base apenas na existencia do usuario — em vez do
predicado real de autorizacao — vira laco de redirecionamento no instante em que uma sessao carrega
um perfil que falha nesse predicado.

## Checklist

- [ ] Token de acesso curto; renovacao rotativa com janela de tolerancia
- [ ] Nenhum dado sensivel no token
- [ ] Sessao unica em armazenamento proprio, com reivindicacao verificada
- [ ] Sessoes invalidadas apos correcao de perfil ou permissao
- [ ] Segundo fator com alternativa, validade curta e limite de tentativas
- [ ] Recuperacao de senha isolada do fluxo de login
- [ ] Sessao administrativa por aba, com privilegio verificado no servidor
- [ ] Redirecionamento baseado no predicado de autorizacao, nao na existencia de usuario

## Pronto quando

Sessao expira e renova sem expulsar o usuario, acesso cruzado e negado, e correcao de perfil no
banco derruba a sessao antiga.
