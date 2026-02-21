**Análise de Logs - SSH Brute Force**

Projeto focado em auditoria de segurança e análise forense de logs no Linux (auth.log). O objetivo aqui foi identificar padrões de ataques automatizados e validar acessos legítimos.

**O Cenário**

Subi um servidor exposto à internet e, em pouco tempo, os logs de autenticação começaram a registrar tentativas de invasão. Este repositório contém o dump desses logs e a metodologia que usei para filtrar os ataques.

**Ferramentas Utilizadas**

Para não perder tempo abrindo arquivo gigante na mão, usei o básico de sobrevivência no terminal Linux:

grep: Para filtrar as falhas e sucessos.

awk: Para isolar os endereços IP e nomes de usuários.

sort / uniq: Para contar quantas vezes cada IP tentou forçar a entrada.

**O que os logs revelaram**

Após passar o pente fino no auth.log, identifiquei o seguinte:

Ataque de Dicionário: O IP 185.231.247.91 testou usuários comuns como admin e test.

Persistência no Root: O IP 45.91.201.33 focou exclusivamente no usuário root, tentando várias vezes em um curto intervalo de tempo.

Acesso Confirmado: O usuário gabriel logou com sucesso às 05:44:20 (IP 179.209.135.42).

Nota: Em uma auditoria real, eu verificaria se esse IP de origem é conhecido pelo usuário.

**Arquivos do Projeto**

auth.log: O "dump" bruto com as tentativas de login.

relatorio-analise-logs.md: Onde detalhei os comandos que usei e as conclusões da defesa.
