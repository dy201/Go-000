# 题目
我们在数据库操作的时候，比如 dao 层中当遇到一个 `sql.ErrNoRows` 的时候，是否应该 `Wrap`这个 `error`，抛给上层。为什么，应该怎么做请写出代码？

# 分析
不应该。该错误是查询不到结果，上层不需要该错误的堆栈信息，所以不需要 Wrap，而是直接抛给上层。
# 代码

## dao 层
```go
type Dao struct{
    db *DB
}

func NewDao() *Dao {
    return &Dao{ db : &DB{...}}
}

func(d *Dao) QueryList() ([]User,error){
    data,err := d.db.query("select * from table ...")
    if err != nil {
        if errors.Is(sql.ErrNoRows){
            return nil, errors.New("query users errors: " + sql.ErrNoRows.Error())
        }
        return errors.Wrap(err,"query users errors")
    }
    return data,err
}
```

## service层
```go
type Service struct{ 
    dao *Dao
}

func NewService(){
    dao := NewDao()
    return &Service{dao:dao}
}

func (s *Service) QueryList ([]User,error){
    return s.dao.QueryList()
}
```

## main

```go
func main(){
    service := NewService()
    data,err := service.QueryList()
    if err != nil {
        return
    }
    fmt.Printf("user data: %v",data)
}
```


[参考作业1](https://github.com/fizzse/Go-000/tree/main/Week02)

[参考作业2](https://github.com/weiluoliang/Go-000/tree/main/Week02)

[参考作业3](https://github.com/labazhang/Go-000/tree/main/Week02)

[提交地址](https://github.com/Go-000/Go-000/issues/8)