## Function interact between MegaApp with Native App through SDK (middleware) and return data Json String? to 3th through SDK
```kotlin
    @JavascriptInterface
    fun reflectFunction(method: String, args: String): String? {
        try {
            val jsonArrayArgument = JSONArray(args)
            val params = arrayListOf<Class<*>>()

            val list = mutableListOf<Any>()
            for (item in 0 until jsonArrayArgument.length()) {
                params.add(jsonArrayArgument.get(item).javaClass)
                list.add(jsonArrayArgument[item])
            }

            val mt = this@MiniAppGatewaySDK::class.java.getMethod(method, *(params.toTypedArray()))
            val result = mt.invoke(this@MiniAppGatewaySDK, *(list.toTypedArray())) as? String

            // package

            return result

        } catch (e: Exception) {
            e.printStackTrace()
            return callback?.error()
        }
    }
```
#### Get method corresponding to params called from SDK
```comment
    val mt = this@MiniAppGatewaySDK::class.java.getMethod(method, *(params.toTypedArray()))
```
#### Call method with params called from SDK and return data to SDK
```comment
    val result = mt.invoke(this@MiniAppGatewaySDK, *(list.toTypedArray())) as? String
```
#### For example
```comment
    I have the function "getVodDetail(id: String)", I'm going to call on chrome devices: megaSdk.reflectFunction("getVodDetail", '["61f4f512b22e44fefc5979c0"'])
    with "getVodDetail" is the name function you want to call, and "61f4f512b22e44fefc5979c0" is the params you push into.   
    Debug webview with chrome devices: [chrome://inspect/devices#devices](url)
```
## RULE
![image](https://user-images.githubusercontent.com/88249324/235056155-8b1ae4db-4598-4ecb-89e9-39abe5264910.png)

