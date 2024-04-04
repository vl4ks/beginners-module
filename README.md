pwd выводит путь к текущей директории
cd имя_папки смена директории 
cd .. возврат к родительской директории,т.е. на уровень выше
cd / перейди в корневую директорию
cd ~ перейди в домашнюю директорию (/Users/Username)
ls выводить содержимое директорий
ls -a просматривать содержимое вместе со скрытыми файлами и папками 
touch %ИМЯ_ФАЙЛА% создать файл
mkdir создать директорию
-p флаг для создания структуры директорий 
mkdir -p dir1/dir-inside/dir-deeper-inside
# создали папку dir-deeper-inside в папке dir-inside, которая находится в папке dir1 
mkdir ~/my-git-projects создать папку my-git-projects внутри домашней директории
touch ../../file.txt создаст файл file.txt на две папки выше по иерархии
cp что_копируем куда_копируем 
cp что_копируем что_копируем что_копируем куда_копируем
cp index.html style.css script.js src/
# скопировали три файла (index.html, style.css и script.js) в папку src 

mv что_перемещаем куда_перемещаем  
cat чтение текстового файла
rm удалить файл
rmdir удалить папку
rm -r рекурсивно удаляет файлы и папки (ключ -r позволяет удалять папки вместе с их содержимым)
&& амперсанд для соединения нескольких комманд
git config --global user.name "Ksenia Denisova" задаем имя пользователя в git
git config --global user.email veli4koksenia@yandex.ru задаем адрес эл.почты в git
git init создали репозиторий (инициализировали репозиторий)
rm -rf .git разгитить папку (ключ -f избавит вас от вопроса «Вы точно хотите удалить этот файл?)
git status текущее состояние репозитория
git add --all подготовили к сохранению все файлы в репозитории
git add . добавить текущую папку целиком
git commit выполнить коммит
git commit -m 'Мой первый коммит!'  коммит с комментарием
git log просмотреть историю коммитов
ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub" генерация SSH-пары
ls -a ~/.ssh содержимое папки .ssh
ls -la ~/.ssh содержимое папки .ssh в виде списка файлов
clip < ~/.ssh/id_ed25519.pub после генерации нужно скопировать содержимое ключа в буфер обмена
clip < ~/.ssh/id_rsa.pub та же команда для RSA
публичный ключ зашифрует данные, а приватный — расшифрует (Расширение .pub указывает на то, что ключ публичный)
ssh -T git@github.com проверка правильности ключа
git remote add привязать удалённый репозиторий к локальному (сначала перейти в каталог локального репозитория) 
git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git  передаем два параметра origin(имя удаленного р-я) и URL 
git remote -v Убедиться, что репозитории связаны
если выводится ошибка, то попробовать команду git remote remove origin для того чтобы удалить связь и потом заново сделать по новой URL

В дальнейшем при работе с удалённым репозиторием флаг -u можно опустить и писать просто git push

git clone git@github.com:TheGreatOwner/the-great-project.git Копирование чужих репозиториев

javac -encoding UTF-8 <имя java-файла> скомпилировать исходный код в байт-код (-encoding UTF-8 кодировка)
java <имя class-файла без расширения> 
java -Dfile.encoding=UTF-8 HelloJdk (так команда выглядит для HelloJdk.class) запустить файл с байт-кодом

#работа с несколькими файлами 
eсли все файлы лежат в src , то после клонирования нужно перейти в папку src и использовать команду:
javac -d <имя папки> *.java  (-d <имя папки> соберёт все сгенерированные class-файлы в одну папку; *.java означает, что скомпилированы будут все файлы с расширением .java, которые находятся в текущей папке — src)
javac -d bin -encoding UTF-8 *.java так выглядит команда (для компилирования нескольких файлов) для нашего примера 

java -cp <имя папки, в которой лежат class-файлы> <имя стартового класса>  выполнить программу, (обязательное требование к такому классу — внутри него должен быть метод main()) 
java -cp bin Practicum пример команды с параметрами 

#собираем архив 
jar cfe <имя jar-файла> <имя стартового класса> <список файлов> создаем jar (но только после того как мы уже все исходные файлы перевели в байт-код с помощью компилятора javac)
jar cfe library.jar Practicum -C bin . пример команды для создания jar
# Точка в конце строки указывает на то, что в JAR должны попасть 
# все файлы из папки bin.

java -jar <имя jar-файла>  запустить программу
java -jar library.jar 

# команда cat показывает содержимое файла
$ cat HEAD

# в файле вот такая ссылка 
ref: refs/heads/master 
# взяли ссылку из файла HEAD
$ cat refs/heads/master 
# внутри хеш
e007f5035f113f9abca78fe2149c593959da5eb7
$ git log 
# сверяем с хешем последнего коммита
commit e007f5035f113f9abca78fe2149c593959da5eb7
Author: John Doe <johndoe@example.com>

Когда вы делаете коммит, Git обновляет refs/heads/master — записывает в него хеш последнего коммита
HEAD указывает на последний коммит. Если передать его в качестве параметра, Git поймёт вас.

#Статусы untracked/tracked, staged и modified

untracked (англ. «неотслеживаемый»)

staged (англ. «подготовленный») //После_выполнения_команды_git_add_файл_попадает_в_staging_area

tracked (англ. «отслеживаемый»)

modified (англ. «изменённый»)

modified + git add = staged

staged + git commit = tracked

tracked + изменения = modified

untracked + git add = staged 

staged + изменения = modified

#Оформление сообщений к коммитам

*в выводе команды git log --oneline умещается максимум 72 первых символа сообщения*

#Conventional Commits (англ. «соглашение о коммитах»)

 <type>: <сообщение>
 
feat (сокращение от англ. feature) — для новой функциональности;
fix (от англ. «исправить», «устранить») — для исправленных ошибок.

git commit -m "feat: добавить подсчёт суммы заказов за неделю"

*В корпоративном стиле в начале сообщения обычно указывают Jira-ID, а после — текст сообщения.*

$ git commit -m "LGS-239: Дополнить список пасхалок новыми числами"

*Если коммит «закрывает» или «решает» какую-то задачу, то в его сообщении  укажите - #<номер задачи>*

$ git commit -m "Исправить #334, добавить график температуры"

Для сообщений на *русском* языке часто рекомендуют использовать инфинитивы. 
Например: Добавить тесты для PipkaService, Исправить ошибку #123

Для сообщений на *английском* рекомендуется использовать повелительное наклонение (англ. imperative). 
Например: Use library mega_lib_300, Fix exit button


#Good luck!