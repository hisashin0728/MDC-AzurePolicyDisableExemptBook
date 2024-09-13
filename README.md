# MDC-AzurePolicyDisableExemptBook
本レポジトリは Microsoft Defender for Cloud で設定されているイニシアティブの無効化/適用除外を可視化するブックです。

# Book Image
> 可視化イメージ

- parameter でサブスクリプション毎に filter 可能
- 適用除外/無効化を filter 可能

![image](https://github.com/user-attachments/assets/8aab9a38-c892-4609-9c70-e5e839d476e5)

# How to Install
> ブック導入方法

- MDC ブックより、「空にする」を選択
![image](https://github.com/user-attachments/assets/1850c9c2-1f24-4db6-9f3f-6de07ac8783e)

- 「詳細エディター」から「ギャラリーテンプレート」を開く
![image](https://github.com/user-attachments/assets/5d43f674-9c78-47c2-94c4-15dcb048c46e)

- [こちらのJSONファイル](https://github.com/hisashin0728/MDC-AzurePolicyDisableExemptBook/blob/main/MdcExemptDisableBook.json)をコピーして保存

# 制限事項など
> 現在分かっている仕様

- Microsoft Defender for Cloud 側の仕様により、出力されるのは Azure Policy で提供されるポリシーの無効化/適用除外になります。
- 適用除外時に追加できるコメントは、Azure Resource Graph で取得がサポートされておりません。
  - 適用除外時のコメントも含めてリストを取得したい場合は、以下 Powershell スクリプトをご活用下さい

```powershell
# 必要なモジュールをインポート
Import-Module Az.Resources

# Azureにログイン
#Connect-AzAccount

# Get-AzPolicyExemptionを実行し、結果を取得
$exemptions = Get-AzPolicyExemption

# 結果をCSVファイルにエクスポート
$exemptions | Export-Csv -Path ".\output.csv" -NoTypeInformation -Encoding UTF8

# 完了メッセージ
Write-Output "Exemptions have been exported to current directory output.csv"
``` 

``Get-AzPolicyExemption`` で生成された CSV ファイルを Excel 等でデータインポートして下さい。
![image](https://github.com/user-attachments/assets/521e9f66-72f6-4ed7-b24e-2cfc422ebca7)



