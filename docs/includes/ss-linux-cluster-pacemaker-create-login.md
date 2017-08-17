1. **在所有 SQL Server 上，為 Pacemaker 建立 Server 登入**。 下列 Transact-SQL 會建立登入：

   ```Transact-SQL
   USE [master]
   GO
   CREATE LOGIN [pacemakerLogin] with PASSWORD= N'ComplexP@$$w0rd!'
    
   ALTER SERVER ROLE [sysadmin] ADD MEMBER [pacemakerLogin]
   ```

   或者，您可以以更細微的層級設定權限。 Pacemaker 登入需要 ALTER、CONTROL 和 VIEW DEFINITION 權限才能管理可用性群組，而且登入需要 VIEW SERVER STATE 才能執行 sp_server_diagnostics。 如需詳細資訊，請參閱[GRANT Availability Group Permissions (Transact-SQL)](http://msdn.microsoft.com/library/hh968934.aspx) (授與可用性群組權限 (Transact-SQL)) 和 [sp_server_diagnostic 權限](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql#permissions)。

   下列 Transact-SQL 只會將必要權限授與 Pacemaker 登入。 在下列陳述式中，'ag1' 是將加入為叢集資源的可用性群組名稱。

   ```Transact-SQL
   GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO pacemakerLogin
   GRANT VIEW SERVER STATE TO pacemakerLogin
   ```

1. **在所有 SQL 伺服器上，儲存 SQL Server 登入的認證**。

   ```bash
   echo 'pacemakerLogin' >> ~/pacemaker-passwd
   echo 'ComplexP@$$w0rd!' >> ~/pacemaker-passwd
   sudo mv ~/pacemaker-passwd /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd
   sudo chmod 400 /var/opt/mssql/secrets/passwd # Only readable by root
   ```
