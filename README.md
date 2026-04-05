株式会社EISHINでの長期インターンにて担当した複数のコーポレートサイト新規構築案件のうち、一部を抽出して掲載しています。著作権の都合上、画像・文章はダミーに差し替えています。<br>
【開発背景】既存のHPが古くなったためリニューアルを検討しており、「デザインを新しくしたい」「自社で手軽にコンテンツを更新したい」というクライアントの要望を解決するために制作されました。<br>
【利用技術】HTML5, CSS3 (Sass), JavaScript, PHP, WordPress<br>
【開発環境】Local (Local by Flywheel), VS Code, Cyberduck (FTPソフト), Git, Figma<br>
【チーム構成】3名（ディレクター1名、デザイナー1名、エンジニア1名：本人）。実装からテスト環境への公開作業までを一人で完遂しました。<br>
【担当領域】コーディング全般、WordPressテーマ化、カスタムフィールドを用いた更新機能の実装、サーバーへのファイル転送。<br>
【工夫したところ（まとめ）】<br>
デザインの指定がなかったタブレット表示は、PCとスマホのデザインをもとに自分で考えて実装しました。デザインそのものは変えられない制約の中で、ホバーアニメーションやスクロール連動など動きで視覚的なわかりやすさを高めることに注力しました。また各ページのボタンやセクション構造が似ていることに着目し、プロパティを少し変えるだけで使い回せる柔軟なコンポーネントとして設計したことで、実装効率を大幅に向上させました。納期通りにミスなく確実に動くものを納品することにも注力しました。
【特に工夫した点（抜粋）】<br>

工夫した点１　フォームバリデーションを自前で実装<br>
【課題】社内で用意されていたバリデーションのコードをそのまま使えば簡単に実装できましたが、仕組みを理解せずに使うだけでは成長につながらないと考えました。またもともとのデザインは未入力のままでも送信できてしまう状態でした。<br>
【対応】あえて自分で一から実装しました。未入力や形式不正（カタカナ・電話番号・メールアドレス）の場合、該当項目の下に赤字でエラーメッセージを表示することで、ユーザーが何を入力すべきか直感的にわかるようにしました。

<img width="400"  alt="image" src="https://github.com/user-attachments/assets/a4e80d08-0438-4bed-9562-a91dc6cea1ce" />

<details>
<summary>バリデーション例（フリガナ）</summary>
<pre>

var katakanaRegex = /^[ァ-ヶー　]*$/;

if (value === "") {
  errorMessage.textContent = "フリガナを入力してください。";
} else if (katakanaRegex.test(value)) {
  errorMessage.textContent = "";
} else {
  errorMessage.textContent = "カタカナで入力してください。";
}

</pre>
</details>




次のテキスト




工夫した点２　開発実績ページの管理画面を一本化<br>
【課題】当初はモビリティ・AV機器・医療ヘルスケアなど各カテゴリをサイドバーに個別に作成する想定でしたが、カテゴリが増えるたびに管理画面が増えてクライアントが迷う可能性がありました。また各カテゴリで表示する項目が若干異なるため、個別対応が必要でした。<br>
【対応】カスタム投稿タイプで「開発実績」を一つ作りその中にまとめることで、クライアントが迷わず編集できる構成にしました。入力がない項目はHTML構造ごと出力しない仕組みをテンプレート側で実装し、1つの共通フィールドセットで全カテゴリに対応できるようにしました。新規カテゴリの追加も既存のフィールドセットを流用するだけで対応でき、長期的な保守コストの削減にもつながっています。
<img width="400" alt="Gemini_Generated_Image_839iya839iya839i" src="https://github.com/user-attachments/assets/4f14cca9-d7e3-4d37-b854-e89412749764" />
<img width="400"  alt="image" src="https://github.com/user-attachments/assets/310cde30-1e17-4ee8-b8ca-885ae155cbce" />


<br><br><br>

工夫した点３　スクロールに応じてヘッダーの背景を切り替え<br>
【課題】トップページのヘッダーは初期状態では背景透過でメインビジュアルに溶け込む見た目にしていましたが、スクロールするにつれて背景画像との兼ね合いで文字が見づらくなっていました。<br>
【対応】スクロールし始めると背景が白に切り替わるよう実装しました。getBoundingClientRect()でヘッダーとメインビジュアルの位置を比較し、重なったタイミングでクラスを付け替えることで切り替えを実現しています。

