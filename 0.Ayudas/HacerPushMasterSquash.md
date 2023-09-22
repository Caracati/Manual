# Pase para columnas de pie de camión

## Como hacer el pase

### Utilizando git cherry pick

- git pull 
- git checkout master
- git pull
- git checkout -b master_prov_rts (esta la creo igual y al final la borramos o se queda para futuros pasos )
- git cherry-pick a5b6338 27dd0ef ff901ea c0cc4db 5874927 34ed170
- git checkout master
- git merge master_prov_rts
- git push origin master

### Utilizando Squashed - Mas limpio

#### Squashed
- git checkout master
- git pull
- git checkout -b temp_replenishment-fields
- git cherry-pick a5b6338 27dd0ef ff901ea c0cc4db 5874927 34ed170
- git reset HEAD~6
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\pie-de-camion-replenishment\pie-de-camion-replenishment.component.html" 
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\pie-de-camion-replenishment\pie-de-camion-filter\pie-de-camion-filter.component.scss" 
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\pie-de-camion-replenishment\pie-de-camion-filter\vertex-providers.service.ts"
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\replenishment-assistant\replenishment-assistant.component.ts"
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\pie-de-camion-replenishment\pie-de-camion-replenishment.component.ts"
- git commit -m "Squashed para cambios en resutido y pie de camión donde se afectan el auto ajuste en campos, los campos de resurtido se replican en pie de camión"
#### Cherry pick
- git checkout master
- git pull origin master
- git cherry-pick ba462ef
- git push origin master