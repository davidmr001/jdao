  jdao��һ��java��������orm���߰���ͨ������������Զ�������֮��Ӧ��dao�ࡣ

һ��ʹ��DAO��ʽ�������ݣ�

��ѯSQL: select value,rowname from hstest where id between 2 and 10;
jdao����������£�
Hstest t = new Hstest();
t.where(Hstest.ID.BETWEEN(2, 10));
t.query(Hstest.VALUE, Hstest.ROWNAME);

����SQL:  insert into hstest (id,rowname,value) values(1,"donnie","wuxiaodong")
jdao����������£�
Hstest t = new Hstest();
t.setId(1);
t.setRowname("donnie");
t.setValue("wuxiaodong");
t.save();

��������SQL:  insert into hstest (id,rowname,value) values(1,"donnie1","wuxiaodong1"),(2,"donnie2","wuxiaodong2"),(3,"donnie3","wuxiaodong3")
jdao����������£�
Hstest t = new Hstest();
t.setId(1);
t.setRowname("donnie1");
t.setValue("wuxiaodong1");
t.addBatch();
t.setId(2);
t.setRowname("donnie2");
t.setValue("wuxiaodong2");
t.addBatch();
t.setId(3);
t.setRowname("donnie3");
t.setValue("wuxiaodong3");
t.addBatch();
t.batchForSave();

����SQL:  update hstest set rowname="wuxiaodong",value="wuxiaodong" where id=10
jdao����������£�
Hstest t = new Hstest();
t.setRowname("wuxiaodong");
t.setValue("wuxiaodong");
t.where(Hstest.ID.EQ(10));
t.update();

ɾ��SQL:  delete from hstest where id=2
jdao�����������:
Hstest t = new Hstest();
t.where(Hstest.ID.EQ(2));
t.delete();


����ʹ��QueryDao��ѯ����,�������ڸ���SQL��ѯ,������ɾ�Ĳ齨�黹��ʹ��DAO���������

QueryDao qd = new QueryDao(JdaoHandlerFactory.getDBHandler4c3p0(), "select id,rowname from hstest limit ?,?", 0, 10);
//��ȡ���ݷ�ʽһ
while (qd.hasNext()) {
    QueryDao q = qd.next();
    //��ȡ�ֶη�ʽһ
    System.out.println(q.fieldValue(1) + "   " + q.fieldValue(2));
    //��ȡ�ֶη�ʽ��
    System.out.println(q.fieldValue("id") + "   " + q.fieldValue("rowname"));
}
//��ȡ���ݷ�ʽ��
for(QueryDao q:qd.queryDaoList()){
    System.out.println(q.fieldValue(1) + "   " + q.fieldValue(2));
}