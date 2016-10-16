# MIS
>ER图
![查询](https://github.com/masery09143521/MIS/blob/master/ER%E5%9B%BE.png)
>1.查询设备保养情况
SELECT 设备.设备ID, 设备类型.设备类型, 保养记录.保养ID, 保养记录.保养项目, 保养记录.保养内容, 保养消耗.保养消耗, 保养消耗.单位, 保养记录.保养时间, 保养记录.保养人FROM (((保养记录 INNER JOIN 保养项目 ON 保养记录.保养项目 = 保养项目.保养项目) INNER JOIN 保养消耗 ON 保养项目.保养项目 = 保养消耗.保养项目) INNER JOIN 设备 ON 保养记录.设备ID = 设备.设备ID) INNER JOIN 设备类型 ON 保养记录.设备ID = 设备类型.设备IDWHERE (((设备.设备ID)=[情输入设备号]));
![查询](https://github.com/masery09143521/MIS/blob/master/%E6%9F%A5%E8%AF%A2%E6%A3%80%E4%BF%AE%E6%8A%A5%E5%91%8A.png)
![查询](https://github.com/masery09143521/MIS/blob/master/%E6%9F%A5%E8%AF%A2%E6%8A%A5%E5%91%8A%E7%BB%93%E6%9E%9C.png)
>2.提前一天预警
SELECT 设备.设备ID, 设备类型.设备类型, 设备类型.保养周期, 设备.设备名FROM 设备类型, (设备 INNER JOIN 保养记录 ON 设备.设备ID = 保养记录.设备ID) INNER JOIN 保养项目 ON 保养记录.保养项目 = 保养项目.保养项目WHERE (((Date()-[保养时间]+1)=[保养周期]));
![查询]（images/预警.png）
