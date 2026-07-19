# sessao-03-README.md
Hardening de Redes Linux e Configuração de Firewalls
## Metodologia
1. Verificação do estado inicial do UFW (`ufw status`)
2. Definição de políticas padrão restritivas (bloquear entrada, permitir saída)
3. Criação de exceção para acesso SSH (porta 22/tcp)
4. Bloqueio de um IP malicioso fictício via iptables (chain INPUT)
5. Persistência das regras do iptables em `/etc/iptables/rules.v4`
   
 ## Resultados
### UFW — sudo ufw status verbose
<img width="385" height="48" alt="image" src="https://github.com/user-attachments/assets/fbf2f725-1473-4931-9f0c-654565489510" />

### iptables — sudo iptables -L -v
<img width="1163" height="896" alt="Captura de ecrã 2026-07-19 183644" src="https://github.com/user-attachments/assets/9e0835d3-622d-4511-8778-750ea1a32b46" />
#### Explicação 
Por padrão, toda a ligação de entrada (incoming) é bloqueada, seguindo o princípio de segurança de "negar por padrão, permitir por exceção" — reduz 
a superfície de ataque ao mínimo necessário. A única exceção aberta é a porta 22/tcp (SSH), necessária para administração remota do servidor.
Todo o tráfego de saída (outgoing) permanece permitido, para que o servidor consiga continuar a funcionar normalmente (atualizações, DNS, etc.).
Adicionalmente, foi bloqueado especificamente o IP fictício 203.0.113.50 na chain INPUT do iptables, simulando a resposta a um IP identificado 
como malicioso. 
#### Conclusões
Esta política reduz drasticamente a superfície de ataque, mas é essencial garantir que a porta SSH está sempre acessível antes de ativar o firewall, para evitar perder acesso remoto ao servidor.
