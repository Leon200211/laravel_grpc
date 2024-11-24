Для Windows и OpenServer настройка gRPC будет немного лучше. Давайте настроим всё пошагово:

Первоначальная установка необходимых инструментов для Windows:


скачать protoc (компилятор протокольных буферов) для Windows с официальной репозитории:
https://github.com/protocolbuffers/protobuf/releases
(Выберите файл protoc-xxx-win64.zip)

Распакуйте архив и путь к папке в переменную систему PATH.



Шаг 1: Установка расширения PHP для Protobuf
Скачайте .dll файл для PHP Protobuf:

Для начала скачайте соответствующую версию расширения protobuf для PHP с сайта PECL:
Перейдите на страницу PECL: protobuf.
Выберите подходящую версию для вашей установки PHP. Например, если у вас PHP 7.4, найдите версию для PHP 7.4, VC15, TS (Thread Safe) или NTS (Non-Thread Safe), в зависимости от того, какой тип PHP у вас используется.
Скачайте файл .dll (например, php_protobuf-3.18.0-7.4-ts-vc15-x64.dll).
Поместите .dll файл в папку расширений OpenServer:

Найдите папку с расширениями PHP, обычно это C:\OpenServer\modules\php\PHP_X.X.X\ext, где PHP_X.X.X — это версия PHP, которую вы используете.
Поместите скачанный файл .dll в эту папку.

Установите необходимые приложения через композитор:

composer require grpc/grpc
composer require google/protobuf


Создайте структуру для прототипа файлов:

mkdir proto
mkdir app/Grpc


Создайте пример прототипа файла (proto/service.proto):

protoc --proto_path=proto --php_out=app/Grpc proto/*.proto


Для удобства работы с gRPC в Laravel можно использовать пакет:

composer require vindx/laravel-grpc


После установки опубликуйте конфигурацию:

php artisan vendor:publish --provider="Vindx\LaravelGrpc\LaravelGrpcServiceProvider"



