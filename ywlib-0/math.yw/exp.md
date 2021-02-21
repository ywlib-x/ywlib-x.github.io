# math::exp
`template<_quant T_> inline constexpr ret_type_fat<T_> exp(T_ X_)noexcept`

## 前提

[`concept _quant`](../../concept.yw/_quant.md)<br>
[`typename math::ret_type_fat`](../ret_type_fat.md)<br>
[`function math::round`](../round.md)<br>
[`function _zyx::ywmath_pown`](../ywmath_powi.md)<br>
[`function math::abs`](../abs.md)<br>
[`class type::props`](../../utility/props.md)<br>
[`function math::factorial_inv`](../factorial_inv.md)<br>
[`constant type::is_same`](../../type.yw/is_same)<br>

## 実装

```cpp
template<_quant T_> inline constexpr ret_type_fat<T_> exp(T_ X_)noexcept
{
  intt a = round(X_);
  fat8 b = static_cast<fat8>(X_ - a);
  if (b == 0.) return _zyx::ywmath_powi(math::c_e, a);
  fat8 c(b), d(1. + c), e(1.);
  for (natt i = 2; abs(d - e) > type::props<ret_type_quant<T_>>::epsilon; ++i) {
    d = (e = d) + (c *= b) * factorial_inv(i);
  }
  b = _zyx::ywmath_powi(math::c_e, a) * d;
  return type::is_same<T_, fat4> ? static_cast<fat4>(b) : b;
}
```
