# python-for-mysql-learn

python使用slect获取mysql的数据并遍历
import MySQLdb
import sys

conn=MySQLdb.connect(host='133.***.***.106',user='root',passwd='*******',db='*pos_lte_V3',port=5031)
with conn:
    cur=conn.cursor()
    cur.execute("SELECT mme_sgw,COUNT(*) from s1_common_xdr_201603180000 where (start_date_time BETWEEN '2016-03-18 09:00:00' and '2016-03-18 09:10:00') and tac in(30692,30693) GROUP BY mme_sgw HAVING mme_sgw LIKE'NNMME%'")
    numrows=int(cur.rowcount)
    for i in range(numrows):
        row=cur.fetchone()
        print row[0],row[1]

    cur.close()
    conn.close()
    
numrows = int(cur.rowcount)用于获取结果集的数目
row = cur.fetchone()每次取出一行数据，同时记录集的指针执行下一行

