# homelab

Meu laboratório de estudos de infraestrutura, servidores e virtualização.

## Objetivo
Ficar pronto para vagas de suporte e, depois, seguir para infraestrutura com foco em virtualização.

## Ambiente
- PC: AMD Ryzen 5 5600GT, 16 GB de RAM
- Hipervisor: VirtualBox  7.2.22
- Sistema da VM: Ubuntu Server, 26.04.1 LTS
- Recursos da VM: 2 CPUs, 4 GB de RAM, 25 GB de disco (o `/` tem 11,5 GB)

## Diário
- 20-11-2026: VM criada, atualizada e com snapshot `instalaçao-limpa`.
- 20-11-2026: Caminho para o diário de erros: https://github.com/yoseph-carcabini/homelab/blob/main/Diario-de-erros.md

## Como recriar
- ISO: ubuntu-26.04.1-live-server-amd64.iso
- Idioma: Português (Portugal), pt_PT
- Teclado: layout br, modelo pc105
- Tipo de instalação: Ubuntu server normal 
- Rede: NAT
- Proxy: Nenhum 
- Servidor de downloads (mirror): Não lembro 
- Armazenamento: Disco inteiro com LVM. O volume raiz (`/`) ficou com 11,5 GB dos 23 GB do LVM
- Perfil: nome: yoseph | nome do servidor: yoseph | nome de usuário: yoseph
- OpenSSH instalado 
- Programas extras sugeridos (os "snaps") : Nenhum extra
- VM: Lab-linux1, RAM 4GB, 2 CPUs, disco VDI de 25 GB com alocação dinâmica, adaptador NAT
- Após instalar: `sudo apt update`, `sudo apt upgrade -y` e, se o sistema pedir, `sudo reboot`
- Snapshot: depois de atualizar (e reiniciar, se foi preciso), desligar com `sudo poweroff` e tirar o snapshot com a VM desligada. Nome: `instalaçao-limpa`
