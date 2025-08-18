**Code_counter_views**

**Profile views counting**

![](https://komarev.com/ghpvc/?username=LaraEvdokimova&color=green&style=for-the-badge&label=PROFILE+VIEW+COUNTINGS&base=100500)

**Including:**

**Profile views count**

![](https://komarev.com/ghpvc/?username=LaraEvdokimova&label=PROFILE+VIEWS+COUNT)

**Profile views extra-amount**

![](https://komarev.com/ghpvc/?username=LaraEvdokimova&abbreviated=true)

**Profile views counter **

![](https://komarev.com/ghpvc/?username=LaraEvdokimova)

**green**

![](https://komarev.com/ghpvc/?username=LaraEvdokimova&color=green)

**color**

![](https://komarev.com/ghpvc/?username=LaraEvdokimova&color=dc143c)

**flat-square-style**

![](https://komarev.com/ghpvc/?username=LaraEvdokimova&style=flat-square)

**flat-color-base**

![](https://komarev.com/ghpvc/?username=LaraEvdokimova&base=0)

## REVIEW

[![Total Views](https://komarev.com/ghpvc/?username=LaraEvdokimova&style=for-the-badge&label=ВСЕГО+ПРОСМОТРОВ&color=00FF00&base=100500)](https://github.com/LaraEvdokimova)

[![Daily](https://img.shields.io/badge/СЕГОДНЯ-{TODAY}-8A2BE2?logo=github&style=flat-square)]()

**Fresh up-to-date**  
[![Date](https://img.shields.io/date/1755482101$(date +%s)?label=ОБНОВЛЕНО&color=009688&style=for-the-badge)](https://github.com/LaraEvdokimova)

**Views**  

[![Counter](https://img.shields.io/badge/Total_Views-100,836-brightgreen)](https://github.com/yourprofile)  

**Updates**  

![Date](https://img.shields.io/date/1755482101$(date -u +%s)?label=Обновлено&color=blue&style=flat-square)

![Custom](https://img.shields.io/badge/Счетчик-344-ff69b4?style=for-the-badge&logo=github&logoColor=white)

## Timestamp
[![Update](https://img.shields.io/date/{timestamp}?cache=buster&label=%D0%9E%D0%91%D0%9D%D0%9E%D0%92%D0%9B%D0%95%D0%9D%D0%9E&color=009688&style=for-the-badge&logo=github)](https://github.com/LaraEvdokimova)
echo "TZ=America/New_York" >> $GITHUB_ENV
NEW_DATE="$(TZ=America/New_York date '+%d.%m.%Y %H:%M EST')"

name: Emergency Fix
on: [workflow_dispatch]

permissions:
  contents: write
  pages: write
  id-token: write

jobs:
  debug:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Debug environment
        run: |
          echo "UTC Time: $(date -u '+%Y-%m-%d %H:%M:%S')"
          echo "Server Timezone: $(TZ=$TZ date '+%Z')"  # Покажет актуальную зону (например, EST)
          echo "README exists: $(ls -la README.md)"
          echo "Current content:"
          cat README.md | grep -E 'Последнее|date'

      - name: Force update
        run: |
          NEW_DATE="$(TZ=$TZ date '+%d.%m.%Y %H:%M %Z')"  # Автоматически подставляет аббревиатуру зоны
          TIMESTAMP=$(date +%s)          
     
          sed -i "s|/date/[0-9]*|/date/$TIMESTAMP?cache=buster|g" README.md

          echo "Modified content:"
          grep -E 'Последнее|date' README.md

      - uses: stefanzweifel/git-auto-commit-action@v5
        with:
          commit_message: "EMERGENCY FIX: $(date +'%s')"
          branch: main
