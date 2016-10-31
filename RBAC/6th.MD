##查询用户test1可以查看的页面（Sys_menu）
SELECT CF_User.LoginName, CF_Privilege.PrivilegeMasterKey, CF_Privilege.PrivilegeAccess, CF_Privilege.PrivilegeAccessKey, CF_Privilege.PrivilegeOperation, Sys_Menu.MenuName
FROM (CF_Privilege INNER JOIN Sys_Menu ON CF_Privilege.PrivilegeAccessKey = Sys_Menu.MenuID) INNER JOIN ((CF_UserRole INNER JOIN CF_User ON CF_UserRole.UserID = CF_User.UserID) INNER JOIN CF_Role ON CF_UserRole.RoleID = CF_Role.RoleID) ON CF_Privilege.PrivilegeMasterKey = CF_Role.RoleID
WHERE (((CF_User.LoginName)="test1") AND ((CF_Privilege.PrivilegeAccess)="Sys_Menu") AND ((CF_Privilege.PrivilegeOperation)="permit"));
##截图
![image]()
