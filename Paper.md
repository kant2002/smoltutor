# Paper.Rmd

#### 2024-03-02

<script>// Pandoc 2.9 adds attributes on both header and div. We remove the former (to
// be compatible with the behavior of Pandoc < 2.8).
document.addEventListener('DOMContentLoaded', function(e) {
  var hs = document.querySelectorAll("div.section[class*='level'] > :first-child");
  var i, h, a;
  for (i = 0; i < hs.length; i++) {
    h = hs[i];
    if (!/^h[1-6]$/i.test(h.tagName)) continue;  // it should be a header h1-h6
    a = h.attributes;
    while (a.length > 0) h.removeAttribute(a[0].name);
  }
});
</script>
<script
  src="https://code.jquery.com/jquery-3.7.1.min.js"
  integrity="sha256-/JqT3SQfawRcv/BIHPThkBvs0OEvtFFmqPF/lYI/Cxo="
  crossorigin="anonymous"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
<script src="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/html5shiv/3.7.3/html5shiv.min.js" integrity="sha512-UDJtJXfzfsiPPgnI5S1000FPLBHMhvzAMX15I+qG2E2OAzC9P1JzUwJOfnypXiOH7MRPaqzhPbBGDNNj7zBfoA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/respond.js/1.4.2/respond.min.js" integrity="sha512-qWVvreMuH9i0DrugcOtifxdtZVBBL0X75r9YweXsdCHtXUidlctw7NXg5KVP3ITPtqZ2S575A0wFkvgS2anqSA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
<style>h1 {font-size: 34px;}
h1.title {font-size: 38px;}
h2 {font-size: 30px;}
h3 {font-size: 24px;}
h4 {font-size: 18px;}
h5 {font-size: 16px;}
h6 {font-size: 12px;}
code {color: inherit; background-color: rgba(0, 0, 0, 0.04);}
pre:not([class]) { background-color: white }</style>
<script src="./sticky.tabs.js"></script>
<style type="text/css">.hljs-literal {
color: #990073;
}
.hljs-number {
color: #099;
}
.hljs-comment {
color: #998;
font-style: italic;
}
.hljs-keyword {
color: #900;
font-weight: bold;
}
.hljs-string {
color: #d14;
}
</style>
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/highlight.min.js" integrity="sha512-ExaEi+x+Zqq50MIBraxsK23lQQJZd8Q7ZDlwJsxQwsWlO8XvRouQev9ZWaFxCKdTvrgb2fmf2pglwGp61/7qZA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>

<style type="text/css">
code{white-space: pre-wrap;}
span.smallcaps{font-variant: small-caps;}
span.underline{text-decoration: underline;}
div.column{display: inline-block; vertical-align: top; width: 50%;}
div.hanging-indent{margin-left: 1.5em; text-indent: -1.5em;}
ul.task-list{list-style: none;}
</style>

<style type="text/css">code{white-space: pre;}</style>
<script type="text/javascript">
if (window.hljs) {
  hljs.configure({languages: []});
  hljs.initHighlightingOnLoad();
  if (document.readyState && document.readyState === "complete") {
    window.setTimeout(function() { hljs.initHighlighting(); }, 0);
  }
}
</script>

<style type="text/css">
.main-container {
max-width: 940px;
margin-left: auto;
margin-right: auto;
}
img {
max-width:100%;
}
.tabbed-pane {
padding-top: 12px;
}
.html-widget {
margin-bottom: 20px;
}
button.code-folding-btn:focus {
outline: none;
}
summary {
display: list-item;
}
details > summary > p:only-child {
display: inline;
}
pre code {
padding: 0;
}
</style>



<!-- tabsets -->

<style type="text/css">
.tabset-dropdown > .nav-tabs {
display: inline-table;
max-height: 500px;
min-height: 44px;
overflow-y: auto;
border: 1px solid #ddd;
border-radius: 4px;
}
.tabset-dropdown > .nav-tabs > li.active:before, .tabset-dropdown > .nav-tabs.nav-tabs-open:before {
content: "\e259";
font-family: 'Glyphicons Halflings';
display: inline-block;
padding: 10px;
border-right: 1px solid #ddd;
}
.tabset-dropdown > .nav-tabs.nav-tabs-open > li.active:before {
content: "\e258";
font-family: 'Glyphicons Halflings';
border: none;
}
.tabset-dropdown > .nav-tabs > li.active {
display: block;
}
.tabset-dropdown > .nav-tabs > li > a,
.tabset-dropdown > .nav-tabs > li > a:focus,
.tabset-dropdown > .nav-tabs > li > a:hover {
border: none;
display: inline-block;
border-radius: 4px;
background-color: transparent;
}
.tabset-dropdown > .nav-tabs.nav-tabs-open > li {
display: block;
float: none;
}
.tabset-dropdown > .nav-tabs > li {
display: none;
}
</style>

