# bcrypt 

## Intro 
Password hashing is crucial for protecting your data from attackers. It converts user credentials into an unreadable string of characters, making it difficult for unauthorized access.


1. Hashing :- a process that converts Text into a key
2. Password Hashing: This is a specific application of hashing where a password is converted into a fixed-length string. It’s a one-way process, meaning you can’t reverse the hash to get the original password. Each time the same password is hashed, it should produce the same hash, but with techniques like salting, even the same password can generate different hashes to enhance security.


### bcrypt provide two important methods to hash the password and compare hash and password to return true value

#### 1. bcrypt.hash()
 this method takes 3 parameters (text,saltRound,callback(optional))

 1. text :- eg "Abhinish123"
 2. saltround : - also called as `cost factor` , eg if we have 10 then hash function runs 2pow10 times to generate a strong password.
 3. callback :- it takes 2 arguments , (err,hashedpassword).


```javascript
//without callback
//its async because of takingmore time

const bcrypt = require("bcrypt");

async function hashPassword(name) {
  let hasedP = await bcrypt.hash(name, 10);
  console.log(hasedP)
}

checkPassword("Abhinish");
```

Output :- `$2b$10$0jsSrswwWlZnWUaMH9LPb.wCEYff1PjOg5YQvbClV
yd4UGEeL8SdG`


this is the hashed password

let's do the postmatam of this output.

1. Prefix(`$2b$`)
2. Cost Factor(`10`) :- hashing algorithm was applied 10 times.
3. Salt and Hash(`$0jsSrswwWlZnWUaMH9LPb`) :- first 22 character before `.` is the *salt*, and remaining is the *hashed Password* (`wCEYff1PjOg5YQvbClV
yd4UGEeL8SdG`)

















