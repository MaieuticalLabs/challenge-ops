# Assessment Ansible


## Dipendenze

- docker
 
``` sh
pip install -r requirements.txt
```

## Prova

La directory `./static_site` contiene lo scheletro di un ruolo Ansible.

L'obiettivo della prova è quello di compilare il ruolo per servire un sito statico con nginx su una distribuzione Ubuntu Focal.

Per fare ciò sarà necessario:
- installare nginx
- attivarne le unit systemd
- scrivere un config file di nginx aggiungendo tramite la direttiva `add_header` gli header http definiti nella variabile `nginx_http_headers` (il cui default è definito in `./static_site/defaults/main.yml`)
- gestire il reload del webserver al cambio della configurazione
- scrivere un file di index (il contenuto non è importante, basta una stringa)


## Verifica

Il corretto funzionamento del ruolo può essere verificato con [molecule](https://molecule.readthedocs.io/en/latest/) su un container docker tramite il comando:

``` sh
cd ./static_site && molecule test
```

In fase di sviluppo la configurazione di nginx puó essere testata modificando quella presente in `./helpers`:

``` sh
docker run --rm --name docker-nginx -p 8000:80 -v $(pwd)/helpers/html:/usr/share/nginx/html -v $(pwd)/helpers/default.conf:/etc/nginx/conf.d/default.conf nginx
```
