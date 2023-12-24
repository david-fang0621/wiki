## Sendinblue

API Token: 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

## Hosting server

https://app.brevo.com/senders/domain/list
Email: vincent@dcs.nl
Password: 6LzPK.NGnY9JvFy!!!!

## SFTP/SSH Login:

Host: 35.228.245.82
Username: wonderwave
Password: GW8zaPcZazMGezt
Port: 13003

## Database Login:

PHPMyAdmin: https://mysqleditor-staging-wonderwave-staging.kinsta.cloud/
DB name: wonderwave
DB username: wonderwave
DB password: mMVYSuqnyTbpB3v

## DevOps Guide

This is DEV WP hosting:
Dev domein: https://uit-dev.dmilab.nl
FTP: 185.57.10.240
User: uit-dev.dmilab.nl_c6w86pnwisi
Pass: O1FoUq!8v9wcufr$

DB: admin_UIT23893io
User: usrUIT23db
Pass: \_3Giej850

https://uit-dev.dmilab.nl/wp-admin
User: UITadmin023
Pass: dk5wM\*tgg^HTFApb1q

### Workflow

- SSH
  ssh uit-dev.dmilab.nl_c6w86pnwisi@185.57.10.240
  PWD: O1FoUq!8v9wcufr$
- SQL dump
  cd backup
  mysqldump -u usrUIT23db -p admin_UIT23893io > wp_uit_db_dump.sql
  PWD: \_3Giej850
  scp uit-dev.dmilab.nl_c6w86pnwisi@185.57.10.240:~/wp_uit_db_dump.sql .
  PWD: O1FoUq!8v9wcufr$
  mv wp_uit_db_dump.sql backup/wp_uit_db_dump_20230210.sql
- WebApp dump
  zip -r wp_backup.zip httpdocs
  scp uit-dev.dmilab.nl_c6w86pnwisi@185.57.10.240:~/wp_backup.zip .
  PWD: O1FoUq!8v9wcufr$
  mv wp_backup.zip wp_backup_20230210.zip

# Live WP admin credentials

username: alexristic
email: [alexsandar1210@gmail.com](mailto:alexsandar1210@gmail.com)
password: HOwkzTYbJGlHmv$s(lWYTN$d
https://utrechtseintroductietijd.nl/wp-admin
