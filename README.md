# laravel-docker-template
起こったトラブル
**1.envファイルに書き込めない問題**

- **原因**: ホストのディレクトリ権限設定の不備。
- **解決方法**: 以下のコマンドで所有権を変更し、コンテナを再起動。
使用したコード
ターミナル
sudo chown -R shiny:shiny ~/coachtech/laravel/contact-form/src
docker-compose down
ocker-compose up -d --build

**2. 不要なファイルがGitで追跡される問題**

- **原因**: Dockerのボリュームデータ (`docker/mysql/data`) が追跡対象に含まれていた。
- **解決方法**: プロジェクトルートに `.gitignore` ファイルを作成し、以下を追記。
Code
`docker/mysql/data/`

**3. ContactController.phpの加筆修正が出来ない問題**
**原因**：権限がrootになっていた
**確認コマンド（ターミナル）**
ls -l /home/shiny/coachtech/laravel/contact-form/src/app/Http/Controllers/
**解決方法：所有者の変更（ターミナル）** 
sudo chown shiny:shiny /home/shiny/coachtech/laravel/contact-form/src/app/Http/Controllers/ContactController.php
※この後パスワード入力

**4. index.blade.phpがブラウザに表示されない問題**
**原因、.env内の設定がSESSION_DRIVER=fileとなっていたため**
**Laravel がアクセスできるようにしておく必要があった**
**確認コマンド（ターミナル）**
ls -l /home/shiny/coachtech/laravel/contact-form/src/storage/logs/

ls -l /home/shiny/coachtech/laravel/contact-form/src/storage/framework/
**解決方法：所有者の変更（ターミナル）** 
sudo chown -R www-data:www-data /home/shiny/coachtech/laravel/contact-form/src/storage/logs/laravel.log

sudo chown -R www-data:www-data /home/shiny/coachtech/laravel/contact-form/src/storage/framework/
※この後パスワード入力

**5.create_contacts_table.phpの編集が出来ない**
**原因権限がrootになっていた**
**確認コマンド（ターミナル）**
 ls -l /home/shiny/coachtech/laravel/contact-form/src/database/migrations/
**解決方法：所有者の変更（ターミナル）** 
sudo chown shiny:shiny /home/shiny/coachtech/laravel/contact-form/src/database/migrations/2025_08_16_085552_create_contacts_table.php
※この後パスワード入力
