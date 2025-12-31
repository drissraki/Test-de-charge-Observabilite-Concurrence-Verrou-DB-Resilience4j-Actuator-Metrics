### Test de charge & Observabilité : Concurrence + Verrou DB + Resilience4j + Actuator Metrics

## Conclusion
Le verrouillage en base de données (généralement pessimiste via SELECT … FOR UPDATE) est essentiel dans un contexte multi-instances afin de garantir la sérialisation des accès à une ressource partagée, comme le stock. Sans ce mécanisme, deux transactions concurrentes pourraient lire la même valeur initiale (par exemple 1) et la décrmenter simultanément, provoquant une incohérence (stock négatif ou double emprunt).

Le Circuit Breaker joue un rôle de protection du système en interrompant rapidement les appels vers un service défaillant (ici le pricing-service), évitant ainsi la saturation des threads et la propagation des erreurs. Le Fallback, quant à lui, permet d’assurer une continuité de service en retournant une valeur par défaut (prix = 0.0) lorsque le service distant est indisponible, garantissant ainsi une expérience utilisateur dégradée mais toujours opérationnelle.