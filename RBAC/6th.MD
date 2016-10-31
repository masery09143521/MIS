##查询用户test1可以查看的页面（Sys_menu）
###SQL语句
&emsp;&emsp;SELECT CF_User.LoginName, CF_Privilege.PrivilegeMasterKey, CF_Privilege.PrivilegeAccess, CF_Privilege.PrivilegeAccessKey, &emsp;&emsp;CF_Privilege.PrivilegeOperation, Sys_Menu.MenuName
&emsp;&emsp;FROM (CF_Privilege INNER JOIN Sys_Menu ON CF_Privilege.PrivilegeAccessKey = Sys_Menu.MenuID) INNER JOIN ((CF_UserRole INNER JOIN &emsp;&emsp;CF_User ON CF_UserRole.UserID = CF_User.UserID) INNER JOIN CF_Role ON CF_UserRole.RoleID = CF_Role.RoleID) ON &emsp;&emsp;CF_Privilege.PrivilegeMasterKey = CF_Role.RoleID
&emsp;&emsp;WHERE (((CF_User.LoginName)="test1") AND ((CF_Privilege.PrivilegeAccess)="Sys_Menu") AND &emsp;&emsp;((CF_Privilege.PrivilegeOperation)="permit"));
###截图
![image](https://github.com/masery09143521/MIS/blob/master/RBAC/1.png)
###伪代码
1、根据登录名"test1"查找对应编号UserID
&emsp;&emsp;2、根据UserID在user_role表查找改人员所对应的角色RoleID
&emsp;&emsp;3、CF_Privilege表连接CF_Role表并查找对应角色
  &emsp;&emsp; PrivilegeMasterKey=RoleID 
  &emsp;&emsp; CF_Privilege表连接Sys_Menu表并查找对应菜单
  &emsp;&emsp; PrivilegeAccessKey=MenuID
  &emsp;&emsp;并且 权限属性为Permit   并且   权限为Sys_Menu的数据
  
##对订单(order)页面中的操作权限(sys_button)
###SQL语句
SELECT CF_User.LoginName, Sys_Menu.MenuName, CF_Privilege.PrivilegeAccess, Sys_Button.BtnName
&emsp;&emsp;FROM ((CF_Privilege INNER JOIN ((CF_UserRole INNER JOIN CF_Role ON CF_UserRole.RoleID = CF_Role.RoleID) INNER JOIN CF_User ON &emsp;&emsp;CF_UserRole.UserID = CF_User.UserID) ON CF_Privilege.PrivilegeMasterKey = CF_Role.RoleID) INNER JOIN Sys_Menu ON &emsp;&emsp;CF_Privilege.PrivilegeAccessKey = Sys_Menu.MenuID) INNER JOIN Sys_Button ON Sys_Menu.MenuNo = Sys_Button.MenuNo
&emsp;&emsp;WHERE (((CF_User.LoginName)="test1") AND ((Sys_Menu.MenuName)="订单"));
###截图
![image](https://github.com/masery09143521/MIS/blob/master/RBAC/2.png)
###伪代码
1、根据登录名称查找人员编号UserID
&emsp;&emsp;2、根据UserID在user_role表查找改人员所对应的角色RoleID
&emsp;&emsp;3、CF_Privilege表连接CF_Role表并查找对应角色
 &emsp;&emsp;  PrivilegeMasterKey=RoleID 
 &emsp;&emsp;  CF_Privilege表连接Sys_Menu表并查找对应菜单
 &emsp;&emsp;  PrivilegeAccessKey=MenuID
 &emsp;&emsp;  Sys_Menu表连接Sys_Button表并查找对应按钮
 &emsp;&emsp; 并且 权限属性为Permit 并且 菜单类型为"订单"的数据
