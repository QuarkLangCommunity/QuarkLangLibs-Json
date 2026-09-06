# QuarkLangLibs-Json

**QuarkLang 官方库（json）——JSON 序列化/反序列化，官方认证。**

调用方法对标 Python 的 `json` 模块：`json::dumps(...)` / `json::loads(...)`。

## 使用方法

把 `json.qk` 放在与你的源码同目录：

```qk
import "json";

fn main(io IOStream) {
    h HashTable<String, String> = HashTable::new();
    h.put("name", "QuarkLang");
    h.put("version", "0.2");

    // 任意值 -> JSON 字符串（Python: json.dumps）
    s String = json::dumps(h);
    io.println(s);                       // {"name":"QuarkLang","version":"0.2"}

    // JSON -> 值（Python: json.loads）；对象->HashTable、数组->List、整数->int
    back HashTable<String, String> = json::loads(s);
    io.println(back.get("name"));        // QuarkLang

    l List<int> = [1, 2, 3];
    io.println(json::dumps(l));          // [1,2,3]
}
```

## API

| 函数 | 签名 | 说明 |
|---|---|---|
| `dumps` | `(v interface{}) String` | 任意值 → JSON 字符串（对象/数组/标量/嵌套均可） |
| `loads` | `(s String) interface{}` | JSON → 值：对象→`HashTable`，数组→`List`，字符串→`String`，整数→`int`，小数→`float`，布尔→`bool`；非法输入报 `JSONError` |

## 类型映射（与 Python json 对齐）

| JSON | QuarkLang |
|---|---|
| object | `HashTable<String, T>` |
| array | `List<T>` |
| string / number(int) / number(float) / true / false / null | `String` / `int` / `float` / `bool` / `null` |

## 认证信息

- 库名：`json`（`import "json"`）
- 语言版本：QuarkLang v0.2（`space`/`interface{}`/`HashTable`/`List` 体系）
- 运行时版本：见 QuarkLang 主仓库 `compiler/main.go` 的 `engineVersion`
- 认证方：QuarkLang 官方项目

> 官方库=认证；实现原语（`qkjson_dumps`/`qkjson_loads`）在 QuarkLang 运行时内部。
