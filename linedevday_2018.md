# LINE Developer Day2018
## 全体
AI関連のトークが多い

### ネタ
意外と硬い雰囲気  
ほとんどMacユーザー  
wifi完備  
準備大変そう これ用に公式アカウントとかcwaとか  
スライドが英語  

## 10:40 Opening Session - "Next LINE" LINEが創る新たな世界 -
朴イビン LINE / CTO  
open api でいろいろ利用できるものが増えている  
Liff とか  
LINEはAIとブロックチェーンにフォーカスしている  
## いけべさんパート AI
・Clova  
　ClovaはAIの名前。LINE でAIといえばClovaを去年出した。  
　Wave、フレンズ、フレンズミニの3つがある

・LINEニュース  
　各個人に最適な情報をAIをつかって配信  
・Smart Channel  
・Shopping LENS  
　画像から商品を検索  
・Character Effect  
　テレビ電話で、キャラクターが表情にあわせて会話する  

今後はさらに自社サービスだけでなくテクノロジそのものを開発者の皆様に提供したい

・今後のサービス  
Clovaとチャットぼっとの連携

OCR  
画像を認識してテキストに起こす  
　→スクショを貼り付けて、コピペや翻訳できる

## なすさんパート ブロックチェーン
LinkChain  
サービスからユーザーへお金が流れやすくなる。  
安全性と透明性の実現がメリット。  

・ユーザーメリット  
　透明性と安全性

・企業メリット  
　煩雑な手続きなしに、ユーザーにお金を渡せる

ブロックチェーンを用いたプラットフォームを新たに築くのは、なかなか大変なこと。  
開発者なら簡単にLinkChainを使うことができ、一般開発者は夏くらいから使えるようになるそうです。

## 再びイビンさんパート
今年はFintech

## いけださんパート Fintech
LINE Pay  
　QRコード決済に注力  
　自動販売機でLINEをかざすとジュースが買える  
　店舗側は小さい端末１つ入れるだけで、POSの改修は発生しない  

Pay利用者 4000万人  
月の取引額 125Billion

### 最近のサービス
・BitBox  
　仮想通貨  
・LINE保険  
　旅行の保険とか。profile+に登録すれば、入力不要になる  
・LINE家計簿  

今後LINEはクロージング the Distanceを掲げて、金融と皆さんの距離を縮めて行きたい

## パネルディスカッション: グローバルな組織で働くエンジニアから見たLINEのエンジニアカルチャー
LINEエンジニアの人数：2,100人　→　3,000人目指す  
海外の人が多い

### LINEの文化
TakeOwnerShip  
　自動ログインは、エンジニア発で発信し各サービスに浸透した  
Be Open  
　ほとんどのPJのソースコードがgithub上で全て見れる  
　タウンホールMtgでは、CTOなど役員が出席し、質問に答える  
Trust & Respect  
　基本的にMicroServiceな作りになっており、連携先のシステムを信頼して動いている  

## LINEのインフラプラットフォームはどのように大規模サービスをスケールさせ運用コストの小さなインフラを提供しているのか
LINEではOSレイヤー以下をインフラチームが担当 &  storage領域(DBなど)

### 課題
・データセンター内のサーバ間通信のネットワークをいかにさばくか  
・connection数の問題  
　LINEユーザー数：165,000,000 + MAU
　→　LBのセッションテーブルの枯渇
　LBはDSR(サーバからクライアントへの通信量は大きいのでLBを通さないようにするため)  
　→　通信量の対策にはよいが、セッションテーブルを圧迫しやすい設計  
・開発チームの増加の問題  
　→　利用者ごとに担当者がつくのは限界が来ていた

### 課題に対する考え方
・根本解決  
・運用負荷を下げる解決策  

### 対応方針
・圧倒的なキャパシティの実現  
・2Nの冗長化をやめる  
・運用負荷下げる  

### 解決策
CLOS Network
　→　冗長構成がN+1 で可能

L2 VS L3  
　→　L2はgraceful なフェイルオーバーができない  
　　　→　メンテナンス性を考えて、L3  
　　　→　APレイヤーに影響がでるが、開発者に協力してもらった  

LBは L3 → L4 → L7
　L3 はAnycast + ECMP で解決  
　L4 は難しい  
　　→　セッションテーブルを使ったステートフルな作りだと無理(セッションテーブル枯渇するため)
　　　→　sourceIp,distIp, port, protocol, , の5つのハッシュを使う  
　L4のパフォーマンス要件
　　→　 XDPを使ったソフトウェアベースのLBを開発(linux上)
  
LINEのインフラのPrivate Cloud化  
　Verdaを構築  
　　サーバの配置・vip・ネットワークなど、Verdaが適切に設定してくれる  
　　ただし、外部にサービスを公開する際には、申請を出して、ACLを通す  

### まなび
・大きな変化(改善)の際には、ゴールを明確にすることが重要  
・インフラはライフサイクルがあるので、適切なタイミングで改善をする必要がある  

### 今後
・SRv6 を使って、マルチテナントに対応  
・Verda上で作成できるkubernetes クラスタ  
・kubernetes上にイベントハンドラのプラットフォーム構築  
　logのイベントやVMのイベントなどにfunctionとaction を設定できる
　　Knative


##フロントエンド開発によって進化するLINEの未来
### フロントエンドチームの組織について
UITチーム(UserInterfaceTechnology)  
海外含め7拠点、100名以上のエンジニア  
オフラインでの交流もある(2日間のOSSへの貢献への取り組みなど)

### WebApp
FamilyService が多い  
News、キャリア、デリマ、LINEマンガ  などなど  

### Challenge
HYBRID APP  
　Apache Coldvaを使ったネイティブ上でwebを動かす  

LINEはSPAが多い  
　→　JSの肥大化の問題  
　→　Code Splitting  　
　→　grow loader というCodeSplitting を開発し、OSSで提供  

SKELTON SCREEN  
PAGE Transition

LINE Analytics  
　torimochi  
Heat Map  
　yakimochi  
UI FRAMEWORK  
　koromo  
　koromo-vue  
　　→　LINEでよく使うものをコンポーネント化  
SASS LIBRARY  
　sasslai  
LIFF(LineFrontendFramework)  
　カスタムURLで、トークルーム内にwebがひらける  
　LIFF SDKを使うと、MessagingAPIのユーザーtoユーザーのメッセージ送信が簡単にできる  
　すでに500以上のLIFFアプリケーションがある  

## LINE QR Code Loginとそれを支える技術
尾上良範  
LINE / DP2チーム  
サーバサイドは全てkotlin

QRコードログイン  
　PCブラウザにQRコードを表示し、スマホで読み込むことで、PC側がログイン状態になる  

Spring5.0から導入されたSpring WebFluxを利用
　→　SpringMVCでやると、1リクエスト1スレッドになるので、待機スレッドが枯渇する  
　→　WebFluxだと、Servlet機能つかえないので、作り直し大  

## MySQL Query Re-player: パケット解析によるクエリの観測とその再現
大塚知亮 LINE / DB1チーム  

クエリをパケットキャプチャして、Goの構造体に変換するツール
