
3. 在這兩個叢集節點上，開啟 Pacemaker 防火牆連接埠。 若要使用 `firewalld` 開啟這些連接埠，請執行下列命令：

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

   

2. 設定安裝 Pacemaker 和 Corosync 套件時建立的預設使用者密碼。 在這兩個節點上使用相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```

   

3. 啟用並啟動 `pcsd` 服務和 Pacemaker。 這將會允許節點在重新開機後重新加入叢集。 在這兩個節點上執行下列命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 建立叢集。 若要建立叢集，請執行下列命令︰

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >如果您先前已在相同節點上設定叢集，執行 'pcs cluster setup' 時需要使用 '--force' 選項。 請注意，這相當於執行 'pcs cluster destroy'，而且需要使用 'sudo systemctl enable pacemaker' 來重新啟用 Pacemaker 服務。

5. 安裝 SQL Server 的 SQL Server 資源代理程式。 在這兩個節點上執行下列命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```
