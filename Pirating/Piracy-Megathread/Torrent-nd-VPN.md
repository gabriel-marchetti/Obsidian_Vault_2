---
tags:
  - Torrent
  - VPN
---
# References:
1) https://rentry.org/torrentvpn
---
# Background Information
## Torrenting Risks:
- Peer-to-peer file sharing
- Your IP becomes visible for everyone in the torrent
- Some countries send DMCA to the ISP services responsible for the addresses
## VPN:
- **Bind** your VPN to your torrent client
- **Kill Switches** can have a delay and can expose your IP
### Choosing a VPN Provider:
- Consider: Price, Speed, Security (no-logs policy, based on a country friendly to piracy), features (port-forwarding, split tunneling).
- The recommendation is **Proton Premium**
- [FMHY VPN Guide](https://fmhy.net/privacy#vpn)
### Test Your VPN Binding:
- http://ipleak.net/
- Test downloading https://fosstorrents.com/distributions/arcolinux/ and disconnect from your VPN. See if results are as expected (i.e. Download should stop and only continue when you reestablish connection)
### Exclude Problematic File Extensions 
- Tools > Options > Downloads > Excluded FIle Names
```
*.lnk  
*.scr  
*.arj
```
# Torrent Sites
- Ensure Torrent Client and VPN are correct configured
- Use Firefox + UBlock Origin
- Use trusted sources

--- 
# To-Do
- Avaliar a configuração de Port-Forwarding
- Avaliar a configuração de Split-Tunneling