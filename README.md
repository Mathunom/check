# check
  checkは研究時間を記録するために作られました。基本的な使い方は指定したプロジェクトにcheck-in, check-outするというシンプルな機能です。複数のプロジェクトに対応しているので毎日の活動を記録するのに最適です。check-inした後もバックグラウンドで動いていないためコンピュータを再起動したりしても問題ありません。
  
  注意：このコマンドはMacとzshで使用することを前提に作られています。Macは標準でsqlite3を採用しています。checkはsqlite3をデータベースとして時間を記録しています。また補完関数_checkはzshのcompletionを元に作成しているため、bash等の他のシェルでの動作は保証していません。
  
  checkはたくさんのコマンドを持っています。

      check in [project] : プロジェクトにcheck-inし、測定を開始します。
      check out : プロジェクトをcheck-outし、測定を終了します。
      check stop : プロジェクトの測定を一時的に中断します。
      check resume : プロジェクトの測定を再開します。
      check list : 全てのプロジェクト名を確認します。
      check now : 現在check-inしているプロジェクトを確認します。
      check total [project] : 指定したプロジェクトの合計時間を確認します。
      check view [project] : 指定したプロジェクトの日毎の合計時間を確認します。
      check show [none or project] : 指定したプロジェクト及びすべてのプロジェクトのレコードを確認できます。
      check alter : 指定したプロジェクトの最も新しいレコードの終了時刻を変更します。
      check delete [project] : 指定したプロジェクトの最も新しいレコードを削除します。
      check drop [project] : 指定したプロジェクトを消去します。
      check dump : データベースの内容をdumpfileに記録します。
      check restore : dumpfileをデータベースに読み込みます。
      check man : checkの使い方を確認します。

　　インストールの方法
        - checkの有効化
            PATHの通ってる場所にcheckのシンボリックリンクを貼る。
            $ln -s $HOME/check/check ＄HOME/bin/check
        - 複数のMacでcheckを使用する場合
            1. 複数のMacでcheckを有効化する。
            2. Google Driveなどのクラウドサービスのフォルダ内にcheckフォルダをつくる。
                checkコマンドのdirpathとfilepathを以下のように変更する。
                  　dirpath=$HOME/check
		    filepath=$HOME/check/CHECK_TIME
		    	↓
	            dirpath=$HOME/Google\ Drive/check
	            filepath=$HOME/Google\ Drive/check/CHECK_TIME
        - checkのログをcsvで出力する
            1. コマンドラインでsqlite3を起動する。
            2. 以下のコマンドを実行する。（この際SELECT文は複数実行しないこと）
            		> .mode csv
		        > .outout ファイル名
	            	> SELECT START, END, MEMO FROM テーブル名;
