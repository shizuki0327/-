[validation.js](https://github.com/user-attachments/files/26404693/validation.js)概要〉株式会社EISHINでの長期インターンにて担当した、株式会社エクスのコーポレートサイト新規構築案件です。
【開発背景】既存のHPが古くなったためリニューアルを検討しており、「デザインを新しくしたい」「自社で手軽にコンテンツを更新したい」というクライアントの要望を解決するために制作されました。
【利用技術】HTML5, CSS3 (Sass), JavaScript, PHP, WordPress
【開発環境】Local (Local by Flywheel), VS Code, Cyberduck (FTPソフト), Git, Figma
【チーム構成】3名（ディレクター1名、デザイナー1名、エンジニア1名：本人）。実装からテスト環境への公開作業までを一人で完遂しました。
【担当領域】コーディング全般、WordPressテーマ化、カスタムフィールドを用いた更新機能の実装、サーバーへのファイル転送。
【工夫したところ】初めての実案件として、納期通りにミスなく確実に動くものを納品することに注力しました。「開発実績」ページはもともと管理画面から編集できない想定でしたが、実績は頻繁に更新されるものだと考え、モビリティ・AV機器・医療ヘルスケアなど多岐にわたるカテゴリごとに簡単に追加・変更できるよう、管理画面から編集できる構成を自ら提案し実装しました。また各ページのボタンやセクション構造が似ていることに着目し、プロパティを少し変えるだけで使い回せる柔軟なコンポーネントとして設計したことで、実装効率を大幅に向上させました。さらに、数年後に別の開発者が見ても迷わないよう、保守性を意識して常にコードを整理し、読みやすい状態に保つことを心がけました。

工夫した点１　フォームバリデーションを自前で実装
社内で用意されていたバリデーションのコードをそのまま使わず、仕組みを理解するためにあえて自分で実装しました。コードとしては冗長な部分もありますが、一から書くことでフォームの動作原理を深く理解することができました。
未入力や形式不正（カタカナ・電話番号・メールアドレス）の場合、該当項目の下に赤字でエラーメッセージを表示を以下の写真のように表示しました
<img width="500"  alt="image" src="https://github.com/user-attachments/assets/40a0c5e5-b898-495b-afb8-46d9157d0bce" />
[Uploadocument.addEventListener(
  "wpcf7submit",
  (e) => {
    const form = e.target;
    // 氏名フィールドのバリデーション
    const selectedName = form.querySelector('input[name="your-name"]');
    const nameErrorMessage = form.querySelector(".name-error-message");

    if (selectedName && nameErrorMessage) {
      if (!selectedName.value || selectedName.value.trim() === "") {
        nameErrorMessage.textContent = "氏名を入力してください";
      } else {
        nameErrorMessage.textContent = "";
      }
    }

    // フリガナフィールドのバリデーション
    const selectedFurigana = form.querySelector('input[name="your-furigana"]');
    const furiganaErrorMessage = form.querySelector(".furigana-error-message");

    var katakanaRegex = /^[ァ-ヶー　]*$/;

    if (selectedFurigana && furiganaErrorMessage) {
      const value = selectedFurigana.value.trim(); // ← これが超重要

      if (value === "") {
        furiganaErrorMessage.textContent = "フリガナを入力してください。";
      } else if (katakanaRegex.test(value) && value !== "") {
        // 空欄（""）は通さない
        furiganaErrorMessage.textContent = "";
      } else {
        furiganaErrorMessage.textContent = "有効なカタカナを入力してください。";
      }
    }

    // 電話番号フィールドのバリデーション
    const selectedPhone = form.querySelector('input[name="your-tel"]');
    const phoneErrorMessage = form.querySelector(".tel-error-message");

    var regex =
      /^(0[5-9]0[-(]?[0-9]{4}[-)]?[0-9]{4}|0120[-]?\d{1,3}[-]?\d{4}|050[-]?\d{4}[-]?\d{4}|0[1-9][-]?\d{1,4}[-]?\d{1,4}[-]?\d{4})*$/;
    if (selectedPhone.value.trim() === "") {
      phoneErrorMessage.textContent = "電話番号を入力してください。";
    } else if (regex.test(selectedPhone.value)) {
      phoneErrorMessage.textContent = "";
    } else {
      phoneErrorMessage.textContent = "有効な電話番号を入力してください。";
    }

    // メールフィールドのバリデーション
    const selectedMail = form.querySelector('input[name="your-email"]');
    const mailErrorMessage = form.querySelector(".email-error-message");

    var mailpattern =
      /^[A-Za-z0-9]{1}[A-Za-z0-9_.-]*@{1}[A-Za-z0-9_.-]+.[A-Za-z0-9]+$/;
    if (selectedMail.value.trim() === "") {
      mailErrorMessage.textContent = "メールアドレスを入力してください。";
    } else if (mailpattern.test(selectedMail.value)) {
      mailErrorMessage.textContent = "";
    } else {
      mailErrorMessage.textContent = "有効なメールアドレスを入力してください";
    }
  },
  false,
);

const selectedCheck = document.querySelector('input[name="acceptance-956"]');
const checkErrorMessage = document.querySelector(".check-error-message");
const validateCheck = () => {
  if (selectedCheck && checkErrorMessage) {
    if (!selectedCheck.checked) {
      checkErrorMessage.textContent = "同意してください。";
    } else {
      checkErrorMessage.textContent = "";
    }
  }
};

if (selectedCheck) {
  // 'change' イベント（チェックの状態が変わったとき）を監視
  selectedCheck.addEventListener("change", validateCheck);
}
ding validation.js…]()

