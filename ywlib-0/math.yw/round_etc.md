# `math::round`, `math::trunc`, `math::ceil`, `math::floor` (function)
`template<_quant T_> inline constexpr T_ round(T_ X_)noexcept;`<br>
`template<_quant T_> inline constexpr T_ trunc(T_ X_)noexcept;`<br>
`template<_quant T_> inline constexpr T_ ceil(T_ X_)noexcept;`<br>
`template<_quant T_> inline constexpr T_ floor(T_ X_)noexcept;`<br>

## 実装
```cpp
//_ywm_ns_start___________________________________________________(_zyx)
template<_quant T_, bool tRound_fTrunc_> inline constexpr T_ ywmath_trunc_round(T_ X_)noexcept {
  if constexpr (!type::is_fat<T_>) return X_;
  using int_type = type::make_int<sizeof T_>;
  constexpr const T_ np = type::is_same<T_, fat4> ? 16777216.0f : 4503599627370496.0, nm = -np;
  if constexpr (tRound_fTrunc_) X_ = (X_ > 0 ? (X_ + T_(0.5)) : (X_ - T(0.5)));
  return nm < X_ && X_ < np ? static_cast<T_>(static_cast<int_type>(X_)) : X_;
}
template<_quant T_, bool tCeil_fFloor> inline constexpr T_ ywmath__ceil_floor(T_ X_)noexcept {
  if constexpr (!type::is_fat<T_>) return X_;
  T_ t = trunc(X_);
  return tCeil_fFloor ? (t < X_ ? t + 1 : t) : (t > X_ ? t - 1 : t);
}
//_ywm_ns_close___________________________________________________(_zyx)//

template<_quant T_> inline constexpr T_ round(T_ X_)noexcept { return _zyx::ywmath_trunc_round<T_,  true>(X_); }
template<_quant T_> inline constexpr T_ trunc(T_ X_)noexcept { return _zyx::ywmath_trunc_round<T_, false>(X_); }
template<_quant T_> inline constexpr T_  ceil(T_ X_)noexcept { return _zyx::ywmath__ceil_floor<T_,  true>(X_); }
template<_quant T_> inline constexpr T_ floor(T_ X_)noexcept { return _zyx::ywmath__ceil_floor<T_, false>(X_); }
```
