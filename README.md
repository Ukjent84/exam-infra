##Infra for REST API

### Fremgangsmåte 
Fikk problemer med å gjenopplastet app etter første gang. Fant ut at jeg måtte pulle og slette terraform.tfstate hver gang jeg skulle gjen-kjøre infra.   kom frem til denne siden her https://stackoverflow.com/questions/33157516/best-practices-when-using-terraform hvor det blir anbefalt åå legge til denne filen i git.Ignore og det løste seg. 
