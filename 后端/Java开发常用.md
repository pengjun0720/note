# Java开发常用

## 获取post 参数为JSON.stringify后的参数

https://blog.csdn.net/qq_25475445/article/details/82896367

## lamda表达式

```java
public List<SysDept> queryAllParentDeptByDeptIdAndLevel(Long deptId, String nodeFlag) {
    int nodeLevel = 0;
    SysDept sysDept = deptMapper.selectDeptById(deptId);
    // 获取当前部门所有的父级节点
    List<String> deptIdList = Arrays.stream(sysDept.getAncestors().split(",")).collect(Collectors.toList());
    // 移除0节点
    deptIdList.remove("0");
    // 添加当前节点
    deptIdList.add(deptId.toString());
    // 根据ids查询部门列表
    List<SysDept> allDeptList = deptMapper.queryAllByIds(deptIdList);
    allDeptList.forEach(dept -> {
        int length = dept.getAncestors().split(",").length;
        dept.setNodeLevel(length);
    });
    // 根据节点标志值确定返回的节点层级
    for (SysDept dept : allDeptList) {
        if (nodeFlag.equals(dept.getNodeFlag())) {
            nodeLevel = dept.getNodeLevel();
            break;
        }
    }
    // 根据节点层级排序
    allDeptList.sort(Comparator.comparingInt(SysDept::getNodeLevel));
    // 复制
    int finalNodeLevel = nodeLevel;
    // 筛选出所有符合条件的节点对象
    return allDeptList.stream().filter(dept -> dept.getNodeLevel() >= finalNodeLevel).collect(Collectors.toList());
}
```

`Comparator.comparingInt(SysDept::getNodeLevel)` 等于 `(o1, o2) -> o1.getNodeLevel() - o2.getNodeLevel()`

## linux启动springboot jar

> 根据应用获取已经启动的pid，如果没有则启动程序，如果有则关闭程序。并在屏幕输入红色字体提示。

```bash
#!/bin/bash
# 获取java进程id
pid=`ps -ef | grep jsdye.jar |grep -v grep |head -n 1 | awk '{print $2}'`;
# 判断是否启动
if [ "$pid" == "" ]; then
	# 启动程序并将日志输入到jsdye.log中
	echo -e "\033[31m jsdye.jar 正在启动 \033[0m"
	nohup java -jar /data/programs/jsdye.jar >> /data/programs/jsdye.log 2>&1 &
	# 查看日志
	tail -f ./jsdye.log
else
	# 杀掉进程
	kill -9 $pid
fi
echo -e "\033[31m jsdye.jar jsdye.jar 已关闭 \033[0m"

```

