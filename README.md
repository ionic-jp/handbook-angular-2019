# Ionicで作るモバイルアプリ制作入門［Angular版］
書籍「[Ionicで作る モバイルアプリ制作入門［Angular版］](https://amzn.to/35mKmVq)」のサポートページです。著者とIonic Japan User Groupにて運営を行っております。

## 【重要】Ionic5リリースによる変更
2020年2月12日にIonic5がリリースされました。それに伴ってスターターテンプレートのアップデートがあったため、 **書籍の通りに進めるためには以下の読み替えが必要です。**
なお、スターターテンプレートの変更があっただけですので、パッケージのバージョンをあげることには問題はありません（2020年2月12日現在）。

また 新しいUIデザインを使ったすばらしいスターターテンプレートを利用できますので、ぜひ自分のプロダクトでプロジェクトをつくる時は `ionic start --type=angular` コマンドをご利用ください。

### 1) P43 SECTION 06 プロジェクトをつくろう
コマンドを以下の通り変更ください。なお、作成するプロジェクト名の質問と `? Starter template:` のテンプレートの選択はスキップされます。

```bash
% ionic start --type=angular
↓
% ionic start 'tasklist-tutorial' https://github.com/ionic-jp/starters-v4-angular-sidemenu.git
```

### 2) P113 SECTION 14 WordPressを表示するアプリを作ろう〜チュートリアル②
コマンドを以下の通り変更ください。なお、 `? Starter template:` のテンプレートの選択はスキップされます。

```bash
% ionic start wp-tutorial --type=angular
↓
% ionic start 'wp-tutorial' https://github.com/ionic-jp/starters-v4-angular-blank.git
```

### 3) P169 SECTION 19 Capacitorを使ったモバイルアプリ制作〜チュートリアル④
コマンドを以下の通り変更ください。なお、 `? Starter template:` のテンプレートの選択はスキップされます。

```bash
% ionic start native-tutorial --type=angular
↓
% ionic start 'native-tutorial' https://github.com/ionic-jp/starters-v4-angular-tabs.git
```

### 4) P207 SECTION 21 本気で作るチャットアプリ〜チュートリアル⑤
コマンドを以下の通り変更ください。

```bash
% ionic start chat-tutorial tabs --type=angular
↓
% ionic start 'chat-tutorial' https://github.com/ionic-jp/starters-v4-angular-tabs.git
```

## 【重要】Capacitor4リリースによる変更
Capacitor4リリースがリリースされました。Capacitor4ではコアプラグインは本体から外れ、別パッケージになったため、追加でパッケージのインストールが必要です。

- P179にて以下のコマンドを実行

```bash
% npm install @capacitor/local-notifications
% npm install @capacitor/camera
% npx cap sync
```

また、このことでインポート元が変更になります。

- P182

```diff
- import { Plugins } from '@capacitor/core';
+ import { LocalNotifications } from '@capacitor/local-notifications';
...
- Plugins.LocalNotifications.schedule({
+ LocalNotifications.schedule({
```

- P196

```diff
- import { Plugins } from '@capacitor/core';
+ import { Camera, CameraResultType, CameraSource } from '@capacitor/camera';
...
- const image = await Plugins.Camera.getPhoto({
+ const image = await Camera.getPhoto({
```

同様に、利用してるプラグインが `@rdlabo/capacitor-admob` から `@capacitor-community/admob` に変更となります。

- P186

```diff
- npm install @rdlabo/capacitor-admob
+ npm install @capacitor-community/admob
```

- P188

以下のAndroidのプラグインを `MainActivity `で `add` する処理は不要になりました。

```
add(jp..rdlabo.capacitor.plugin.admob.Admob.class)
```

- P189

```diff
- import { Plugins } from '@capacitor/core';
+ import { Admob } from '@capacitor-community/admob'
...
- Plugins.Admob.initialize({
+ Admob.initialize({
```

- P190

```diff
- import { Plugins } from '@capacitor/core';
- import { AdOptions, AdSize, AdPosition } from '@rdlabo/admob';
+ import { Admob, AdOptions, AdSize, AdPosition } from '@capacitor-community/admob';
...
- Plugins.Admob.showBanner(options).then({
+ Admob.showBanner(options).then({
...
- Plugins.Admob.hideBanner(options).then({
+ Admob.hideBanner(options).then({
```

詳細は、 https://github.com/capacitor-community/admob をご確認ください。

### @ionic-nativeパッケージが削除されています
P71などに、 `@ionic-native/core` 、 `@ionic-native/splash-screen` 、　`@ionic-native/status-bar` といった表記があり、インポートされたり、providersに入ったりしておりますが、Capacitor4以降これらは不要になったため、テンプレートファイルから削除されています。

また、Capacitorプラグインが充実し、Cordovaプラグインを使う必要が薄くなったことから、P192の「Cordovaプラグインを使ってバッジで通知数を知らせよう」は非推奨とします。もしも自分でチャレンジする場合は、 `@ionic-native` が、 `@awesome-cordova-plugins` にリネームされたことを念頭にお試しください。詳しくは以下記事をご覧ください。

https://ionic.io/blog/a-new-chapter-for-ionic-native


### iOS15からの変更
iOS15からPush通知まわりでユーザにパーミッションを求めないと権限を受け取ることができなくなりました。それに伴い、P182で以下のコードの変更が必要です。

```diff
- localNotification() {
+ async localNotification() {
+     await Plugins.LocalNotifications.requestPermissions();
      Plugins.LocalNotifications.schedule({
```

## 【重要】 @angular/fire6.0.0からの変更
`@angular/fire@6.0.0` から仕様に変更があったため、以下を読み替えてください。
- SECTION21全般
新APIが公開されたため、書籍で利用してるAPIは互換APIとなります。すべての `@angular/fire` のインポートパスを `@angular/fire/compat` としてください。例えば、P210では以下のように読み替えてください。

```diff
- + import { AngularFireModule } from '@angular/fire';
- + import { AngularFireAuthModule } from '@angular/fire/auth';
+ + import { AngularFireModule } from '@angular/fire/compat';
+ + import { AngularFireAuthModule } from '@angular/fire/compat/auth';
```


APIが変更され、AngularFireAuth以下の `auth` が不要となりました。 `this.afAuth.auth.****()` は `this.afAuth.****()` となります。例えば、P219では以下のように読み替えてください。

```diff
- + return this.afAuth.auth
+ + return this.afAuth
```

- P243の `this.afAuth.currentUser` メソッドがPromiseになったため、以下に変更。

```diff
- getUserId(): string {
-   return this.afAuth.currentUser.uid;
+ async getUserId(): Promise<string> {
+   const user = await this.afAuth.currentUser;
+   return user.uid;
  }
```

また、そのため、 `getUserId()` メソッドを利用していたところには、 `await` を追加する必要があります。

- P244の `ionViewWillEnter()` 内
```diff
- this.uid = this.auth.getUserId();
+ this.uid = await this.auth.getUserId();
```

- P248の `tab1.page.ts` - `ngOnInit()` 内
```diff
- const user = this.firestore.userInit(await this.auth.getUserId());
+ const user = await this.firestore.userInit(await this.auth.getUserId());
```

- P257の `tab1.page.ts` - `ionViewWillEnter` 内
```diff
- this.uid = this.auth.getUserId();
+ this.uid = await this.auth.getUserId();
```


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
