**Relatório de Análise de Logs - SSH Brute Force**

**1. Objetivo da Análise**

Auditar o arquivo /var/log/auth.log para identificar tentativas de invasão via SSH e validar se acessos legítimos ocorreram no período selecionado.

**2. Metodologia (Comandos Utilizados)**

Para extrair as informações dos logs de forma rápida, utilizei ferramentas nativas do Linux no terminal:

**A. Filtrando tentativas de login com usuários inválidos**
Usei este comando para ver quais nomes de usuários os atacantes estavam tentando chutar:

Bash
grep "invalid user" auth.log | awk '{print $9}' | sort | uniq -c | sort -nr
°Resultado: Identifiquei tentativas para admin, oracle e test.

**B. Identificando os IPs que mais atacaram**
Para isolar quem estava tentando forçar a entrada no servidor:

Bash
grep "Failed password" auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr

Top Ofensores:

° 45.91.201.33 (Focado no root)

° 185.231.247.91 (Tentando múltiplos usuários)

**C. Verificando Logins Bem-Sucedidos**
O comando mais importante para saber se o servidor foi comprometido:

Bash
grep "Accepted password" auth.log

°Evento Detectado: Usuário gabriel logou com sucesso às 05:44:20.

**3. Diagnóstico Técnico**

Atacante IP | Alvo | Comportamento
45.91.201.33| root |Brute-force persistente. Tentativas em intervalos curtos.
185.231.247.91 | admin/test | Scanner de vulnerabilidades (Credential Stuffing).
102.223.94.12 | oracle | Busca por bancos de dados expostos.

**Status de Segurança:** O servidor sofreu uma tentativa de invasão automatizada, mas os ataques foram repelidos. O único acesso bem-sucedido foi do usuário gabriel.

**4. Recomendações de Segurança (Remediação)**

Com base na análise, as seguintes medidas são sugeridas para "fechar" o servidor:

**1. Instalar o Fail2Ban:** Para banir automaticamente IPs que errarem a senha 3 vezes.

**2. Desativar login de Root:** Alterar PermitRootLogin no no arquivo sshd_config.

**3. Mudar a porta do SSH:** Sair da porta padrão (22) para reduzir o barulho de bots.

**4. Autenticação por Chave (Ed25519):** Desativar senhas e usar apenas chaves criptográficas.


