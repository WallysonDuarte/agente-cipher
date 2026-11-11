---
name: gestao-de-segredos
description: Manter credenciais fora do codigo, com cofre, rotacao, varredura de historico e permissoes corretas.
---

# Gestao de segredos

## Quando usar

Sempre. E imediatamente ao suspeitar de exposicao.

## Regras absolutas

1. **Nenhum segredo no repositorio.** Nem em arquivo de exemplo, nem comentado, nem em teste.
2. **Nenhum segredo em registro de log**, mensagem de erro, relatorio ou nota tecnica.
3. **Nenhum segredo impresso na saida de comando.** Ao depurar, mascare antes de imprimir — e
   lembre que mascarar apenas o parametro de senha nao cobre a forma com credencial embutida no
   endereco. Mascare as duas.
4. **Arquivo de credencial com permissao restritiva**, dono igual a conta do servico.
5. **Local canonico unico** para credenciais operacionais, fora de qualquer arvore versionada.

## Cofre

Com cofre habilitado, o arquivo de configuracao versionado contem **apenas valores vazios ou
marcadores**. Valor real nunca aparece ali.

Pontos de atencao:

- Aplicacao que resolve segredo apenas na partida exige reinicio do servico depois de qualquer
  mudanca de valor.
- Se a resolucao acontece por substituicao de marcador, criar a chave no cofre **nao surte efeito**
  enquanto o campo na configuracao for um valor literal. Troque o literal pelo marcador.
- Configuracao por ambiente: o arquivo base e carregado junto. Todo marcador presente no base que o
  arquivo do ambiente nao sobrescrever continua resolvendo o ambiente errado.
- Se o servico de segredos limita requisicoes, reiniciar muitos servicos ao mesmo tempo pode
  esgotar o limite. Reinicie de forma escalonada.
- Cliente que engole o erro e devolve vazio faz causas diferentes parecerem o mesmo problema. Leia
  o codigo do cliente antes de culpar o servidor.

## Varredura de historico

Estado atual limpo nao significa historico limpo. Varra o historico completo do repositorio por
padroes de credencial. Segredo que **ja** foi enviado ao repositorio esta comprometido: reescrever
o historico nao basta, e preciso **rotacionar**.

Varredura de padrao de credencial em texto gravado precisa escapar corretamente os caracteres
especiais do proprio padrao.

## Rotacao

- Periodicamente, e **imediatamente** apos qualquer suspeita de exposicao.
- Sequencia: gerar novo valor, atualizar no cofre, reiniciar quem consome, invalidar o valor antigo
  — nessa ordem, para nao derrubar o servico.
- Chave desatualizada guardada no arquivo de credencial e causa silenciosa de recusa de acesso
  meses depois. Compare o resumo do valor guardado com o registrado no servico.

## Criptografia de campo

Para dado sensivel em repouso: chave derivada, cifra autenticada, prefixo de versao no valor,
leitura dupla durante a troca de chave, indice cego para busca por igualdade, e migracao
idempotente com reversao.

Nunca armazene a senha tentada numa falha de login. Nunca trate uma imagem capturada como fator de
autenticacao.

## Checklist

- [ ] Nenhum segredo no repositorio, nem no historico
- [ ] Arquivo de configuracao versionado com valores vazios quando o cofre esta ativo
- [ ] Permissao e dono dos arquivos de credencial corretos
- [ ] Nenhum segredo em log, erro, relatorio ou nota
- [ ] Mascaramento cobrindo tambem credencial embutida em endereco
- [ ] Rotacao feita apos qualquer exposicao
- [ ] Servicos reiniciados um por vez apos mudanca no cofre

## Pronto quando

A varredura do historico nao encontra credencial, o servico funciona lendo tudo do cofre, e nenhum
valor real existe em arquivo versionado.
