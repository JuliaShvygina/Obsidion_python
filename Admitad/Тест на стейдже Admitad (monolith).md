### Подготовка

* Забронирвоать стейдж в канале [# dev_stage_q](https://app.slack.com/client/T02UVE68M/G01G20CK76K)
* *ОПЦИОНАЛЬНО*.  **Деплой на стейдж** - при необходимости посмотреть как отрабатывает код из ветки. Идем в проект [admitad-world-stage](https://mimimi.ninja/admitad-team/admitad-world-stage/-/pipelines) и подготавливаем новый деплой через Run pipeline.
	DEPLOY_HOST = stage0X, где X - номер стейджа. Например, stage05.
	MONOLITH_VERSION = хеш коммита нужной ветки
	...
* Доступ ко стейджу через терминал.
	* открываем терминал
	* в терминале `ssh -i ~/.ssh/admitad_developer.key -p 30777 admitad@HOST`
		посмотреть PORT и HOST можно [тут](https://mimimi.ninja/admitad-team/admitad-world-stage/-/blob/master/devops/environment/stage/inventory.ini).
	* ввести пароль от bastilion
* проверить состояние стейджа и очиститьего от предыдущих изменений:
	* `git status`
	* удалить лишние папки через `rm ...` . `.env` не трогаем
	* `git reset HEAD --hard`
	* `git status`
* можно работать со стейджом.

### Работа со стейджом
#### Скрипты
Скрипты для проверки складывают в специальный раздел GitLab - [snippets](https://mimimi.ninja/admitad-team/admitad/-/snippets).
Скрипт запускается в shell:
`docker exec -it admitad-monolith-web ./manage.py shell`
Далее пишем сниппет без лишних пустых строк.


#### Тестирование и отладка функционала новой ветки.



### Работа со стейджовым интерфейсом
* Логинимся на стейдж https://store.stage0x.crutches.space/login
	spenkow2 / abibok - рекламодатель
	pen_web / abibok - веб-мастер
	p.bubnevich@admitad.com / abibok - доступ в hq

Далее меняем адрес в соответсвии с нуждами, например, https://store.stage05.crutches.space/ru/hq/