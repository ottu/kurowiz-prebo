# これは？
「魔法使いの黒猫とウィズ」にて実装は不可能と表明されてしまった  
プレゼントボックスのソート機能をどうにかしようと頑張るやつ。  
でもプレボの中身は全部手動管理。

## 使い方
まず news.csv にプレボのカードをひたすら写経していく。  
この時プレボの順番を守る事。  

写経が終わったら実行する。  
list.json 相当の jsonが標準出力に吐かれるので
リダイレクトして list.jsonに上書いてください。  
この動作でプログラム自身が list.json / news.csv を更新する事は無い。

カードをプレボから出した場合は、  
list.json から該当の cardオブジェクトを削除する。

カードがプレボに追加された場合は、  
news.csv に都度追加していく。

プレボの操作が終わったらまた実行する。  
news.csv のカードを追加して、list.json を再整形します。


**list.json**

これがプレボの代わりになる json。

* pages キー
  * page オブジェクトの配列
* page オブジェクト
  * page キー
    * このオブジェクトが何ページ目に当たるか
  * cards キー
    * card オブジェクトの配列  
    最大 10個まで cardオブジェクトを含む
* card オブジェクト
  * row キー
    * そのページ内の何番目に当たるか
  * element キー
    * 属性 ( fire or water or thunder )
  * rank
    * レア度 ( C+ or B or B+ or A+ or S or SS or L or 任意 )
  * name
    * 名前

**news.csv**

名前,属性,ランク の 3項目を , で区切って書く。  
このファイルの先頭から順に  
プレボの 1ページ 1枚目... 2枚目... と追加されてく。

## カードの絞り込み

未実装。  
[jq](http://stedolan.github.io/jq/) 便利だよ。  

デフォルトのソート順は 属性 > ランク > 名前 。  
cardオブジェクトの各キーを
* ソートのオーダー
* 検索キー


として使えるようにしたい。