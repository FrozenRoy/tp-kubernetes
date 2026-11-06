# Questions - Partie 1

## 1. Vérification des événements et des pods

**Question :** Quelles sont les deux commandes utilisées pour vérifier les
événements du namespace et le démarrage des pods et de leurs conteneurs ?

Les deux commandes sont :

```powershell
kubectl get events -n front
kubectl get pods -n front
```

La première commande affiche les événements du namespace `front`. La seconde
affiche l'état des pods dans ce namespace.

## 2. Pointillés violets

**Question :** À quoi correspondent les pointillés violets ?

Les pointillés violets correspondent à un **Worker Node** (nœud de travail).

## 3. Pointillés

**Question :** À quoi correspondent les pointillés ?

Les pointillés correspondent à un **cluster Kubernetes**.