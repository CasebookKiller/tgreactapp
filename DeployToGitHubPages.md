# Развёртывание Приложения React* на GitHub Pages

\* создание с использованием `create-react-app`

# Введение

В этом руководстве я покажу вам, как можно создать приложение React и развернуть его на страницах GitHub.

Для создания приложения React я буду использовать [`create-react-app`](https://create-react-app.dev/), который является инструментом, который люди могут использовать для создания приложения React с нуля. Для развертывания приложения React я буду использовать [`gh-pages`](https://github.com/tschaub/gh-pages), который представляет собой пакет npm, который пользователи могут использовать для развертывания на [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages), бесплатном веб-хостинге, предоставляемом GitHub.

Если вы будете следовать этому руководству, то в итоге получите новое приложение React, размещенное на страницах GitHub, которое затем сможете настроить.

## Переводы

Это учебное пособие было переведено с английского оригинала на следующие языки:
- [Традиционный китайский](https://github.com/gitname/react-gh-pages/issues/167#issuecomment-1925551338) (автор: [@creaper9487](https://github.com/creaper9487))

# Руководство

## Предварительные условия

1. Установлены [Node и npm](https://nodejs.org/en/download/). Вот версии, которые я буду использовать при создании этого руководства:

    ```shell
    $ node --version
    v16.13.2

    $ npm --version
    8.1.2
    ```
  > Установка npm добавляет в систему две команды — `npm` и `npx` — обе из которых я буду использовать при    создании этого руководства.

2. [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) установлен. Вот версия, которую я буду использовать при создании этого руководства:

    ```shell
    $ git --version
    git version 2.29.1.windows.1
    ```

3. Учетная запись на [GitHub](https://github.com/signup). :octocat:

## Процедура

### 1. Создайте **пустой** репозиторий на GitHub

1. Войдите в свою учетную запись на GitHub.
2. Перейдите к форме [Создать новый репозиторий](https://github.com/new).
3. Заполните форму следующим образом:
    - **Название репозитория:** Вы можете ввести любое имя, которое хотите\*.
      
        > \* Для [сайта проекта](https://pages.github.com/#project-site) вы можете ввести любое название, которое вы хотите. Для [сайта пользователя](https://pages.github.com/#user-site), GitHub [requires](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites) имя хранилища должно иметь следующий формат: `{имя пользователя}.github.io ` (например, `gitname.github.io`)
        
        > Введенное вами имя будет отображаться в нескольких местах: (а) в ссылках на репозиторий на GitHub, (б) в URL-адресе репозитория и (в) в URL-адресе развернутого приложения React.

        > В этом руководстве я буду развертывать приложение React в качестве сайта проекта.

        Я введу: `react-gh-pages`
        
   - **Конфиденциальность репозитория:** Выберите _Public_ (или _Private_\*).

        > \* Для пользователей [GitHub Free](https://docs.github.com/en/get-started/learning-about-github/githubs-products#github-free-for-user-accounts) единственным типом хранилища, который можно использовать со страницами GitHub, является _Public_. Для пользователей [GitHub Pro](https://docs.github.com/en/get-started/learning-about-github/githubs-products#github-pro) (и других платных пользователей) со страницами GitHub можно использовать как публичные, так и частные репозитории.

        Я выберу: _Public_

   - **Инициализировать репозиторий:** Оставьте все флажки пустыми.

        > Это приведет к тому, что GitHub создаст пустой репозиторий, вместо того, чтобы предварительно заполнять его файлами `README.md`, `.gitignore` и/или `ЛИЦЕНЗИЯ`.
4. Отправьте форму.

На данный момент ваша учетная запись на GitHub содержит пустой репозиторий с указанным вами именем и типом конфиденциальности.

### 2. Создайте приложение React

1. Создайте приложение React с именем "my-app".:

    > Если вы хотите использовать имя, отличное от `my-app` (например, `web-ui`), вы можете сделать это, заменив все упоминания `my-app` в этом руководстве на другое имя (например, `my-app` --> `web-ui`).  

    ```shell
    $ npx create-react-app my-app
    ```

    > Эта команда создаст приложение React, написанное на JavaScript. Чтобы создать приложение, написанное на [TypeScript](https://create-react-app.dev/docs/adding-typescript/#installation), вы можете выполнить эту команду вместо:
    > ```shell
    > $ npx create-react-app my-app --template typescript
    > ```

    Эта команда создаст новую папку с именем `my-app`, которая будет содержать исходный код приложения React.

    > В дополнение к тому, что эта папка содержит исходный код приложения React, она также является репозиторием Git. Эта характеристика папки будет использована на шаге 6.

    > #### Названия ветвей: `master` или `main`
    > 
    > В репозитории Git будет одна ветвь, которая будет называться либо (а) `master`, по умолчанию для новой установки Git; либо (б) значением переменной конфигурации Git `init.defaultBranch`, если на вашем компьютере запущен Git версии 2.28 или более поздней, и у вас есть в вашей конфигурации Git [установите эту переменную](https://github.blog/2020-07-27-highlights-from-git-2-28/#introducing-init-defaultbranch) (например, через `$ git config --global init.defaultBranch main`).
    >
    > Поскольку я не устанавливал эту переменную при установке Git, ветка в моем репозитории будет называться `master`. В случае, если ветвь в вашем репозитории имеет другое имя (которое вы можете проверить, запустив `$ git branch`), например `main`, вы можете **заменить** все упоминания `master` в оставшейся части этого руководства на другое имя (например, `master` → `main`).

3. Войдите во вновь созданную папку:
  
    ```shell
    $ cd my-app
    ```

На данный момент на вашем компьютере установлено приложение React, и вы находитесь в папке, содержащей его исходный код. Все остальные команды, показанные в этом руководстве, можно запустить из этой папки.

### 3. Установите npm-пакет `gh-pages`

1. Установите пакет [`gh-pages`](https://github.com/tschaub/gh-pages) npm и назначьте его [для разработки dependency](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file):
 
    ```shell
    $ npm install gh-pages --save-dev
    ```

На данный момент пакет npm `gh-pages` установлен на вашем компьютере, и зависимость приложения React от него задокументирована в файле `package.json` приложения React.

### 4. Добавьте свойство `домашняя страница` в файл `package.json`.

1. Откройте файл `package.json` в текстовом редакторе.
   
    ```shell
    $ vi package.json
    ```

    > В этом руководстве я буду использовать текстовый редактор [vi](https://www.vim.org/). Вы можете использовать любой текстовый редактор, который вам нравится, например [Visual Studio Code](https://code.visualstudio.com/).

2. Добавьте свойство `домашняя страница` в следующем формате\*: `https://{имя пользователя}.github.io/{название репозитория}`

    > \* Для [сайта проекта](https://pages.github.com/#project-site) это формат. Для [сайта пользователя](https://pages.github.com/#user-site) это формат: `https://{имя пользователя}.github.io `. Вы можете прочитать больше о свойстве `домашняя страница` в разделе ["Страницы GitHub"](https://create-react-app.dev/docs/deployment/#github-pages) документации `create-react-app`.

    ```diff
    {
      "name": "my-app",
      "version": "0.1.0",
    + "homepage": "https://gitname.github.io/react-gh-pages",
      "private": true,
    ```
На данный момент файл `package.json` приложения React содержит свойство с именем `homepage`.

### 5. Добавьте сценарии развертывания в файл `package.json`

1. Откройте файл `package.json` в текстовом редакторе (если он еще не открыт в нем).
   
    ```shell
    $ vi package.json
    ```

2. Добавьте свойства `predeploy` и `deploy` к объекту `scripts`.:

    ```diff
    "scripts": {
    +   "predeploy": "npm run build",
    +   "deploy": "gh-pages -d build",
        "start": "react-scripts start",
        "build": "react-scripts build",
    ```

На данный момент файл `package.json` приложения React содержит сценарии развертывания.

### 6. Добавьте "удаленный", который указывает на репозиторий GitHub

1. Добавьте "[удаленный](https://git-scm.com/docs/git-remote)" в локальный репозиторий Git.

    Вы можете сделать это, выполнив команду в следующем формате:
    
    ```shell
    $ git remote add origin https://github.com/{username}/{repo-name}.git
    ```
    
    Чтобы настроить эту команду для вашей ситуации, замените `{username}` на свое имя пользователя на GitHub и замените `{repo-name}`на имя репозитория GitHub, который вы создали на шаге 1.

    В моем случае, я побегу:

    ```shell
    $ git remote add origin https://github.com/gitname/react-gh-pages.git
    ```

    > Эта команда сообщает Git, куда я хочу, чтобы она отправляла данные всякий раз, когда я — или пакет npm `gh-pages`, действующий от моего имени, — отправляю команду `$ git push` из этого локального репозитория Git.

На данный момент в локальном репозитории есть "remote", URL-адрес которого указывает на репозиторий GitHub, созданный вами на шаге 1.

### 7. Переместите приложение React в репозиторий GitHub

1. Переместите приложение React в репозиторий GitHub.

    ```shell
    $ npm run deploy
    ```

    > Это приведет к запуску сценариев `pre deploy` и `deploy`, определенных в `package.json`.
    >
    > Далее скрипт `predeploy` создаст распространяемую версию приложения React и сохранит ее в папке с именем `build`. Затем скрипт `deploy` перенесет содержимое этой папки в новую фиксацию в ветке `gh-pages` репозитория GitHub, создав эту ветку, если она еще не существует.

    > By default, the new commit on the `gh-pages` branch will have a commit message of "Updates". You can [specify a custom commit message](https://github.com/gitname/react-gh-pages/issues/80#issuecomment-1042449820) via the `-m` option, like this:
    > ```shell
    > $ npm run deploy -- -m "Deploy React app to GitHub Pages"
    > ```

На данный момент в репозитории GitHub есть ветка с именем `gh-pages`, которая содержит файлы, составляющие распространяемую версию приложения React. Однако мы еще не настроили GitHub Pages для _обслуживания_ этих файлов.

### 8. Настройка страниц на GitHub

1. Перейдите на страницу настроек **GitHub Pages**e
   1. В вашем веб-браузере перейдите в репозиторий GitHub
   1. Над браузером кода перейдите на вкладку с надписью "Settings".
   1. На боковой панели, в разделе "Код и автоматизация", нажмите на "Страницы".
1. Настройте параметры "Build and deployment" следующим образом:
   1. **Source**: Deploy from a branch
   2. **Branch**: 
      - Branch: `gh-pages`
      - Folder: `/ (root)`
1. Нажмите на кнопку "Save".

**Вот и все!** Приложение React было развернуто на страницах GitHub! :rocket:

На данный момент приложение React доступно любому, кто посетит URL-адрес `homepage`, указанный вами на шаге 4. Например, приложение React, которое я развернул, доступно по адресу https://gitname.github.io/react-gh-pages.

### 9. (Optional) Store the React app's _source code_ on GitHub

In a previous step, the `gh-pages` npm package pushed the distributable version of the React app to a branch named `gh-pages` in the GitHub repository. However, the _source code_ of the React app is not yet stored on GitHub.

In this step, I'll show you how you can store the source code of the React app on GitHub.

1. Commit the changes you made while you were following this tutorial, to the `master` branch of the local Git repository; then, push that branch up to the `master` branch of the GitHub repository.

    ```shell
    $ git add .
    $ git commit -m "Configure React app for deployment to GitHub Pages"
    $ git push origin master
    ```

    > I recommend exploring the GitHub repository at this point. It will have two branches: `master` and `gh-pages`. The `master` branch will contain the React app's source code, while the `gh-pages` branch will contain the distributable version of the React app.

# References

1. [The official `create-react-app` deployment guide](https://create-react-app.dev/docs/deployment/#github-pages)
2. [GitHub blog: Build and deploy GitHub Pages from any branch](https://github.blog/changelog/2020-09-03-build-and-deploy-github-pages-from-any-branch/)
3. [Preserving the `CNAME` file when using a custom domain](https://github.com/gitname/react-gh-pages/issues/89#issuecomment-1207271670)

# Notes

- Special thanks to GitHub (the company) for providing us with the GitHub Pages hosting service for free.
- And now, time to turn the default React app generated by `create-react-app` into something unique!
- This repository consists of two branches: 
    - `master` - the _source code_ of the React app
    - `gh-pages` - the React app _built from_ that source code

 # Contributors

Thanks to these people for contributing to the maintenance of this tutorial.

<!--

Template:
---------

<a href="https://github.com/____" target="_blank" title="____">
  <img src="https://github.com/____.png?size=40" height="40" width="40" alt="____" />
</a>

Instructions:
-------------

1. Copy the template and paste it below.
2. Replace the four "____" strings with the contributor's GitHub username.

Note: I specified the avatars using HTML because, when I did so using Markdown,
      only the _custom_ avatars appeared at the size I specified via the URL
      (e.g. 40px squared, for `https://github.com/gitname.png?size=40`);
      the GitHub-generated avatars seemed to ignore the size parameter and,
      instead, appear at their full size (approximately 420px squared).
      By using HTML, I can force _both_ types to appear at 40px squared.

-->

<a href="https://github.com/gitname" target="_blank" title="gitname">
  <img src="https://github.com/gitname.png?size=40" height="40" width="40" alt="gitname" />
</a>
<a href="https://github.com/rhulse" target="_blank" title="rhulse">
  <img src="https://github.com/rhulse.png?size=40" height="40" width="40" alt="rhulse" />
</a>
<a href="https://github.com/AbhishekCode" target="_blank" title="AbhishekCode">
  <img src="https://github.com/AbhishekCode.png?size=40" height="40" width="40" alt="AbhishekCode" />
</a>
<a href="https://github.com/adnjoo" target="_blank" title="adnjoo">
  <img src="https://github.com/adnjoo.png?size=40" height="40" width="40" alt="adnjoo" />
</a>
<a href="https://github.com/thebeatlesphan" target="_blank" title="thebeatlesphan">
  <img src="https://github.com/thebeatlesphan.png?size=40" height="40" width="40" alt="thebeatlesphan" />
</a>
<a href="https://github.com/valerio-pescatori" target="_blank" title="valerio-pescatori">
  <img src="https://github.com/valerio-pescatori.png?size=40" height="40" width="40" alt="valerio-pescatori" />
</a>
<a href="https://github.com/jackweyhrich" target="_blank" title="jackweyhrich">
  <img src="https://github.com/jackweyhrich.png?size=40" height="40" width="40" alt="jackweyhrich" />
</a>

This list is maintained manually—for now—and includes (a) each person who submitted a pull request that was eventually merged into `master`, and (b) each person who contributed in a different way (e.g. providing constructive feedback) and who approved of me including them in this list.
