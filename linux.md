# linux notes
- openssl 
  - enc
    $ echo $string | openssl enc -aes-256-cbc -a -pass pass:$pass 
  - dec
    $ echo $string | openssl enc -aes-256-cbc -d -pass pass:$pass 
- top
  - one shot
    $ top -d 0 -bn 1
