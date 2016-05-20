## Manage Passwords
Don't use outdated hashing algorithms like MD5. Hashing a password with MD5 is virtually useless. Don't come up with your own encryption scheme. Choose a one-way encryption algorithm. Once you've encrypted and stored a user's password, you never need to know the real value. When a user attempts to authenticate, you'll just apply the same algorithm to the password they entered, and compare that to the encrypted password that you stored. The National Institute of Standards and Technology (NIST) recommends PBKDF2 for passwords. bcrypt is a popular and established alternative, and scrypt is a relatively new algorithm that has been well-received. All these are popular for a reason: they're good. 

#### PBKDF2
Adjustable key stretching to defeat brute force attacks. The basic idea of key stretching is that after you apply your hashing algorithm to the password, you then continue to apply the same algorithm to the result many times (the iteration count). If hackers are trying to crack your passwords, this greatly increases the time it takes to try the billions of possible passwords. As mentioned previously, the slower, the better. PBKDF2 lets you specify the number of iterations to apply, allowing you to make it as slow as you like.

Part of Java SE 6. No additional libraries necessary. This is particularly attractive to those working in environments with restrictive open-source policies.
```java
import java.security.NoSuchAlgorithmException;
import java.security.SecureRandom;
import java.security.spec.InvalidKeySpecException;
import java.security.spec.KeySpec;
import java.util.Arrays;

import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.PBEKeySpec;

public class PasswordEncryptionService {

 public boolean authenticate(String attemptedPassword, byte[] encryptedPassword, byte[] salt)
   throws NoSuchAlgorithmException, InvalidKeySpecException {
  // Encrypt the clear-text password using the same salt that was used to
  // encrypt the original password
  byte[] encryptedAttemptedPassword = getEncryptedPassword(attemptedPassword, salt);

  // Authentication succeeds if encrypted password that the user entered
  // is equal to the stored hash
  return Arrays.equals(encryptedPassword, encryptedAttemptedPassword);
 }

 public byte[] getEncryptedPassword(String password, byte[] salt)
   throws NoSuchAlgorithmException, InvalidKeySpecException {
  // PBKDF2 with SHA-1 as the hashing algorithm. Note that the NIST
  // specifically names SHA-1 as an acceptable hashing algorithm for PBKDF2
  String algorithm = "PBKDF2WithHmacSHA1";
  // SHA-1 generates 160 bit hashes, so that's what makes sense here
  int derivedKeyLength = 160;
  // Pick an iteration count that works for you. The NIST recommends at
  // least 1,000 iterations:
  // http://csrc.nist.gov/publications/nistpubs/800-132/nist-sp800-132.pdf
  // iOS 4.x reportedly uses 10,000:
  // http://blog.crackpassword.com/2010/09/smartphone-forensics-cracking-blackberry-backup-passwords/
  int iterations = 20000;

  KeySpec spec = new PBEKeySpec(password.toCharArray(), salt, iterations, derivedKeyLength);

  SecretKeyFactory f = SecretKeyFactory.getInstance(algorithm);

  return f.generateSecret(spec).getEncoded();
 }

 public byte[] generateSalt() throws NoSuchAlgorithmException {
  // VERY important to use SecureRandom instead of just Random
  SecureRandom random = SecureRandom.getInstance("SHA1PRNG");

  // Generate a 8 byte (64 bit) salt as recommended by RSA PKCS5
  byte[] salt = new byte[8];
  random.nextBytes(salt);

  return salt;
 }
}
```
