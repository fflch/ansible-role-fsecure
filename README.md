### Se for uma migração de outra versão (ARRUMAR):

  1. Faz o backup pela interface na máquina antiga:

    /var/opt/f-secure/fspms/data/backup/2024_08_25_23_01_04.backup.zip

  2. Parar o serviço

    systemctl stop fspms
    
  3. O arquivo 2024_08_25_23_01_04.backup.zip depois de descompactado, gera um arquivo com o nome fspms.h2.db. Subistituir esse arquivo em /var/opt/f-secure/fspms/data/h2db/fspms.h2.db:

    rm /var/opt/f-secure/fspms/data/h2db/fspms.h2.db
    cp fspms.h2.db /var/opt/f-secure/fspms/data/h2db/fspms.h2.db
    chown fspms: fspms.h2.db
    chmod 660 fspms.h2.db

  4. Subir o serviço

    systemctl start fspms

  5. Exportar as chaves no servidor antigo e importar no novo:

    No Antigos: Tools -> Server Configuration -> Keys-> Export
    No Novo: Tools -> Server Configuration -> Keys-> Replace
       
### Extra

Redirecionamentos das portas na internuvem:

  - 47124 (pública) -> 8081 (f-secure)
  - 47123 (pública) -> 8080 (f-secure)
  - 47122 (pública) -> 443 (f-secure)
  - 47121 (pública) -> 80 (f-secure)

### Acessando com o console da sua máquina

1. Instalar o pacote disponível em https://www.withsecure.com/en/support/product-support/business-suite/policy-manager#download, WithSecure Policy Manager Console 16.02 (Linux) DEB files:

    sudo apt install ./wspmc_16.02.98349_amd64.deb

2. Acessar o serviço:

    sudo /opt/f-secure/fspmc/fspmc

3. Usuário padrão é admin e a senha está definida no playbook


