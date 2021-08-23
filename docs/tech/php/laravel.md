# Laravel


## create project

`composer create-project laravel/laravel [PROJ_NAME]`

run project: `php -S localhost:8000 -t [DIR_NAME]`

Usually, dir name should be the `public` directory (for webroot).


## Migration

create migration checkpoint: `php artisan make:migration MIGRATION_NAME`

apply migration: `php artisan migrate`

dry-run (show all changes but not apply): `php artisan migrate --pretend`

## Dev env

Valet

uninstall: https://stackoverflow.com/questions/40276967/uninstall-laravel-valet

### Ref:

* [PHP Laravel Vue.js 视频教程 - CODECASTS](https://codecasts.com/)
* [Laravel 8 中文文档 | 学院君](https://xueyuanjun.com/books/laravel-docs-8)
* [集成开发环境Laradock: Documentation - Laradock](http://laradock.io/documentation/)