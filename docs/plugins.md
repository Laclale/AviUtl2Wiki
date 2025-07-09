# プラグイン一覧

!!! Warning "現在制作中です"

このページでは、AviUtl2で利用できるプラグインを一覧で紹介しています。
AviUtl2で動くプラグインを発見・自作された方は、ぜひ[プラグイン投稿フォーム](./plugin_post.md)から投稿してください。

---

<div id="script-list-container">
  <p>プラグイン一覧を読み込んでいます...</p>
</div>

<script>
  // ▼▼▼ 下の行のURLを、ステップ1でコピーしたご自身のウェブアプリURLに書き換えてください ▼▼▼
  const GAS_URL = 'https://script.google.com/macros/s/AKfycbwbx9H8i40DeeuVj8_M8bmEd6na36e-Bq6EeUBPGej_8d3zP7YVGNnD1UP7SySMPRQRfg/exec';
  // ▲▲▲ 上の行のURLを、ステップ1でコピーしたご自身のウェブアプリURLに書き換えてください ▲▲▲

  document.addEventListener('DOMContentLoaded', () => {
    const container = document.getElementById('script-list-container');

    fetch(GAS_URL)
      .then(response => {
        if (!response.ok) throw new Error('Network response was not ok.');
        return response.json();
      })
      .then(data => {
        if (data.scripts && data.scripts.length > 0) {
          let tableHtml = `
            <table>
              <thead>
                <tr><th>種別</th><th>名前</th><th>説明</th><th>制作者</th><th>ダウンロード</th></tr>
              </thead>
              <tbody>`;

          data.scripts.reverse().forEach(script => { // 新しい投稿が上に来るように逆順にする
            const author = script.author_url ? `<a href="${script.author_url}" target="_blank" rel="noopener noreferrer">${script.author}</a>` : script.author;
            const description = script.description.replace(/\n/g, '<br>');
            tableHtml += `
              <tr>
                <td>${script_or_plugin || ''}</td>
                <td>${script.name || ''}</td>
                <td>${description || ''}</td>
                <td>${author || ''}</td>
                <td><a href="${script.download_url}" target="_blank" rel="noopener noreferrer">ダウンロード</a></td>
              </tr>`;
          });

          tableHtml += `</tbody></table>`;
          container.innerHTML = tableHtml;
        } else {
          container.innerHTML = '<p>現在、登録されているプラグインはありません。</p>';
        }
      })
      .catch(error => {
        console.error('Error fetching script list:', error);
        container.innerHTML = '<p style="color: red;">プラグイン一覧の読み込みに失敗しました。ページを再読み込みするか、管理者にお問い合わせください。</p>';
      });
  });
</script>

---

!!! info "プラグインの導入方法"
    プラグインの導入方法がわからない場合は、[プラグインの導入方法](./how_to_install_plugin.md)のページを参照してください。