<img width="400" alt="image" src="https://github.com/user-attachments/assets/f845c1f1-52d4-4f2a-99f1-6c29156a6e59" />
<img width="400"  alt="image" src="https://github.com/user-attachments/assets/5cdd8caa-fd85-4eed-91f0-43429e375053" />


<br><br><br>

工夫した点４　トップページの開発事例セクションにカテゴリホバーで画像を切り替える機能を実装<br>
【課題】当初は画像が切り替わらない仕様で、どのカテゴリに対応する内容なのか視覚的に伝わりづらかったです。<br>
【対応】自分からホバーで画像が切り替わる機能の追加を提案し実装しました。WordPressのループ内でカテゴリと画像に同じ連番のIDを自動で振り、ホバー時にJSがその番号をもとに対応する画像を探して表示する仕組みにしています。管理者は管理画面から画像をアップロードするだけで自動的にIDが振られてカテゴリと紐づくため、JSを変更する必要がなく簡単に運用できます。
<details>
<summary>PHP：連番IDの生成（参考）</summary>
<pre>
$args = array(
  'post_type' => 'post',
  'posts_per_page' => -1,
);
query=newWPQuery(query = new WP_Query(
query=newWPQ​uery(args);
if ($query->have_posts()):
  $counter = 1;
  while ($query->have_posts()):
    $query->the_post();
?>
    &lt;a id="item-&lt;?php echo $counter; ?&gt;"&gt;
      &lt;?php the_title(); ?&gt;
    &lt;/a&gt;
&lt;?php
    $counter++;
  endwhile;
endif;
wp_reset_postdata();
</pre>
</details>
<details>
<summary>JavaScript：ホバー処理（参考）</summary>
<pre>
items.forEach((item) => {
  item.addEventListener("mouseenter", function () {
    document.querySelectorAll(".innerItem").forEach((el) => {
      el.classList.remove("active");
    });
const targetId = `item-${this.id.split("-")[1]}`;
const target = document.getElementById(targetId);
if (target) {
  target.classList.add("active");
}
});
});
</pre>
</details>


https://github.com/user-attachments/assets/b848cf19-445b-47c4-8a34-262dfeb61678




<br><br><br>

工夫した点５　企業情報の沿革ページのスライダーをSplideで実装<br>
【課題】当初Swiperで実装を試みましたが、SwiperはスライドのサイズをJSがpxで計算する仕組みのため、gapや子要素の%指定と噛み合わずデザイン通りに実装できませんでした。またSplideにはプログレスバーが標準搭載されていないため、別途実装が必要でした。<br>
【対応】自分からSplideへの切り替えを提案したところ、SplideはCSSのflexで幅を管理するためカスタムスタイルと競合せず問題を解消できました。プログレスバーは自前で実装し、スライドが動くたびに現在位置と総スライド数から進捗率を計算してバーの幅をパーセントで変化させることで現在位置を視覚的に表示しています。

<details>
<summary>プログレスバーの実装</summary>
<pre>
var bar = splide.root.querySelector(".my-carousel-progress-bar");
splide.on("mounted move", function () {
var end = splide.Components.Controller.getEnd() + 1;
var rate = Math.min((splide.index + 1) / end, 1);
bar.style.width = String(100 * rate) + "%";
});
</pre>
</details>


https://github.com/user-attachments/assets/3fa7a337-61f2-4fe0-9142-c997595e307b





工夫した点６　ブレイクポイントで画像エリアを広く見せるレイアウト調整<br>
【課題】画面幅が狭いときは左のテキストが改行されて縦に長くなり、画像エリアが圧迫されてカードが見切れていました。また画面幅が広くなりすぎると画像とテキストが離れすぎて見づらくなる問題もありました。<br>
【対応】ブレイクポイントでテキストの改行を調整して画像エリアを広く確保し、max-widthで幅を固定して中央寄せにすることでデザインの崩れを防ぎました。

https://github.com/user-attachments/assets/ad55268b-1aa7-49a9-b94e-54c0fd073faf

https://github.com/user-attachments/assets/b0216fca-c23f-4eb6-927a-930b2cdeae0a

工夫した点７　ホバーアニメーションでクリックできることを伝える<br>
【課題】もともとのデザインは矢印の色が反転するだけで、その項目がクリックできることが伝わりづらかったです。<br>
【対応】カーソルを乗せた項目の画像が拡大するアニメーションを追加し、ユーザーが「ここを押せる」と直感的にわかるようにしました。

https://github.com/user-attachments/assets/793e179b-d9db-4b0f-b475-f695277e6eb3





