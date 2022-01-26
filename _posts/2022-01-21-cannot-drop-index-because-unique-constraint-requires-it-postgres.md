---
layout: post
category: etc
---

# 문제

Datagrip에서 `stock_move_line_lot_name_uniq`(lot_name에 unique 제약 조건)을 강제로 삭제하려고 하니, 오류가 발생하며 삭제되지 않았다.

![](/no-access-please/assets/image/2022-01-21-cannot-drop-index-because-unique-constraint-requires-it-postgres/1.png)

# 해결

아래와 같이 쿼리를 작성해 실행하면, `stock_move_line_lot_name_uniq`을 강제로 삭제할 수 있다.

```sql
DO
$$BEGIN
   ALTER TABLE <table_name> DROP CONSTRAINT <unique_name>;
EXCEPTION
   WHEN undefined_object
      THEN NULL;  -- ignore the error
END$$;
```


# 참고

[https://stackoverflow.com/questions/57754479/cannot-drop-index-because-unique-constraint-requires-it-postgres](https://stackoverflow.com/questions/57754479/cannot-drop-index-because-unique-constraint-requires-it-postgres){:target="_blank"}
