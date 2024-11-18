```java
Dept repeatFullNameDetp = this.getOne(Wrappers.<Dept>query().lambda()  
        .eq(Dept::getParentId, 0)  
        .and(wrapper -> wrapper.eq(Dept::getDeptName, dept.getDeptName())  
                .or().eq(Dept::getSort, dept.getSort())  
                .or().eq(Dept::getFullName, dept.getFullName())));
```