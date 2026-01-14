# Relatório de Análise de Logs – Suspeita de Ataque de Força Bruta SSH

## 1. Visão Geral
Foi realizada a análise do arquivo `auth.log` para identificar tentativas de acesso indevido ao serviço SSH do servidor.  
Foram encontrados diversos eventos de falha de autenticação, indicando possível ataque de força bruta.

## 2. Endereços IP suspeitos
- 185.231.247.91  
- 45.91.201.33  
- 102.223.94.12  

Esses IPs repetem tentativas em poucos segundos, indicando automação (bots).

## 3. Usuários atacados
- admin (inválido)  
- root (alvo crítico)  
- teste (inválido)  
- oráculo (inválido)  

## 4. Login bem-sucedido
Foi identificado um acesso legítimo:  
`Senha aceita para Gabriel a partir de 179.209.135.42`  
Este evento não indica comportamento malicioso.

## 5. Tipo de ataque identificado
 **Ataque de Força Bruta via SSH**  
Características observadas:
- Muitas tentativas de senha em sequência  
- Vários usuários padrão  
- IPs internacionais  
- Tentativas falhando constantemente  

## 6. Ações recomendadas
- Bloquear os IPs maliciosos no firewall  
- Implementar Fail2Ban para bloquear tentativas repetidas  
- Desabilitar login via root pelo SSH  
- Alterar a porta padrão (22) para outra  
- Habilitar autenticação por chaves SSH  
- Monitorar regularmente o `auth.log`  

##  Conclusão
Os registros analisados indicam um ataque de força bruta direcionado principalmente ao usuário root.  
Nenhuma intrusão bem-sucedida foi identificada.  
A implementação das medidas recomendadas reduz drasticamente o risco.



