1. **在這兩個叢集節點上，建立檔案以儲存 SQL Server 使用者名稱和密碼，以供 Pacemaker 登入使用**。 下列命令會建立並填入這個檔案：

    ```bash
    sudo touch /var/opt/mssql/secrets/passwd
    sudo echo '<loginName>' >> /var/opt/mssql/secrets/passwd
    sudo echo '<loginPassword>' >> /var/opt/mssql/secrets/passwd
    sudo chown root:root /var/opt/mssql/secrets/passwd 
    sudo chmod 600 /var/opt/mssql/secrets/passwd
    ```
2. **所有叢集節點都必須能夠透過 SSH 互相存取**。 hb_report 或 crm_report 之類的工具 (用於疑難排解) 和 Hawk 的 History Explorer 都要求節點之間的無密碼 SSH 存取，否則它們只能從目前的節點收集資料。 如果您使用非標準 SSH 連接埠，請使用 -X 選項 (請參閱 man 頁面)。 例如，如果您的 SSH 連接埠是 3479，則以下列方式叫用 hb_report：

    ```bash
    crm_report -X "-p 3479" [...]
    ```

    如需詳細資訊，請參閱 [SUSE 文件中的系統需求和建議 (英文)](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_requirements_other.html)。

3. **安裝高可用性延伸模組**。 若要安裝延伸模組，請依照下列 SUSE 主題中的步驟執行：
    
    [安裝和設定快速入門 (英文)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html)

4. **安裝 SQL Server 的 FCI 資源代理程式**。 在這兩個節點上執行下列命令：

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server.repo
    sudo zypper --gpg-auto-import-keys refresh
    sudo zypper install mssql-server-ha
    ```

5. **自動設定第一個節點**。 下一個步驟是透過設定第一個節點 SLES1，以設定執行單節點的叢集。 依照 SUSE 主題[設定第一個節點 (英文)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node) 中的指示執行。

    完成時，使用 `crm status` 檢查叢集狀態：
    ```bash
    crm status
    ```

    這應該會顯示已設定一個節點 (SLES1)。

6. **將節點加入現有叢集**。 接下來，將 SLES2 節點加入至叢集。 依照 SUSE 主題[加入第二個節點 (英文)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.2nd-node) 中的指示執行。
    
    完成時，使用 **crm status** 來檢查叢集狀態。 如果您已成功加入第二個節點，則輸出將如下所示︰
        
    ```
    2 nodes configured
    1 resource configured
    Online: [ SLES1 SLES2 ]
    Full list of resources:
    admin_addr     (ocf::heartbeat:IPaddr2):       Started SLES1
    ```

    > [!NOTE]
    > **admin_addr** 是虛擬 IP 叢集資源，它是在初始單節點叢集設定期間所設定。

7.    **移除程序**。 如果您需要從叢集移除節點，請使用 **ha-cluster-remove** 啟動程序指令碼。 如需詳細資訊，請參閱[啟動程序指令碼概觀 (英文)](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.bootstrap)。  

