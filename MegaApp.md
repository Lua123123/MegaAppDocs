# Function interact between MegaApp with Native App through SDK
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
