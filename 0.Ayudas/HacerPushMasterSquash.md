# Pase para columnas de pie de camión

## Como hacer el pase

### Utilizando git cherry pick

- git pull 
- git checkout master
- git pull
- git checkout -b master_prov_rts 
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
- Realizar los git add (es posible hacer el commit desde vscode)
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\pie-de-camion-replenishment\pie-de-camion-replenishment.component.html" 
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\pie-de-camion-replenishment\pie-de-camion-filter\pie-de-camion-filter.component.scss" 
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\pie-de-camion-replenishment\pie-de-camion-filter\vertex-providers.service.ts"
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\replenishment-assistant\replenishment-assistant.component.ts"
- git add "C:\Tandrify\tandrify\angular-app\src\app\@tandrify-app\categories\inventory\replenishment\pie-de-camion-replenishment\pie-de-camion-replenishment.component.ts"
- git commit -m "Squashed para cambios en resutido y pie de camión donde se afectan el auto ajuste en campos, los campos de resurtido se replican en pie de camión"
#### Cherry pick
- git checkout master
- git pull origin master
- git cherry-pick 0b5783a
- git push origin master
- #### Squashed con rebase
- git checkout {Rama actual para combinar el commit}
- git rebase -i HEAD~6 (DONDE 6 ES EL NUMEOR DE COMMITS A UNIR)
- Ajustar los comits que se ven en pantalla cambiando pick por s y dejando solo el ultimo com pick para que ese sea el comit que se quiera dejar 