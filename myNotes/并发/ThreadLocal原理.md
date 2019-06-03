每个Thread里都保存了一个ThreadLocal.ThreadLocalMap类型的threadLocals变量，以ThreadLocal<T>对象作为key，以T类型的对象作为value。
使用ThreadLocal时候，先调用get()方法获取，get()方法![T get()方法](https://upload-images.jianshu.io/upload_images/13572633-ebb70ef40b0f8fdf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
先获取保存在Thread对象的ThreadLocalMap对象，再以当前ThreadLocal<T>对象为key获取ThreadLocalMap.Entry对象，进一步获取对应value。
如果map为空，或者是Entry为空，则调用 setInitialValue方法。
![T setInitialValue()方法](https://upload-images.jianshu.io/upload_images/13572633-91132bc8175cd168.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
setInitialValue方法会先调用initialValue方法，需要在初始化ThreadLocal时重写该方法，如果不重写该方法，则应该在调用get前调用set方法。
![set()方法](https://upload-images.jianshu.io/upload_images/13572633-656c6a07a310a60f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如果不调用set()方法，则返回的value为null。
![ThreadLocal的 initialValue()方法](https://upload-images.jianshu.io/upload_images/13572633-6e4fd79cb2267101.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
