# _quant (concept)
`template<typename T_> concept _quant;`

## 前提
[`constant type::is_quant<T>`](../type.yw/is_quant)<br>

## 実装
```cpp
template<typename T_> concept _quant = type::is_quant<T_>;
```

## 経緯
* quantはquantity(量)に由来し、このconceptは`intx`, `natx`, `fatx`で構成される。<br>
  (`fatx`の有無で対称的な[`_count`](../_count.md)と文字数と文字の韻を揃えている)
* template関数の引数に使用できる型を限定する目的で、特に[`<math.yw>`](../../math.md)において多用している。
