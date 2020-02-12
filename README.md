# Ionicで作るモバイルアプリ制作入門［Angular版］
書籍「[Ionicで作る モバイルアプリ制作入門［Angular版］](https://amzn.to/35mKmVq)」のサポートページです。著者とIonic Japan User Groupにて運営を行っております。

## サポートチャンネル
Ionic Japan User Groupのslack #code_question でサポートを行っております。なぜかうまく動かない、よくわからない、ということありましたら挫折する前にぜひご利用くださいませー。

[Ionic Japan User Groupのslack](https://ionic-jp.herokuapp.com/)

## チュートリアル
本書のチュートリアルは、以下のレポジトリでステップ別にコミットしています。なぜか動かない時などにご利用下さい。
- [チュートリアル「タスクリストアプリをつくってみよう」](https://github.com/ionic-jp/handbook-angular-2019-tasklist-tutorial)
- [チュートリアル「WordPressを表示するアプリをつくろう / コードリファクタリング」](https://github.com/ionic-jp/handbook-angular-2019-wp-tutorial)
- [チュートリアル「Capacitorをつかったモバイルアプリ制作」](https://github.com/ionic-jp/handbook-angular-2019-native-tutorial)
- [チュートリアル「本気でつくるチャットアプリ」](https://github.com/ionic-jp/handbook-angular-2019-chat-tutorial)

## 本書での誤字・誤植
誤字・誤植についてご案内いたします。「間違った記述もしくはチュートリアルを進めることができないもの」は *致命的な誤字誤植* 、 そうでないものを *その他の誤字誤植* として案内しております。

### 致命的な誤字誤植
- P213で削除してはいけない行を削除するように案内している

```
-    },
- ];  // この行は削除してはいけません
```

- P228で、 `src/app/auth/firebase.error.ts` が `src/auth/firebase.error.ts` と表記されている

### その他の誤字誤植
- P225でInputが[type=text]になっている。なお、どちらにしてもFirebaseのチェックがあるためどちらにしても問題なく動きます

```
- <ion-input type="text" required></ion-input>  // type="email" の間違い
+ <ion-input type="text" required [(ngModel)]="login.email" // type="email" の間違い
+ name="email"></ion-input>
```

- P247の文中で、 `ionViewWillEnter()` が `ioniViewWillEnter()` と表記されてる
