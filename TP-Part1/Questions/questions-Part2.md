❓ Les différentes ressources sont déployées dans le bon namespace ? Quelle commande utilisez-vous pour vérifier cela ?

Oui. Chaque ressource doit être vérifiée dans son namespace (`database`, `middle` ou
`front`). La commande suivante affiche toutes les ressources d'un namespace :

```powershell
kubectl get all -n <namespace>
```

On peut aussi vérifier le namespace déclaré d'une ressource avec :

```powershell
kubectl get <type> <nom> -n <namespace> -o jsonpath="{.metadata.namespace}"
```

❓ Les ressources MySQL ConfigMap et MySQL sont à déployer au sein des namespaces middle et database, pourquoi ?

Les ressources Kubernetes comme les ConfigMaps, les Secrets, les Pods et les
Services sont limitées à leur namespace. MySQL et ses ConfigMap/Secrets sont donc
déployés dans `database`. WordPress est déployé dans `middle` et doit disposer de
copies de la ConfigMap et du Secret dans ce namespace, car il ne peut pas
référencer directement les ressources de `database`. En revanche, WordPress peut
joindre MySQL entre namespaces avec le DNS
`mysql.database.svc.cluster.local`.

❓ Les différentes pods sont-ils correctement démarrés ? Quelle commande utilisez-vous pour vérifier cela ?

On vérifie que la colonne `READY` correspond au nombre de conteneurs attendus et
que la colonne `STATUS` vaut `Running` :

```powershell
kubectl get pods -n database
kubectl get pods -n middle
kubectl get pods -n front
```

Pour obtenir davantage de détails :

```powershell
kubectl describe pod <nom-du-pod> -n <namespace>
```

❓ Lorsqu'un pod est en erreur comment accédez-vous aux events du namespace et aux logs du pod ? Quelles commandes utilisez-vous pour vérifier cela ?

Pour afficher les événements récents du namespace, notamment les erreurs de
planification, de montage ou de démarrage :

```powershell
kubectl get events -n <namespace> --sort-by=.lastTimestamp
```

Pour afficher les logs du pod :

```powershell
kubectl logs -n <namespace> <nom-du-pod>
```

Si le pod contient plusieurs conteneurs, préciser le conteneur :

```powershell
kubectl logs -n <namespace> <nom-du-pod> -c <nom-du-conteneur>
```