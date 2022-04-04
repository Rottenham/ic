# BrainVsZombies 拦截计算器v1.1


## 使用说明
### 基础指令
    DE/PE/RE                - 设置场景
    wave                    - 查看当前波长，并显示巨人坐标范围
    wave [冰时机] [激活时机] - 设置冰时机、激活时机（冰时机可不填）
    hit (炮列数)              - 求正好全伤的落点（风炮需指定炮尾所在列）
    nohit (炮列数)            - 求正好不伤的落点（风炮需指定炮尾所在列）
    hit (炮列数) [延迟]       - 求延迟炮正好全伤的落点（风炮需指定炮尾所在列）
    nohit (炮列数) [延迟]     - 求延迟炮正好不伤的落点（风炮需指定炮尾所在列）
    delay (炮列数) [落点] [拦截行数] - 求最早、最晚拦截（尾炸）时机
        --程序会智能推测行数。默认前院/天台尾炸三行，后院尾炸两行。若不符，可自行输入拦截行数。
        --风炮需指定炮尾所在列

### 高级指令
    doom(r, c) - 表示用r行c列的核弹
    cob(r, c, (paoCol, paoRow))  - 表示发炮落点r行c列
        --屋顶场地需指定炮尾所在列；特殊落点需要指定炮所在行

    delay(xgInfo, rows, explodeInfo, isIced=False, exact=False) - 求最早/最晚拦截时机
        --为简化计算，计算时只考虑最左、最右巨人
        --可以单独使用minDelay或maxDelay；xgInfo接受单数也接受范围
            --例如，minDelay(806, [1, 2, 5, 6], doom(3, 3)) 表示1、2、5、6路原速巨人x坐标806，3-3核武最早何时能尾炸；delay([788, 806], [1, 2, 5, 6], doom(3, 3))则可以求出最早和最晚时机
        --如果认为结果有问题，请尝试将exact设为True（开销较大）；程序会遍历每个坐标的巨人并分别计算

    pos(iceTime, paoTime) - 输入冰时机、激活时机，求巨人坐标范围
        --可以输入多个冰时机，paoTime也可以大于2300。

    walk([walkTime1, walkTime2, ...]) - 输入行走时间，求巨人坐标范围（支持输入多段）
        --巨人举锤/投掷后相位会重置（受冰不会），需分多段输入。

    findMaxDelay(xgInfo, xgRows, dropRow, dropColRange, isIced=False, step=5, paoCol=None) - 求最大可能延迟的拦截落点（开销较大）
        --例如，findMaxDelay([788, 817], [2], 1, [8, 8.5]) 表示2路原速巨人x坐标范围[788~817]，炮落点1路[8~8.5]列，每5个px遍历一次，寻找最大可能延迟的拦截落点。
        --屋顶场地需指定炮尾所在列

### 原生函数
    judge(xgInfo, delay, xgRows, explodeInfo, isIced=False, verbosity=1) - 拦截计算
        --例如，judge([788, 817], 107, [1, 2, 5, 6], doom(3, 9)) 表示原速巨人x坐标范围[788~817]，延时107，只考虑1256行巨人，使用3-9核弹，计算是否可以全部拦截。因为可以全部拦截，故输出 True, []。

    iceKill(xgInfo, xgRows, isIced=True, verbosity=1) - 冰杀小鬼计算
        --例如，iceKill([734, 789], [3], True) 表示减速巨人x坐标范围[724~789]，只考虑3路巨人（实际上每一路都一样），计算冰冻全部小鬼的最早时机。
    --judge和iceKill都会给出一个AvgDamege，但这仅为平均值，实际伤害概率分布并不为此，仅可作为参考，不可视为伤害的期望值。

    注意：原生函数需要结合print()使用。

### 其他
    help        - 查看帮助
    helpfull    - 查看详细帮助
    version     - 查看版本
    quit/exit   - 退出
    
## 关于作者
BrainVsZombies General Interception Calculator ver 1.1 by Elovi, Crescendo
