



Documentazione:
https://ygoprodeck.com/api-guide/

1. Creo un file store.js dentro la cartella src
    - importo il metodo reactive che mi permette di creare un oggetto 
    - importo store.js in main.vue e nei componenti

2. tramite una chiamata ajax, richiedo i dati da https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0

3. creo un componente card.vue

4. importo il componente card.vue in App.vue

5. stampo tutte le card presenti nel json in pagina dando un parametro offset in modo da non sovraccaricare la ricerca
https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0