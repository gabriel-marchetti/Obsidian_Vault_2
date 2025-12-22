---
tags:
  - Arch
  - VPN
  - NordVPN
---
# References
1) https://wiki.archlinux.org/title/NordVPN

---
# Content:
Install the $\texttt{nordvpn}$ and $\texttt{nordvpn-gui}$ through AUR. 
Abrindo o $\texttt{nordvpn-gui}$ aparecerá para configurar o usuário nordvpn dentro da sua máquina:
```
sudo groupadd nordvpn
sudo usermod -aG nordvpn $USER
```
Dentro da ferramenta GUI ele indica como configurar tudo.

# Testando o VPN:
1) Teste de VPN.
2) Teste de DNSLeak (https://www.dnsleaktest.com/results.html) - Garantir que ISP é diferente do seu provedor de internet.
3) Teste de WebRTC (https://browserleaks.com/webrtc) - Checar seu Public IP.
4) Teste de KillSwitch - Olhar um vídeo e desativar a VPN.