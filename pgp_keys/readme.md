# Working With PGP Keys General 
When working with Terraform, for some actions, there is needed to work with the PGP keys encoded in base64. Especially, pgpkey is needed for:
* iam_user
* aws_iam_access_key  
* etc

## Working Keys
Let's start with listing keys (before that there is needed to be installed gnugpg:
```javascript
gpg --list-keys
gpg --list-secret-keys
```

For example key will be named "test-key"
```javascript
gpg -o ./test-key.gpg  --export test-key
```
Convert key:
```javascript
cat ./test-key.gpg | base64 | tr -d '\n' > ./test-key.gpg.base64
```

After conversion you will be able to see base64 encrypted public key:
```javascript
cat ./test-key.gpg.base64
```

Import thru default varibale in Terraform:
```javascript
variable "pgp_key" {
    default = "key_output_oumitted"
}
```

Run apply

Then decrypt key

terraform output encrypted_variable | base64 -D | gpg -r test-key