<!-- code folding -->

- [Про цей файл](#про-цей-файл)
  - [підключити бібліотеки](#підключити-бібліотеки)
  - [завантажити інформацію про завдання](#завантажити-інформацію-про-завдання)
  - [завантажити невірні відповіді помарковані із невірною інтерпретацією](#завантажити-невірні-відповіді-помарковані-із-невірною-інтерпретацією)
  - [завантажити датасет](#завантажити-датасет)
  - [визначити допоміжні функції](#визначити-допоміжні-функції)
- [Розділ 5.3: SMoL тести](#розділ-53-smol-тести)
  - [«Деякі запитання та відповіді учнів з Тестів» (Таблиця 2-4)](#«деякі-запитання-та-відповіді-учнів-з-тестів»-таблиця-2-4)
- [Розділ 6.1: Взаємодія з користувачем](#розділ-61-взаємодія-з-користувачем)
  - [«на практиці студенти витратили приблизно 9,8 (медіана) хвилин».](#«на-практиці-студенти-витратили-приблизно-98-медіана-хвилин»)
- [Розділ 6.2: Збір задач для репетитора](#розділ-62-збір-задач-для-репетитора)
  - [«Починаючи з 37 програм у тестах SMoL»](#«починаючи-з-37-програм-у-тестах-smol»)
  - [«ми додали ще 52 програми, щоб отримати загальну кількість 89».](#«ми-додали-ще-52-програми-щоб-отримати-загальну-кількість-89»)
  - [“У тестах SMoL часто є дуже мало неправильних виборів: …”](#у-тестах-smol-часто-є-дуже-мало-неправильних-виборів-)
  - [“зрештою ми значно збільшили кількість варіантів: …”](#зрештою-ми-значно-збільшили-кількість-варіантів-)
- [Розділ 7.2: Каталог хибних уявлень](#розділ-72-каталог-хибних-уявлень)
  - [“ми виявили розрив між 23% і 13%, і, отже, взяли 14% як порогове значення”](#ми-виявили-розрив-між-23-і-13-і-отже-взяли-14-як-порогове-значення)
  - [«хибні уявлення, виявлені викладачем SMoL» (Таблиці 6-8)](#«хибні-уявлення-виявлені-викладачем-smol»-таблиці-6-8)
- [Розділ 8: Чи репетитор ефективний?](#розділ-8-чи-репетитор-ефективний)
  - [«Скільки студентів обрали неправильну відповідь, яка (однозначно) представляє неправильне уявлення?» (Малюнок 4)](#«скільки-студентів-обрали-неправильну-відповідь-яка-однозначно-представляє-неправильне-уявлення»-малюнок-4)
  - [«Ми також зробили логістичну регресію, щоб побачити, чи є ці покращення значними»](#«ми-також-зробили-логістичну-регресію-щоб-побачити-чи-є-ці-покращення-значними»)
  - [«лише 40 із 71 прийнятних проблем (після видалення модулів, які не належать до SMoL) були корисними»](#«лише-40-із-71-прийнятних-проблем-після-видалення-модулів-які-не-належать-до-smol-були-корисними»)
- [Розділ 9: Ефективність щодо інших популяцій](#розділ-9-ефективність-щодо-інших-популяцій)
  - [«Репетитор використовувався в одному курсі …, який пройшли 12 студентів»](#«репетитор-використовувався-в-одному-курсі--який-пройшли-12-студентів»)
  - [«597 людей почали з першого модуля, а 103 користувача дійшли до останнього».](#«597-людей-почали-з-першого-модуля-а-103-користувача-дійшли-до-останнього»)
  - [«Ми зазначаємо, що дати подання на публічну інстанцію та семестр в Університеті 1 не збігаються»](#«ми-зазначаємо-що-дати-подання-на-публічну-інстанцію-та-семестр-в-університеті-1-не-збігаються»)
  - [«ми обчислили рангову кореляцію Спірмена ρ»](#«ми-обчислили-рангову-кореляцію-спірмена-ρ»)
    - [«Між початковим університетом і університетом 2»](#«між-початковим-університетом-і-університетом-2»)
    - [«Між початковим університетом і онлайн-популяцією»](#«між-початковим-університетом-і-онлайн-популяцією»)
- [Розділ 11: Загрози валідності](#розділ-11-загрози-валідності)
  - [«в середньому лише 0,4% (sd = 0,6%) значень відсутні»](#«в-середньому-лише-04-sd--06-значень-відсутні»)

# Про цей файл

Цей файл містить усі важливі статистичні дані в статті. Коли
це має сенс, він також представляє програму R, яка обчислює статистику.
Заголовки розділів, взяті в лапки, є цитатами з статті. Ці розділи наводять докази цитованих слів.

## підключити бібліотеки

```r
library(tidyverse)
```

## завантажити інформацію про завдання

```r
df_tasks = (
  read_csv("SMoL Tutor/Tasks.csv")
  # видалили кінцевий розрив рядка
  %>% mutate(Program = str_replace(Program, "[\\\\]n$", ""))
)
df_tasks
```

```
## # A tibble: 71 × 5
##    TaskID Tutorial Task                          Program                  Result
##     <dbl> <chr>    <chr>                         <chr>                    <chr> 
##  1      1 scope1   warmup_defvar                 "(defvar x 1)\\n(defvar… 1 3   
##  2      2 scope1   warmup_error                  "(defvar xyz 173)\\nabc" error 
##  3      3 scope1   warmup_fun                    "(deffun (sum x y z)\\n… 6     
##  4      4 scope1   local_def_is_possible         "(deffun (addy x)\\n  (… 3     
##  5      5 scope1   refer_global_is_possible      "(defvar y 1)\\n(deffun… 3     
##  6      6 scope1   defs_are_recursive            "(deffun (addy x)\\n  (… 3     
##  7      7 scope1   shadow_or_overwrite           "(defvar y 100)\\n(deff… 202   
##  8      8 scope1   shadow_rather_than_overwrite  "(defvar y 100)\\n(deff… 302   
##  9      9 scope1   error_when_refer_to_undefined "(deffun (addy x)\\n  (… error 
## 10     10 scope1   what_is_x_1                   "(defvar x 1)\\n(deffun… 2     
## # ℹ 61 more rows
```

## завантажити невірні відповіді помарковані із невірною інтерпретацією

```r
df_misinterpreters = (
  read_csv("./SMoL Tutor/Answers_Tagged_with_Misinterpreters.csv")
  %>% group_by(Tutorial, Task, ActualResult)
  %>% arrange(Misinterpreter)
  %>% summarise(
    MIs = str_c(Misinterpreter, collapse = ", "),
    N_MIs = n())
  %>% rename(Answer = ActualResult)
  %>% left_join(df_tasks)
  %>% ungroup()
  %>% select(TaskID, Answer, MIs, N_MIs)
)
df_misinterpreters
```

```
## # A tibble: 73 × 4
##    TaskID Answer                 MIs                    N_MIs
##     <dbl> <chr>                  <chr>                  <int>
##  1     61 error                  FunNotVal, IsolatedFun     2
##  2     60 error                  FunNotVal                  1
##  3     62 error                  FunNotVal                  1
##  4     57 #(#(1 7 3) #(100 7 3)) DefsCopyStructs            1
##  5     58 #(#(2 #(2 3)) #(2 3))  StructsCopyStructs         1
##  6     58 error                  NoCircularity              1
##  7     56 5 5                    DeepClosure, DefOrSet      2
##  8     56 5 error                IsolatedFun                1
##  9     56 6 7                    CallByRef, FlatEnv         2
## 10     55 0                      CallByRef, FlatEnv         2
## # ℹ 63 more rows
```

## завантажити датасет

```r
dns = c(
  "Univ1",
  "Univ2",
  "Book"
)
dfs = list()
for (dn in dns) {
  dfs[[dn]] = read_csv(str_c("./SMoL Tutor/Datasets/", dn, ".csv")) %>% left_join(df_tasks)
}
dfs$Univ1
```

```
## # A tibble: 6,649 × 9
##    Tutee      TaskID Answer IsCorrect Time                Tutorial Task  Program
##    <chr>       <dbl> <chr>  <lgl>     <dttm>              <chr>    <chr> <chr>  
##  1 00f2d764d…      1 1 3    TRUE      2022-09-08 16:19:11 scope1   warm… "(defv…
##  2 01158de8e…      1 1 3    TRUE      2022-09-16 16:19:02 scope1   warm… "(defv…
##  3 013989e34…      1 1 3    TRUE      2022-09-08 11:00:48 scope1   warm… "(defv…
##  4 0175df601…      1 error  FALSE     2022-09-09 17:01:15 scope1   warm… "(defv…
##  5 054eb7074…      1 1 3    TRUE      2022-09-18 14:02:58 scope1   warm… "(defv…
##  6 064f1beb4…      1 1 3    TRUE      2022-09-07 23:05:58 scope1   warm… "(defv…
##  7 07dd5f024…      1 1 3    TRUE      2022-09-14 15:32:13 scope1   warm… "(defv…
##  8 0a0a92b5a…      1 1 3    TRUE      2022-09-08 16:49:48 scope1   warm… "(defv…
##  9 1364cfe91…      1 1 3    TRUE      2022-09-08 19:56:44 scope1   warm… "(defv…
## 10 141bdce8b…      1 1 3    TRUE      2022-09-07 11:18:59 scope1   warm… "(defv…
## # ℹ 6,639 more rows
## # ℹ 1 more variable: Result <chr>
```

## визначити допоміжні функції

```r
# compute the confidence interval (CI) of correct rates (CR)
CR.CI.low = function(N, P) {
  a = round(N * P)
  b = N - a
  p = 0.05 / 2
  qbeta(p, a + 1/2, b + 1/2)
}
CR.CI.high = function(N, P) {
  a = round(N * P)
  b = N - a
  p = 1 - (0.05 / 2)
  qbeta(p, a + 1/2, b + 1/2)
}
# turn tutorial to factor
TUTORIALs = unique(df_tasks$Tutorial)
factor_tutorial = function(x) {
  factor(x, levels = TUTORIALs)
}
# compute how many students made each choice
get_summary = function(df) {
  (
    df
    # compute the Number of students supporting each answer
    %>% group_by(TaskID, Answer)
    %>% summarise(N = n(), IsCorrect = unique(IsCorrect))
    %>% ungroup()
  )
}
# compute the students/tutees who did all the give tasks
get_tutees_did_all = function(df, tasks) {
  tasks = unique(tasks)
  tutees = (
    df
    %>% filter(TaskID %in% tasks)
    %>% group_by(Tutee) %>% summarise(N = n())
    %>% filter(N == length(tasks))
    %>% pull("Tutee")
  )
}
# like get_summary, but summarize only the students who completed the
# given task
get_summary_filtered = function(df, tasks) {
  # like get summary but focus on students who did ALL
  # selected tasks.
  tasks = unique(tasks)
  tutees = get_tutees_did_all(df, tasks)
  get_summary(
    dfs$Univ1
    %>% filter(TaskID %in% tasks)
    %>% filter(Tutee %in% tutees)
  )
}
# how many students did each task correctly
get_cr = function(df) {
  (
    df
    %>% group_by(TaskID)
    %>% summarise(CorrectRate = mean(IsCorrect))
    %>% ungroup()
    %>% arrange(TaskID)
  )
}
```

# Розділ 5.3: SMoL тести

## «Деякі запитання та відповіді учнів з Тестів» (Таблиця 2-4)

Перевірте [./SMoL Quizzes/Quiz Results](./SMoL%20Quizzes/Quiz%20Results.md)

# Розділ 6.1: Взаємодія з користувачем

## «на практиці студенти витратили приблизно 9,8 (медіана) хвилин».

Наступне обчислення (529 с = 8,8 хв) занижує проміжок часу, оскільки ми представляємо лише результати інтерпретації питань.
Викладач завжди показує короткий текстовий опис перед першим питанням інтерпретації. І останні питання іноді не є питанням інтерпретації. Однак різниця невелика. Середній час необроблених даних становить 590,75 секунд, тобто 9,85 хвилин.

```r
(
  dfs$Univ1
  %>% group_by(Tutorial, Tutee)
  %>% summarise(TimeSpan = max(Time) - min(Time))
  %>% ungroup()
  %>% summarise(
    median(TimeSpan),
    mean(TimeSpan))
)
```

```
## # A tibble: 1 × 2
##   `median(TimeSpan)` `mean(TimeSpan)`
##   <drtn>             <drtn>          
## 1 529 secs           2469.479 secs
```

# Розділ 6.2: Збір задач для репетитора

## «Починаючи з 37 програм у тестах SMoL»

37:

- 13 питань у тесті 1
- 10 питань у тесті 2
- 14 питань у тесті 3

Перевірте [Instrument](./SMoL%20Quizzes/Instrument/) для підтверждення.

## «ми додали ще 52 програми, щоб отримати загальну кількість 89».

```r
df_tutor_choices = (
  read_csv("./SMoL Tutor/Choices.csv")
)
df_tutor_choices
```

```
## # A tibble: 493 × 4
##    Tutorial Task          Choice IsAdded
##    <chr>    <chr>         <chr>  <lgl>  
##  1 scope1   warmup_defvar 1 3    FALSE  
##  2 scope1   warmup_defvar 1 2    FALSE  
##  3 scope1   warmup_defvar error  FALSE  
##  4 scope1   warmup_defvar 2 1    TRUE   
##  5 scope1   warmup_defvar 2 3    TRUE   
##  6 scope1   warmup_defvar 3 2    TRUE   
##  7 scope1   warmup_defvar 3 1    TRUE   
##  8 scope1   warmup_error  error  FALSE  
##  9 scope1   warmup_error  173    TRUE   
## 10 scope1   warmup_fun    6      FALSE  
## # ℹ 483 more rows
```

```r
N_tutor_questions = n_distinct(
  df_tutor_choices
  %>% mutate(TaskFullName = str_c(Tutorial, "::", Task))
  %>% select(TaskFullName)
)
N_tutor_questions
```

```
## [1] 89
```

```r
N_tutor_questions - 37
```

```
## [1] 52
```

## “У тестах SMoL часто є дуже мало неправильних виборів: …”

У тесті 1,

- 8 питань мали 3 відповідей (включаючи `Інше`)
- 3 питань мали 4 відповідей
- 1 питань мали 5 відповідей
- 1 питань мали 6 відповідей

У тесті 2,

- 7 питань мали 3 відповідей
- 2 питань мали 4 відповідей
- 1 питань мали 5 відповідей

У тесті 3,

- 11 питань мали 3 відповідей
- 2 питань мали 4 відповідей
- 1 питань мали 5 відповідей

Взагалі, 
* 26 питань мали 3 відповідей 
* 7 питань мали 4 відповідей 
* 3 питань мали 5 відповідей 
* 1 питань мали 6 відповідей

Підрахуйте інструменти для перевірки.

## “зрештою ми значно збільшили кількість варіантів: …”

```r
(
  df_tutor_choices
  %>% group_by(Tutorial, Task)
  # add 1 for the `Other` option
  %>% summarise(N_choices = n_distinct(Choice) + 1)
  %>% group_by(N_choices)
  %>% arrange(N_choices)
  %>% summarise(N_tasks = n())
  %>% arrange(N_choices)
  %>% mutate(TOTAL_tasks = sum(N_tasks))
)
```

```
## # A tibble: 11 × 3
##    N_choices N_tasks TOTAL_tasks
##        <dbl>   <int>       <int>
##  1         3       3          89
##  2         4       5          89
##  3         5      28          89
##  4         6      17          89
##  5         7       5          89
##  6         8      20          89
##  7         9       2          89
##  8        10       5          89
##  9        11       2          89
## 10        12       1          89
## 11        14       1          89
```

# Розділ 7.2: Каталог хибних уявлень

## “ми виявили розрив між 23% і 13%, і, отже, взяли 14% як порогове значення”

```r
(
  get_summary(dfs$Univ1)
  %>% group_by(TaskID)
  %>% mutate(P = N / sum(N))
  %>% filter(! IsCorrect)
  %>% left_join(df_misinterpreters)
  %>% filter(is.na(MIs))
  %>% arrange(desc(P))
  %>% left_join(df_tasks)
  %>% select(TaskID, Tutorial, Task, Answer, P)
)
```

```
## # A tibble: 79 × 5
## # Groups:   TaskID [48]
##    TaskID Tutorial Task                     Answer                          P
##     <dbl> <chr>    <chr>                    <chr>                       <dbl>
##  1     68 lambda2  syntax_pitfall           15                         0.578 
##  2     51 vectors2 alias_mvec_in_mvec_trick error                      0.478 
##  3     58 lambda1  smol_quiz_circularity    #(#(2 3) #(2 3))           0.233 
##  4     43 vectors1 warmup_vecset_1          100 3                      0.132 
##  5     45 vectors1 mpairs_are_mvec          error                      0.132 
##  6     42 vectors1 warmup_vecref            10                         0.110 
##  7     49 vectors2 alias_var_in_mvec        error                      0.0870
##  8     53 vectors2 warmup_circularity       run out of memory or time. 0.0870
##  9     62 lambda1  fun_in_vectors           2                          0.0778
## 10     51 vectors2 alias_mvec_in_mvec_trick #(1 2 #(4))                0.0761
## # ℹ 69 more rows
```

Найчастіша неправильна відповідь (lambda2::syntax_pitfall) — Lisp-ічна. Наступні дві неправильні відповіді (vectors2::alias_mvec_in_mvec_trick) і (lambda1::smol_quiz_circularity) нам здається важко віднести до помилкового уявлення.

The top wrong answer (lambda2::syntax_pitfall) is Lispy. The next two
wrong answers (vectors2::alias_mvec_in_mvec_trick) and (lambda1::smol_quiz_circularity) seem difficult for us to attribute to a
misconception.

Між третім (0,23) і четвертим (0,13) P є розрив.

## «хибні уявлення, виявлені викладачем SMoL» (Таблиці 6-8)

Перевірте [./SMoL Tutor/Tutor Results.html](./SMoL%20Tutor/Tutor%20Results)

# Розділ 8: Чи репетитор ефективний?

## «Скільки студентів обрали неправильну відповідь, яка (однозначно) представляє неправильне уявлення?» (Малюнок 4)

```r
MIs = (
  read_csv("SMoL Tutor/Answers_Tagged_with_Misinterpreters.csv")
  %>% select(Misinterpreter)
  %>% arrange(Misinterpreter)
  %>% distinct()
  %>% pull()
)
MIs
```

```
##  [1] "CallByRef"          "CallsCopyStructs"   "DeepClosure"       
##  [4] "DefByRef"           "DefOrSet"           "DefsCopyStructs"   
##  [7] "FlatEnv"            "FunNotVal"          "IsolatedFun"       
## [10] "Lazy"               "NestedDef"          "NoCircularity"     
## [13] "StructByRef"        "StructsCopyStructs"
```
```r
full_d = tibble(Misconception = NULL, TaskID = NULL, P = NULL, P_low = NULL, P_high = NULL)
for (MI in MIs) {
  # pick up tasks where a representative wrong answer exists
  tasks = (
    df_misinterpreters
    %>% filter(MIs == MI)
    %>% pull(TaskID)
  )
  d = (
    get_summary_filtered(dfs$Univ1, tasks)
    %>% full_join(df_misinterpreters %>% filter(TaskID %in% tasks))
    # if no student chose a wrong answer, we fill in zeros.
    %>% replace_na(list(N = 0))
    %>% group_by(TaskID)
    %>% mutate(
      P = N / sum(N),
      P_low = CR.CI.low(sum(N), P),
      P_high = CR.CI.high(sum(N), P)
    )
    %>% filter(MIs == MI)
    %>% left_join(df_tasks)
    %>% select(TaskID, Tutorial, P, P_low, P_high)
  )
  full_d = rbind(full_d, d %>% mutate(Misconception = MI))
}

full_d = (
  full_d
  %>% group_by(Misconception)
  %>% mutate(MinTaskID = min(TaskID))
  %>% ungroup()
  %>% arrange(MinTaskID)
  %>% mutate(Misconception = factor(Misconception, levels = unique(Misconception)))
)

my_font_size = 12
theme_set(theme_gray(base_size = my_font_size))
p = (
  ggplot(
    full_d
    %>% mutate_at("TaskID", as.factor)
    %>% mutate_at("Tutorial", factor_tutorial))
  + geom_pointrange(
    aes(
      x = TaskID,
      y = P,
      ymin = P_low,
      ymax = P_high,
      color = Tutorial
    ),
    size = 0.2, # decrease size of dots.
  )
  + facet_wrap("Misconception", scales = "free_x", ncol = 4)
  + ylim(0, 1)
  + ylab("Proportion of Students")
  + theme(
    legend.title = element_text(size = my_font_size - 2),
    legend.text = element_text(size = my_font_size - 2),
    legend.direction = "horizontal",
    legend.position="bottom"
  )
)
print(p)
```

<img src="Misconceptions_Decay.png" width="672" />

```r
ggsave(
  "Misconceptions_Decay.png",
  width = 7, height = 8
  ) # depends on `svglite`
```

## «Ми також зробили логістичну регресію, щоб побачити, чи є ці покращення значними»

```r
# regression Models
ms = list()
for (MI in MIs) {
# MI = MIs[3]
  cat("\n=== ")
  cat(MI)
  cat(" ===\n")
  tasks = (
    df_misinterpreters
    %>% left_join(df_tasks, by = "TaskID")
    %>% filter(MIs == MI)
    # %>% filter(str_detect(MIs, MI))
    %>% select(TaskID)
    %>% distinct()
    %>% pull()
  )
  if (length(tasks) <= 1) {
    cat(str_c("Not enought question (", length(tasks), ")\n"))
  } else {
    tutees = get_tutees_did_all(dfs$Univ1, tasks)
    d = (
      dfs$Univ1
      %>% filter(TaskID %in% tasks)
      %>% filter(Tutee %in% tutees)
      %>% group_by(Tutee)
      %>% arrange(TaskID)
      %>% mutate(LocalTaskID = row_number())
      %>% left_join(df_misinterpreters, by = c("TaskID", "Answer"))
      %>% select(LocalTaskID, MIs)
      %>% replace_na(list(MIs = ""))
      %>% mutate(HasTheMisc = MIs == MI)
    )
    # print(d)
    m = glm(formula = HasTheMisc ~ LocalTaskID, data = d)
    ms[MI] = m
    print(summary(m))
  }
  cat("-------")
}
```

```
## 
## === CallByRef ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)   
## (Intercept)  0.16304    0.05737   2.842   0.0050 **
## LocalTaskID -0.06522    0.03628  -1.797   0.0739 . 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.06055901)
## 
##     Null deviance: 11.217  on 183  degrees of freedom
## Residual deviance: 11.022  on 182  degrees of freedom
## AIC: 10.197
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === CallsCopyStructs ===
## Not enought question (1)
## -------
## === DeepClosure ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.33889    0.04002   8.469 6.50e-16 ***
## LocalTaskID -0.08778    0.01461  -6.007 4.64e-09 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.09608007)
## 
##     Null deviance: 37.864  on 359  degrees of freedom
## Residual deviance: 34.397  on 358  degrees of freedom
## AIC: 182.3
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === DefByRef ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.23656    0.05323   4.444 1.52e-05 ***
## LocalTaskID -0.11828    0.03367  -3.513 0.000557 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.05271155)
## 
##     Null deviance: 10.3495  on 185  degrees of freedom
## Residual deviance:  9.6989  on 184  degrees of freedom
## AIC: -15.549
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === DefOrSet ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -0.15217    0.05954  -2.556   0.0114 *  
## LocalTaskID  0.15217    0.03765   4.041 7.83e-05 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.06521739)
## 
##     Null deviance: 12.935  on 183  degrees of freedom
## Residual deviance: 11.870  on 182  degrees of freedom
## AIC: 23.833
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === DefsCopyStructs ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.90370    0.06290   14.37   <2e-16 ***
## LocalTaskID -0.30000    0.02912  -10.30   <2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.1525981)
## 
##     Null deviance: 57.096  on 269  degrees of freedom
## Residual deviance: 40.896  on 268  degrees of freedom
## AIC: 262.63
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === FlatEnv ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.127029   0.021837   5.817  9.1e-09 ***
## LocalTaskID -0.011499   0.004324  -2.659  0.00801 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.06911857)
## 
##     Null deviance: 49.010  on 703  degrees of freedom
## Residual deviance: 48.521  on 702  degrees of freedom
## AIC: 120.82
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === FunNotVal ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -0.09551    0.04344  -2.199   0.0286 *  
## LocalTaskID  0.09551    0.01586   6.021 4.34e-09 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.1119628)
## 
##     Null deviance: 43.694  on 355  degrees of freedom
## Residual deviance: 39.635  on 354  degrees of freedom
## AIC: 234.79
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === IsolatedFun ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.132576   0.018836   7.038 4.22e-12 ***
## LocalTaskID -0.013636   0.003347  -4.074 5.09e-05 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.05915708)
## 
##     Null deviance: 47.716  on 791  degrees of freedom
## Residual deviance: 46.734  on 790  degrees of freedom
## AIC: 12.169
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === Lazy ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.35604    0.04150   8.579  < 2e-16 ***
## LocalTaskID -0.03265    0.01066  -3.064  0.00229 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.1808639)
## 
##     Null deviance: 100.09  on 545  degrees of freedom
## Residual deviance:  98.39  on 544  degrees of freedom
## AIC: 619.81
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === NestedDef ===
## Not enought question (1)
## -------
## === NoCircularity ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)   
## (Intercept)  0.21111    0.06870   3.073  0.00245 **
## LocalTaskID -0.07778    0.04345  -1.790  0.07515 . 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.0849563)
## 
##     Null deviance: 15.394  on 179  degrees of freedom
## Residual deviance: 15.122  on 178  degrees of freedom
## AIC: 70.995
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === StructByRef ===
## 
## Call:
## glm(formula = HasTheMisc ~ LocalTaskID, data = d)
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  0.47826    0.07070   6.765 1.77e-10 ***
## LocalTaskID -0.23913    0.04471  -5.348 2.65e-07 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for gaussian family taken to be 0.09197324)
## 
##     Null deviance: 19.370  on 183  degrees of freedom
## Residual deviance: 16.739  on 182  degrees of freedom
## AIC: 87.087
## 
## Number of Fisher Scoring iterations: 2
## 
## -------
## === StructsCopyStructs ===
## Not enought question (1)
## -------
```

## «лише 40 із 71 прийнятних проблем (після видалення модулів, які не належать до SMoL) були корисними»

```r
n_distinct(
  df_misinterpreters
  %>% filter(N_MIs == 1)
  %>% pull("TaskID")
)
```

```
## [1] 40
```

```r
n_distinct(
  df_tasks
  %>% pull("TaskID")
)
```

```
## [1] 71
```

# Розділ 9: Ефективність щодо інших популяцій

## «Репетитор використовувався в одному курсі …, який пройшли 12 студентів»

```r
n_distinct(
  dfs$Univ2
  %>% pull("Tutee")
)
```

```
## [1] 12
```

## «597 людей почали з першого модуля, а 103 користувача дійшли до останнього».

```r
(
  dfs$Book
  %>% group_by(Tutorial)
  %>% summarise(n_distinct(Tutee))
  %>% mutate_at("Tutorial", factor_tutorial)
  %>% arrange(Tutorial)
)
```

```
## # A tibble: 9 × 2
##   Tutorial  `n_distinct(Tutee)`
##   <fct>                   <int>
## 1 scope1                    597
## 2 scope2                    317
## 3 mut-vars1                 326
## 4 mut-vars2                 230
## 5 vectors1                  153
## 6 vectors2                  149
## 7 lambda1                   158
## 8 lambda2                   110
## 9 lambda3                   103
```

## «Ми зазначаємо, що дати подання на публічну інстанцію та семестр в Університеті 1 не збігаються»

```r
d = (
  rbind(
    dfs$Univ1 %>% mutate(Population = "Univ1"),
    dfs$Book %>% mutate(Population = "Book")
    )
)
(
  ggplot(d)
  + geom_histogram(aes(Time, fill = Population))
)
```

<img src="img2.png" width="672" />

## «ми обчислили рангову кореляцію Спірмена ρ»

```r
analyze_cor = function(dn1, dn2) {
  d = (
    get_cr(dfs[[dn1]])
    %>% inner_join(get_cr(dfs[[dn2]]), by = "TaskID")
    %>% left_join(df_tasks, by = "TaskID")
    %>% mutate(Tutorial = factor(Tutorial, levels = unique(df_tasks$Tutorial)))
    %>% remove_missing()
  )
  o = cor.test(d$CorrectRate.x, d$CorrectRate.y, method = "spearman")
  print(o)
  print(
    ggplot(d, aes(x = CorrectRate.x, y = CorrectRate.y))
    + geom_point()
    + xlim(0, 1) + ylim(0, 1)
    + xlab(dn1)
    + ylab(dn2)
    + scale_x_continuous(breaks = seq(0, 1, len = 3))
    + scale_y_continuous(breaks = seq(0, 1, len = 3))
    + facet_wrap("Tutorial", nrow = 1)
    + coord_fixed()
  )
}
```

### «Між початковим університетом і університетом 2»

```r
analyze_cor("Univ1", "Univ2")
```

```
## 
##  Spearman's rank correlation rho
## 
## data:  d$CorrectRate.x and d$CorrectRate.y
## S = 6097.7, p-value = 2.013e-07
## alternative hypothesis: true rho is not equal to 0
## sample estimates:
##       rho 
## 0.6690337
```

<img src="img3.png" width="672" />

### «Між початковим університетом і онлайн-популяцією»

```r
analyze_cor("Univ1", "Book")
```

```
## 
##  Spearman's rank correlation rho
## 
## data:  d$CorrectRate.x and d$CorrectRate.y
## S = 8582.6, p-value < 2.2e-16
## alternative hypothesis: true rho is not equal to 0
## sample estimates:
##       rho 
## 0.8560936
```

<img src="img4.png" width="672" />

# Розділ 11: Загрози валідності

## «в середньому лише 0,4% (sd = 0,6%) значень відсутні»

```r
(
  dfs$Univ1
  %>% group_by(Tutorial)
  %>% mutate(Total_Tutee = n_distinct(Tutee))
  %>% group_by(TaskID)
  %>% summarise(Missing = 1 - n_distinct(Tutee) / unique(Total_Tutee))
  %>% summarise(
    mean(Missing),
    sd(Missing))
)
```

```
## # A tibble: 1 × 2
##   `mean(Missing)` `sd(Missing)`
##             <dbl>         <dbl>
## 1         0.00436       0.00639
```

<script>

// add bootstrap table styles to pandoc tables
function bootstrapStylePandocTables() {
  $('tr.odd').parent('tbody').parent('table').addClass('table table-condensed');
}
$(document).ready(function () {
  bootstrapStylePandocTables();
});


</script>

<!-- tabsets -->

<script>
$(document).ready(function () {
  window.buildTabsets("TOC");
});

$(document).ready(function () {
  $('.tabset-dropdown > .nav-tabs > li').click(function () {
    $(this).parent().toggleClass('nav-tabs-open');
  });
});
</script>

<!-- code folding -->


<!-- dynamically load mathjax for compatibility with self-contained -->
<script>
  (function () {
    var script = document.createElement("script");
    script.type = "text/javascript";
    script.src  = "https://mathjax.rstudio.com/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML";
    document.getElementsByTagName("head")[0].appendChild(script);
  })();
</script>
