# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_152940.jpg
- R5 mid MISSING
- R6 mid MISSING
## adasind_167700.jpg
- L6 mid IGNORE_SCOPE
- L2 mid SPURIOUS
- L3+R5 center BOX_GEOMETRY
- L5+R3 mid WRONG_CLASS
- L7+R4 center WRONG_CLASS
- R1 center MISSING
- R2 mid MISSING
- R8 center MISSING
- R9 mid MISSING
## adasind_212280.jpg
- L2+R3 edge WRONG_CLASS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 10 | 6 | 4 | 2 |
| mid | 6 | 1 | 5 | 2 |
| edge | 2 | 1 | 1 | 1 |
