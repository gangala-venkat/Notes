## How to read build.gradle file in another build.gradle file.

Example Reading version from build.gradle file.

def props = new Properties()
file("${projectDir}/src/main/java/anyextraPath/build.gradle").withInputStream { props.load(it) }
def version= props.getProperty("version")?.replace("\"","")

Sample Encryption:

```
private object CryptoAES {
    private val encorder = Base64.getEncoder()
    private val decorder = Base64.getDecoder()
    private fun cipher(opmode: Int, secretKey: String): Cipher {
        val cipher = Cipher.getInstance("AES/CBC/PKCS5Padding")
        val sKey = SecretKeySpec(secretKey.toByteArray(Charsets.UTF_8), "AES")
        val ivParam = IvParameterSpec(secretKey.substring(0, 16).toByteArray(Charsets.UTF_8))
        cipher.init(opmode, sKey, ivParam)
        return cipher
    }

    fun encrypt(str: String, secretKey: String): String {
        val encrypted = cipher(Cipher.ENCRYPT_MODE, secretKey).doFinal(str.toByteArray(Charsets.UTF_8))
        return String(encorder.encode(encrypted))
    }

    fun decrypt(str: String, secretKey: String): String {
        val byteStr = decorder.decode(str.toByteArray(Charsets.UTF_8))
        return String(cipher(Cipher.DECRYPT_MODE, secretKey).doFinal(byteStr))
    }
} 
```


## how to read Properties from Propety file in kotlin :

```
@Suppress("UNCHECKED_CAST")
fun <T> getProp(key: String): T {
    val props  = javaClass.classLoader.getResourceAsStream("pairs_ids.txt").use {
        Properties().apply { load(it) }
    }
    return (props.getProperty(key) as T) ?: throw RuntimeException("could not find property $key")
}
```
