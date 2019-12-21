# Mybatis注意事项

1.  <![CDATA[ when min(starttime)<='12:00' and max(endtime)<='12:00' ]]> 
2.  使用转义字符

```mybatis
第一种：用了转义字符把>和<替换掉
SELECT * FROM test WHERE 1 = 1 AND start_date  <= CURRENT_DATE AND end_date >= CURRENT_DATE
附：XML转义字符


转义符号(转义符号前加上&)     			原始符号					说明
lt;										<						小于号
gt;										>						大于号
amp;									&						和
apos;									‘						单引号
quot;									“						双引号

```



###开启慢sql查询