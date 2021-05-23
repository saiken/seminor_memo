# JJUG CCC 2021 Spring
## 全体
* 2021/05/23 (日) 10:00 - 18:00
* オンライン開催(TRAIL WORKSを使ったYoutube での配信)
* 参加者：905人
* セミナー一覧
あまりどれに寄ったというのはない感じ
![image](https://user-images.githubusercontent.com/827936/119246763-22af6600-bbbf-11eb-890a-da4949ea0697.png)

*** 

## 次のLTS Java 17にむけてJava 16までをおさらいしよう
### 登壇者
* LINE(LINE FUKUOKA)
* きしだ なおき
* スポンサーセッション

### リリース方針の変更
* 6ヶ月毎のリリース
    * 3月と9月にできているものをリリース
* 6バージョン毎にLTS
    * 11 → 17(2021/9)
* OracleがJDKを有償化したことで様々なベンダーがJDKを開発

### 各種アップデート
* Records：構造体的なもの
![image](https://user-images.githubusercontent.com/827936/119247630-2e525b00-bbc6-11eb-9dee-ab44fd045e4b.png)

* String
    * Text Blocks:ダブルクォート3つで書ける(kotlinにあるやつ)
    * +での文字連結がInvoke Dynamicに( =実行環境のJVMで最適化)
    初期はStringBuffer(synchronizedするやつ) → StringBuilder → Invoke Dynamicへ。
    * formattedが利用可能(いまではString.format)
    ![image](https://user-images.githubusercontent.com/827936/119247592-d0257800-bbc5-11eb-84de-d2bfaca36659.png)
    
* NPEのメッセージ改善
![image](https://user-images.githubusercontent.com/827936/119247550-64dba600-bbc5-11eb-9e71-801272b84ed7.png)

* 単一ソースのJavaソースはjavaコマンドで実行可
![image](https://user-images.githubusercontent.com/827936/119247507-09111d00-bbc5-11eb-8d1f-6832260a35c7.png)

* GC：java11 → G1GC。java17 → ZGC。

### まとめ
* Java 17は便利

### Q&A
* 特におすすめの機能は？
    * Records → 戻り値用にclass作るのいやだったのが、かなり心理的障壁が下がった

*** 

## ソフトウェアアーキテクチャの選び方
### 登壇者
* 成瀬 允宣(GMO)

### なぜアーキテクチャが必要か
* もっとも重要なファクターはソフトウェアの寿命
* 1ヶ月以上続くサービスであれば内部品質にコストをかけたほうがいい(内部品質 = ソフトウェアアーキテクチャ)
    * マーチンファウラーの擬似グラフでは1ヶ月が損益分岐点とのこと
    ![image](https://user-images.githubusercontent.com/827936/119247919-89854d00-bbc8-11eb-88a6-06135ac0a256.png)

### アーキテクチャの種類
* レイヤードアーキテクチャ
![image](https://user-images.githubusercontent.com/827936/119248080-ac643100-bbc9-11eb-8919-f04a50708342.png)
    * インフラストラクチャの変更が上位レイヤに影響してしまう(本来はアプリケーション・ドメイン層が中心なのに)
    * どこからでもデータを触れてしまい、実装がばらばらになる

* ヘキサゴナルアーキテクチャ
![image](https://user-images.githubusercontent.com/827936/119248109-ef260900-bbc9-11eb-88a3-c95f83646a99.png)
    * Port and Adaptor の考え方（要はI/Fベースにして差し替え可能にする)
    * IoC コンテナ(=DIコンテナ)を使って依存を減らすべし

* オニオンアーキテクチャ
![image](https://user-images.githubusercontent.com/827936/119248221-aae73880-bbca-11eb-916c-13d0a2bfa532.png)
    * ヘキサゴナルアーキテクチャを具体的にしたもの

* クリーンアーキテクチャ
![image](https://user-images.githubusercontent.com/827936/119248712-edf6db00-bbcd-11eb-8cc6-f84f200f2d37.png)
![image](https://user-images.githubusercontent.com/827936/119248723-0109ab00-bbce-11eb-9ce6-d18d7a3e9c45.png)
典型的な実装を想定したクラス図がすでに決まっている。が、多すぎて大変。
![image](https://user-images.githubusercontent.com/827936/119248835-c3595200-bbce-11eb-9384-6531f568d733.png)

* ADOP  
成瀬さんが考案したもの。ヘキサゴナルアーキテクチャをシンプルに実装パターンを提示したようなイメージ
![image](https://user-images.githubusercontent.com/827936/119248867-01567600-bbcf-11eb-837d-e9bf5e6d5792.png)
![image](https://user-images.githubusercontent.com/827936/119248878-1206ec00-bbcf-11eb-8135-e774f8b63e11.png)

*** 選ぶ際の観点
* メンバーの習熟度
![image](https://user-images.githubusercontent.com/827936/119249071-d4a35e00-bbd0-11eb-8af1-8ce899552f03.png)

* 事例を交えた紹介


