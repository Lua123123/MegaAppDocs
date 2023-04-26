# Function interact between MegaApp with Native App through SDK (middleware) and return data Json String? to 3th through SDK
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
//Get method corresponding to params called from SDK
val mt = this@MiniAppGatewaySDK::class.java.getMethod(method, *(params.toTypedArray()))
//Call method with params called from SDK and return data to SDK
val result = mt.invoke(this@MiniAppGatewaySDK, *(list.toTypedArray())) as? String
//For example
debug webview with chrome devices: [chrome://inspect/devices#devices](url)
