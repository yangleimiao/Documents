HashMap的容量、扩容

---

HashMap中与容量、扩容有关的成员变量：`size`、`loadFactor` 、`threshold` 、`DEFAULT_LOAD_FACTOR`和`DEFAULT_INITIAL_CAPACITY`；

`transient int size` ：记录Map中KV对的个数；

`loadFactor` ：装载因子，用来衡量HashMap满的程度，默认值0.75f（`static final float DEFAULT_LOAD_FACTOR = 0.75f;`）

`int threshold`：临界值