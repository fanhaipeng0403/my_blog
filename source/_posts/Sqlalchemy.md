---
title: Sqlalchemy
date: 2017-04-02 08:56:04
tags: sqlalchemy
---


# 简单查询
    print(session.query(User).all())
    print(session.query(User.name, User.fullname).all())
    print(session.query(User, User.name).all())
    
# 带条件查询
    print(session.query(User).filter_by(name='user1').all())
    print(session.query(User).filter(User.name == "user").all())
    print(session.query(User).filter(User.name.like("user%")).all())
    
# 多条件查询
    print(session.query(User).filter(and_(User.name.like("user%"), User.fullname.like("first%"))).all())
    print(session.query(User).filter(or_(User.name.like("user%"), User.password != None)).all())
    
# sql过滤
    print(session.query(User).filter("id>:id").params(id=1).all())
    
# 关联查询 
    print(session.query(User, Address).filter(User.id == Address.user_id).all())
    print(session.query(User).join(User.addresses).all())
    print(session.query(User).outerjoin(User.addresses).all())
    
# 聚合查询
    print(session.query(User.name, func.count('*').label("user_count")).group_by(User.name).all())
    print(session.query(User.name, func.sum(User.id).label("user_id_sum")).group_by(User.name).all())
    
# 子查询
    stmt = session.query(Address.user_id, func.count('*').label("address_count")).group_by(Address.user_id).subquery()
    print(session.query(User, stmt.c.address_count).outerjoin((stmt, User.id == stmt.c.user_id)).order_by(User.id).all())
    
# exists
    print(session.query(User).filter(exists().where(Address.user_id == User.id)))
    print(session.query(User).filter(User.addresses.any()))
    --deals=交易表，areas=地域表，例如香港；我们的目的：查看有交易的地域

select * from areas where id in (select city_id from deals);

select * from areas where id in   (select city_id from deals where deals.city_id = areas.id);

select * from areas where exists (select null     from deals where deals.city_id = areas.id);

区别：
EXISTS语法并没有说哪个字段落在了子查寻的结果中，而是说exists后面的语句执行的结果是不是有记录，只要有记录，则主查询语句就成立。它代表‘存在’，用来引领嵌套查询的子查询，它不返回任何数据，只产生逻辑真值‘true’与逻辑假值‘False’。由EXISTS引出的子查询，其目标列表达式通常都用*（用null也可以），因为带有EXISTS的子查询只返回真值或假值，给出列名没有实际意义


# 限制返回字段查询
person = session.query(Person.name, Person.created_at,                     
             Person.updated_at).filter_by(name="zhongwei").order_by(            
             Person.created_at).first()



# 记录总数查询：

from sqlalchemy import func

# count User records, without
# using a subquery.
session.query(func.count(User.id))

# return count of user "id" grouped
# by "name"
session.query(func.count(User.id)).\
        group_by(User.name)

from sqlalchemy import distinct

# count distinct "name" values
session.query(func.count(distinct(User.name)))




