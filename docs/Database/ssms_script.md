# SQLServer SSMSでテーブルをスクリプト化する

SSMS (SQL Server Management Studio) のコマンドを使用することで、スクリプトを作成できる<br>
現在のデータベース状態を保存しておくことで、差分比較や切り戻しに使える<br>

## Usage
データベース名をクリックして、タスク→スクリプトの作成と進む<br>

![script_step1](img/ssms_script_step1.png)

次へを選択<br>

![script_step2](img/ssms_script_step2.png)

出力したいテーブルを選択<br>

![script_step3](img/ssms_script_step3.png)

詳細設定」をクリックして、「スクリプトを作成するデータの種類」から選択<br>
「スキーマとデータ」を選ぶとテーブル作成、データ挿入の両方のスクリプトが作成される<br>

![script_step4](img/ssms_script_step4.png)

出力先の設定を選択<br>

![script_step5](img/ssms_script_step5.png)

概要の確認、次へを選択<br>

![script_step6](img/ssms_script_step6.png)

この画面がでたら完了<br>

![script_step7](img/ssms_script_step7.png)

## 単一テーブルをスクリプト化する場合
テーブル単体をスクリプト化する場合は、テーブルを右クリックが早い<br>

![script_single](img/ssms_script_single.png)

## Reference
[SQL Server Management Studio でオブジェクトのスクリプトを作成する](https://learn.microsoft.com/ja-jp/sql/ssms/tutorials/scripting-ssms?view=sql-server-ver16)<br>
