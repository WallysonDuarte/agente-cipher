---
name: endurecimento-de-infraestrutura
description: Reduzir superficie de ataque: exposicao minima, acesso por chave, cabecalhos de seguranca e isolamento de servicos.
---

# Endurecimento de infraestrutura

## Quando usar

Novo ambiente, revisao periodica, apos incidente, antes de expor um servico novo.

## Exposicao: a regra mais importante

**Nenhum servico novo escuta em interface publica.** Tudo escuta apenas em interface local e e
exposto exclusivamente pelo proxy reverso, atras de terminacao TLS.

Se uma tarefa parecer exigir abertura de porta, **pare e questione**: a resposta quase sempre e
usar o proxy que ja existe.

Verificacao: liste as portas em escuta e confirme que nenhuma esta vinculada a interface publica
sem necessidade justificada e registrada.

## Acesso administrativo

- Autenticacao por chave; autenticacao por senha desabilitada.
- Acesso direto com a conta de maior privilegio desabilitado.
- Bloqueio automatico apos tentativas repetidas.
- Lista de origens permitidas para acesso administrativo, quando aplicavel — e lembrar que a
  origem do operador muda: mantenha a anterior na lista para nao se trancar fora.

Atencao: uma tentativa com usuario errado pode acionar o bloqueio automatico e derrubar o proprio
acesso. Copie o usuario do roteiro que ja funciona em vez de tentar adivinhar.

## Cabecalhos de seguranca

Obrigatorios na resposta de todo dominio:

| Cabecalho | Valor |
|---|---|
| transporte estrito | periodo longo, incluindo subdominios |
| tipo de conteudo | sem adivinhacao |
| enquadramento | negado ou mesma origem |
| politica de referencia | restritiva |
| politica de permissoes | somente o necessario |
| politica de conteudo | restritiva, sem estilo nem script em linha |

**Armadilha critica:** declarar um cabecalho dentro de um bloco de local cancela a heranca de
**todos** os cabecalhos declarados no bloco do servidor. Ao acrescentar um cabecalho num bloco de
local, repita explicitamente todos os de seguranca ali.

Ao conferir por linha de comando, case o nome **completo** do cabecalho: um prefixo que nao bate
com o separador nao encontra o cabecalho mesmo quando ele esta presente — e isso gera alarme falso.

## Containers

- Processo sem privilegio elevado; sistema de arquivos somente leitura onde possivel.
- Nenhuma capacidade extra sem necessidade.
- Rede interna dedicada; somente o proxy alcanca os servicos.
- Imagem base minima e atualizada.
- Verificacao de saude apontando para a interface local por endereco numerico: a resolucao de nome
  pode falhar em imagem minima sem alternativa.

## Arquivos de configuracao

- Permissao restritiva (leitura apenas para o dono e o grupo do servico), nunca legivel por todos.
- Dono igual a conta que executa o servico. Ajuste de dono em lote pode deixar o arquivo de
  configuracao ilegivel pelo servico e derrubar a aplicacao em laco de reinicio.
- Nenhum arquivo de configuracao de servidor na raiz publicada pelo servidor web.

## Backup de configuracao

Copia de seguranca de configuracao do servidor web **nunca** fica no diretorio que o servidor
carrega: cada arquivo ali e configuracao ativa, e a copia duplica os nomes de dominio, gerando
avisos que escondem erros reais. Mova para fora imediatamente.

## Higiene

- Remover pacotes temporarios, diretorios de publicacao aninhados e backups antigos apos confirmar
  estabilidade.
- Arquivo de backup de configuracao esquecido em diretorio temporario e exposicao de segredo: ao
  encontrar, sinalize — mas nao apague o que outra pessoa criou sem autorizacao.
- Atualizacoes de seguranca do sistema aplicadas automaticamente.

## Checklist

- [ ] Nenhum servico escutando em interface publica sem justificativa registrada
- [ ] Acesso administrativo por chave, sem senha, com bloqueio automatico
- [ ] Seis cabecalhos de seguranca presentes em todos os dominios
- [ ] Cabecalhos repetidos em cada bloco de local que declara cabecalho proprio
- [ ] Containers sem privilegio, em rede interna
- [ ] Permissao e dono dos arquivos de configuracao conferidos
- [ ] Backup de configuracao fora do diretorio carregado
- [ ] Temporarios e backups antigos removidos

## Pronto quando

A varredura de portas nao mostra exposicao inesperada, todos os dominios respondem com os
cabecalhos, e a aplicacao continua funcionando depois do endurecimento.
