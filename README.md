<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<title>猿田彦数秘計算ツール</title>
<style>
body { font-family: sans-serif; padding: 20px; }
input, button { font-size: 1rem; margin: 5px; }
table { border-collapse: collapse; margin-top: 10px; }
td, th { border: 1px solid #999; padding: 5px 10px; text-align: center; }
</style>
</head>
<body>

<h2>猿田彦数秘計算ツール</h2>
<p>名前を入力して「計算」ボタンを押してください。</p>
<input type="text" id="nameInput" placeholder="例: yawarainokuma">
<button onclick="calculate()">計算</button>

<table id="resultTable">
<tr>
<th>方式</th>
<th>コア</th>
<th>ペルソナ</th>
<th>ロード</th>
</tr>
</table>

<script>
// モダン式アルファベット対応
const modern = {
  A:1,B:2,C:3,D:4,E:5,F:6,G:7,H:8,I:9,J:1,K:2,L:3,M:4,N:5,O:6,P:7,Q:1,R:9,S:1,T:2,U:3,V:4,W:5,X:6,Y:7,Z:8
};
// カリオストロ式アルファベット対応
const cali = {
  A:1,B:2,C:3,D:4,E:5,F:8,G:3,H:5,I:1,J:1,K:2,L:3,M:4,N:5,O:7,P:8,Q:1,R:2,S:3,T:4,U:6,V:6,W:6,X:6,Y:1,Z:7
};
const vowels = ['A','E','I','O','U']; // Yは子音扱い

function calculate() {
  const name = document.getElementById('nameInput').value.toUpperCase().replace(/[^A-Z]/g,'');
  
  function compute(table) {
    let core=0, persona=0, total=0;
    for (let ch of name) {
      const val = table[ch] || 0;
      total += val;
      if(vowels.includes(ch)) core += val;
      else persona += val;
    }
    return {core, persona, total};
  }

  const modernRes = compute(modern);
  const caliRes = compute(cali);
  const sarutaCore = modernRes.core + caliRes.core;
  const sarutaPersona = modernRes.persona + caliRes.persona;
  const sarutaTotal = modernRes.total + caliRes.total;

  const tableEl = document.getElementById('resultTable');
  tableEl.innerHTML = `
    <tr>
      <th>方式</th><th>コア</th><th>ペルソナ</th><th>ロード</th>
    </tr>
    <tr>
      <td>モダン式</td>
      <td>${modernRes.core}</td>
      <td>${modernRes.persona}</td>
      <td>${modernRes.total}</td>
    </tr>
    <tr>
      <td>カリオストロ式</td>
      <td>${caliRes.core}</td>
      <td>${caliRes.persona}</td>
      <td>${caliRes.total}</td>
    </tr>
    <tr>
      <td>猿田彦数秘（合算）</td>
      <td>${sarutaCore}</td>
      <td>${sarutaPersona}</td>
      <td>${sarutaTotal}</td>
    </tr>
  `;
}
</script>
</body>
</html>
