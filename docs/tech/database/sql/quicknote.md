# 小抄速记

## WordPress删除垃圾评论

```
DELETE FROM wp_comments WHERE comment_approved = "trash";
DELETE FROM wp_comments WHERE comment_approved = "spam";
```

commentsmeta
```
SELECT * FROM wp_commentmeta WHERE comment_id NOT IN ( SELECT comment_id FROM wp_comments );
DELETE FROM wp_commentmeta WHERE comment_id NOT IN ( SELECT comment_id FROM wp_comments );
```

