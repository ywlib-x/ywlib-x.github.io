# math::abs (function)
`template<_quant T_> inline constexpr T_ abs(T_ V_)noexcept;`

## 前提
[`_quant`](../type.yw/_quant.md)

## 実装
```cpp
template<_quant T_> inline constexpr T_ abs(T_ X_)noexcept { return V_ < X_() ? -X_ : X_; }
```
