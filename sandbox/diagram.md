```mermaid
graph TD;
    HOOFDQUERY-->|sleutelvelden|SUBQUERY1;
    HOOFDQUERY: +splitsen();
    HOOFDQUERY-->|sleutelvelden|SUBQUERY2;
    SUBQUERY1-->|sleutelvelden|SUBQUERY1_2;
```
