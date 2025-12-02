**RELATÓRIO DE ANÁLISE DE LOGS – SUSPEITA DE ATAQUE DE FORÇA BRUTA SSH**

**1. Visão Geral**



Foi realizada a análise do arquivo auth.log para identificar tentativas de acesso indevido ao serviço SSH do servidor.

Foram encontrados diversos eventos de falha de autenticação, indicando possível ataque de força bruta.



**2. Endereços IP suspeitos**



**Durante a análise, os seguintes IPs realizaram múltiplas tentativas de login:**



185.231.247.91



45.91.201.33



102.223.94.12



Esses IPs repetem tentativas em poucos segundos, indicando automação (bots).



**3. Usuários atacados**



**As tentativas de login foram direcionadas aos seguintes usuários:**



admin (inválido)



root (alvo crítico)



test (inválido)



oracle (inválido)



Usuários comuns em ataques automatizados.



**4. Login bem-sucedido**



**Foi identificado um acesso legítimo:**



Accepted password for gabriel from 179.209.135.42





Este evento não indica comportamento malicioso.



**5. Tipo de ataque identificado**



**O padrão dos eventos corresponde a:**



➡ Ataque de Força Bruta via SSH



Características observadas:



Muitas tentativas de senha em sequência



Vários usuários padrão



IPs internacionais



Tentativas falhando constantemente



**6. Ações recomendadas**



**Para mitigar esse tipo de ataque, recomenda-se:**



Bloquear os IPs maliciosos no firewall



Implementar Fail2Ban para bloquear tentativas repetidas



Desabilitar login via root pelo SSH



Alterar a porta padrão 22 para outra



Habilitar autenticação por chaves SSH em vez de senha



Monitorar regularmente o auth.log



**Conclusão**



Os registros analisados indicam um ataque de força bruta direcionado principalmente ao usuário root.

Nenhuma intrusão bem-sucedida foi identificada.

A implementação das medidas recomendadas reduz drasticamente o risco.

