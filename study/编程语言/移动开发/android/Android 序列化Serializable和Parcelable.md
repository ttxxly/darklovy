## Serializable 和 Parcelable 的区别

可以肯定的是，两者都是支持序列化和反序列化的操作。

两者最大的区别在于 **存储媒介的不同**，`Serializable` 使用 **I/O 读写存储在硬盘上**，而 `Parcelable` 是直接 **在内存中读写**。很明显，内存的读写速度通常大于 IO 读写，所以在 Android 中传递数据优先选择 `Parcelable`。

`Serializable` 会使用反射，序列化和反序列化过程需要大量 I/O 操作， `Parcelable` 自已实现封送和解封（marshalled &unmarshalled）操作不需要用反射，数据也存放在 Native 内存中，效率要快很多。

有人直接比较过两个的效率差别

![nanchen](https://user-gold-cdn.xitu.io/2017/12/4/160207eda8e0abfe?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

我们可以来看看分别怎么写？

- **Serializable 「简单易用」一直都是它的代名词**

```
public class TestSerializable implements Serializable {
    String msg;
    
    List<ItemBean> datas;
    
    public static class ItemBean implements Serializable{
        String name;
    }
}
```

- **Parcelable 速度至上**

```
public class TestParcelable implements Parcelable {
    String msg;

    @Override
    public int describeContents() {
        return 0;
    }

    @Override
    public void writeToParcel(Parcel dest, int flags) {
        dest.writeString(this.msg);
    }

    TestParcelable(String msg) {
        this.msg = msg;
    }

    private TestParcelable(Parcel in) {
        this.msg = in.readString();
    }

    public static final Creator<TestParcelable> CREATOR = new Creator<TestParcelable>() {
        @Override
        public TestParcelable createFromParcel(Parcel source) {
            return new TestParcelable(source);
        }

        @Override
        public TestParcelable[] newArray(int size) {
            return new TestParcelable[size];
        }
    };
}
```

很明显，`Parcelable` 实现起来并不容易，它有成吨的模板代码，这使得对象变得难以阅读和维护。但如果你真的想成为一个优秀的 Android 开发工程师，你可能就得多在 `Parcelable` 上花点时间了。实在想偷懒也没事，因为有人在 GitHub 上已经上传了 Android Studio 的插件，帮助你自动生成这一堆模板。

地址：[github.com/mcharmas/an…](https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fmcharmas%2Fandroid-parcelable-intellij-plugin)

## 在两个 Activity 之间传递对象还需要注意什么呢？

**对象的大小，对象的大小，对象的大小！！！**

重要的事情说三遍，一定要注意对象的大小。`Intent` 中的 `Bundle` 是使用 `Binder` 机制进行数据传送的。能使用的 Binder 的缓冲区是有大小限制的（有些手机是 2 M），而一个进程默认有 16 个 `Binder` 线程，所以一个线程能占用的缓冲区就更小了（ 有人以前做过测试，大约一个线程可以占用 128 KB）。所以当你看到 `The Binder transaction failed because it was too large` 这类 `TransactionTooLargeException` 异常时，你应该知道怎么解决了。