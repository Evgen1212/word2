# hello-word

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### P.S.
1. использовал sortablejs(https://sortablejs.github.io/Vue.Draggable/#/simple) для реализации изменения порядка слов перетаскиванием 
2. для  GET запроса использовал axios: https://github.com/axios/axios
3. api взял тут https://dictionaryapi.com/api/v3/references/thesaurus/json/sat?key=a1c59a22-cd0f-4c34-bd07-9cd3bc9b076c
4. во Vue шаблонах много кода, который целесообразно вынести в отдельные свойства, это я понимаю (так же не заморачивался с названиями классов и переменных, по хорошему нужен рефакторинг)
5. при поиске слова, будут выводится слова подсказки, которые уже заложенны в ответ api, рекомендующие/подсказывающие варианты введеного слова. Оставил эту возможность, как вариант реализовать всплывающий список внизу input-а.
6. Само задание: https://github.com/Evgen1212/word2/blob/master/%D0%A2%D0%B5%D1%81%D1%82%D0%BE%D0%B2%D0%BE%D0%B5%20%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20Vue.pdf


