```mermaid
classDiagram
    
    HOOFDQUERY: +splitsen()
  


```
HOOFDQUERY-->|sleutelvelden|SUBQUERY1;
  HOOFDQUERY-->|sleutelvelden|SUBQUERY2;
    SUBQUERY1-->|sleutelvelden|SUBQUERY1_2;
