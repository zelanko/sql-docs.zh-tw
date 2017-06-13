2. 所有叢集節點上，建立要儲存的 SQL Server 使用者名稱和密碼 Pacemaker 登入的檔案。 下列命令會建立並填入這個檔案：

   ```bash
   sudo touch /var/opt/mssql/secrets/passwd
   sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
   sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
   sudo chown root:root /var/opt/mssql/secrets/passwd 
   sudo chmod 600 /var/opt/mssql/secrets/passwd    
   ```

3. 所有叢集節點上，開啟 Pacemaker 防火牆連接埠。 若要使用 `firewalld` 開啟這些連接埠，請執行下列命令：

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 如果您使用其他防火牆，其中沒有內建的高可用性設定，您需要開啟下列連接埠，Pacemaker 才能與叢集中的其他節點通訊
   >
   > * TCP：連接埠 2224、3121、21064
   > * UDP：連接埠 5405

1. 在每個節點上安裝 Pacemaker 套件。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

   

2. 設定安裝 Pacemaker 和 Corosync 套件時建立的預設使用者密碼。 在所有節點上使用相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```

   

3. 啟用並啟動 `pcsd` 服務和 Pacemaker。 這將會允許節點在重新開機後重新加入叢集。 所有節點上執行下列命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 安裝 SQL Server 的 FCI 資源代理程式。 所有節點上執行下列命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```
