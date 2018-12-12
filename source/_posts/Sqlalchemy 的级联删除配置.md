---
title: Sqlalchemy 的级联删除配置
date: 2018-12-12 15:14:50
tags: sqlalchemy
---

```python
class BaseModel(Model):
    id = Column(Integer, primary_key=True)
    created_at = Column(DateTime(True), default=func.now(), nullable=False)
    updated_at = Column(DateTime(True), default=func.now(), onupdate=func.now(), nullable=False)

    @classmethod
    def create(cls, **kw):
        session = db.session
        if 'id' in kw:
            obj = session.query(cls).get(kw['id'])
            if obj:
                return obj
        obj = cls(**kw)
        session.add(obj)
        session.commit()
        return obj

    def to_dict(self):
        columns = self.__table__.columns.keys()
        return {key: getattr(self, key) for key in columns}


app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///../cnblogblog.db'

db = SQLAlchemy(app, model_class=BaseModel)


######################################################################################################

class Parent(db.Model):
    __tablename__ = 'parent'
    id = Column(Integer, primary_key=True)
    name = Column(String(20))


class Child(db.Model):
    __tablename__ = 'child'
    id = Column(Integer, primary_key=True)
    name = Column(String(20))

    parent_id = Column(Integer, ForeignKey('parent.id'))
    parent = relationship("Parent", backref=backref("child"))

    ###  只删除父级，子不影响
    # 1. parent_id = Column(Integer, ForeignKey('parent.id', ondelete="CASCADE"))
    #    parent = relationship("Parent", backref=backref("child", passive_deletes=True))

    ###  子级跟随删除
    # 2. parent = relationship("Parent", backref = backref("child", cascade="all, delete-orphan"))
    # 3. parent = relationship("Parent", backref = backref("child", cascade="all,delete"))

    ##  父级删除，子级不删除，外键更新为 null
    # 4. parent = relationship("Parent", backref = backref("child"))


if __name__ == '__main__':
    db.create_all()
    Parent.create(name='ZhangTian')
    Parent.create(name='LiTian')
    Child.create(name='ZhangDi', parent_id=1)
    Child.create(name='LiDi', parent_id=2)

    parent = db.session.query(Parent).first()
    db.session.delete(parent)
    db.session.commit()
    ```
```