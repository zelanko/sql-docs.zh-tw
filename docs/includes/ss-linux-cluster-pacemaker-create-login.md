1. **在所有 SQL Server 上，為 Pacemaker 建立 Server 登入**。 下列 Transact-SQL 會建立登入：

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

  建立可用性群組時，在其建立之後但在新增任何節點之前，Pacemaker 使用者需要可用性群組的 ALTER、CONTROL 和 VIEW DEFINITION 權限。

1. **在所有 SQL 伺服器上，儲存 SQL Server 登入的認證**。

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
