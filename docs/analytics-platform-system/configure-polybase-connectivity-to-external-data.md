---
title: "設定 PolyBase 連線到外部資料 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f14ac21-a086-4c05-861f-0a12bf278259
caps.latest.revision: 
ms.openlocfilehash: d9777fb2bbfd9af2598a422fc072877ff0b78959
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2018
---
# <a name="configure-polybase-connectivity-to-external-data"></a>設定外部資料的 PolyBase 連線組態
說明如何在 SQL Server PDW 連接到外部 Hadoop 或 Microsoft Azure 儲存體 blob 資料來源中設定 PolyBase。 使用 PolyBase 來執行用來整合多個來源資料，包括 Hadoop、 Azure blob 儲存體，以及 SQL Server PDW 查詢。  
  
### <a name="to-configure-connectivity"></a>若要設定連線  
  
1.  開啟查詢工具，例如 sqlcmd 或 SQL Server Data Tools (SSDT)，然後執行 sp_configure 來檢視目前 'hadoop connectivity' 的設定。  
  
    ![hadoop 連接性設定](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  決定您的設定以及您是否需要變更目前的設定需要的 Hadoop 連接。 此選項適用於整個 SQL Server PDW 區域。 如需的組態設定和版本的完整清單，請參閱[sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
3.  若要變更的 'hadoop connectivity' 的設定，請使用 RECONFIGURE 執行 sp_configure。 以下是一些範例。  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP), HDInsight on Analytics Platform System, or HDInsight’s Microsoft Azure blob storage  
    EXEC sp_configure 'hadoop connectivity', 4;   
    RECONFIGURE;  
  
    -- Enable connectivity to Hortonworks Data Platform (HDP)for Linux   
    EXEC sp_configure 'hadoop connectivity', 5;   
    RECONFIGURE;  
  
    -- Enable connectivity to Cloudera CDH for Linux   
    EXEC sp_configure 'hadoop connectivity', 3;   
    RECONFIGURE;  
  
    -- Disable the Hadoop connectivity option   
    EXEC sp_configure 'hadoop connectivity', 0;  
    RECONFIGURE;  
    ```  
  
    執行 sp_configure 使用 RECONFIGURE 設定組態值。 若要設定執行的值需要重新啟動區域。 因為必須重新啟動下, 一步 停止後也，您不需要在下一個步驟，變更 core-site.xml 之前，請重新啟動。  
  
4.  若要啟用 Microsoft Azure blob 儲存體做為外部資料來源，請先 PDW core-site.xml 檔案中加入一個或多個 Microsoft Azure 儲存體帳戶存取金鑰。 若要加入的機碼：  
  
    1.  尋找您的 Microsoft Azure 儲存體帳戶名稱。 若要檢視您的儲存體帳戶，登入[Azure 入口網站](https://portal.azure.com)按一下**儲存體帳戶 （傳統）**。  
  
        ![Windows Azure 儲存體帳戶名稱](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  找不到 Azure 儲存體帳戶存取金鑰。 若要這樣做，請按一下 儲存體帳戶名稱，並在 設定 刀鋒視窗上按一下**金鑰**。 這會顯示您的帳戶名稱和儲存體金鑰。  
  
        ![Windows Azure 儲存體帳戶存取金鑰](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  開啟 遠端桌面連接至 PDW 控制節點。  
  
    4.  開啟 C:\Program Files\Microsoft SQL Server 平行資料 Warehouse\100\Hadoop\conf\core-site.xml 的檔案。  
  
    5.  將具有名稱和值屬性的下列屬性加入至 core-site.xml。  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        這個範例會使用先前顯示的帳戶名稱和存取金鑰。  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > Core-site.xml 中儲存的存取金鑰之前採取安全預防措施。 任何使用者具有 CONTROL SERVER 或 ALTER ANY EXTERNAL DATA SOURCE 權限可以建立外部資料來源來存取此帳戶。 外部資料來源建立之後，所有 SQL Server PDW 具有都 CREATE TABLE 權限的使用者可以都建立會存取這個儲存體帳戶的外部資料表。 使用者即可存取帳戶的資料或使用的帳戶中的資源。  
  
    6.  Core-site.xml 儲存的變更。  
  
5.  加入 yarn-site.xml 檔案 yarn.application.classpath 屬性和值。  
  
    如果您要連接到外部的 Hadoop 1.3，略過此步驟。  
  
    從 Hadoop 2.0 開始，yarn-site.xml 檔案包含 Hadoop YARN framework 的組態設定。 這個檔案位於 [控制] 節點下**C:\program files\Microsoft SQL Server 平行資料 Warehouse\100\Hadoop\conf\\**。  
  
    若要對外部的 Hadoop 2.0 叢集執行 PolyBase 查詢，在 Windows 或 Linux 上，您要設定 yarn.application.classpath 屬性和值與外部的 Hadoop 叢集上的 yarn-site.xml 設定一致。 即使外部的 Hadoop 叢集使用的預設值，此設定是必要的。  
  
    預設設定的範例：  
  
    ```xml  
    <property>  
        <name>yarn.application.classpath</name>  
        <value>  
          %HADOOP_CONF_DIR%,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/*,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/lib/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/lib/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/lib/*  
         </value>  
      </property>  
    ```  
  
    一旦 yarn-site.xml 中定義的任何內容之後，PolyBase 針對 HDInsight 區域執行查詢時，就會使用這些屬性設定。 如果您打算在 Windows 上執行 PolyBase 查詢針對 HDInsight 區域與外部的 Hadoop 2.0 叢集，必須是所有 yarn-site.xml 檔案之間的一致性，或者 PolyBase 查詢將會失敗。  
  
    若要執行 PolyBase 針對 HDInsight 區域與外部的 Hadoop 2.0 叢集，請外部的 Hadoop 叢集上使用 yarn-site.xml 預設設定。  
  
6.  重新啟動 PDW 區域。 若要這樣做，請使用組態管理員工具。 請參閱[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md).  
  
7.  請確認 Hadoop 連線的安全性設定。 如果**弱的驗證**端啟用利用 Hadoop 上`dfs.permission = true`，您必須建立 Hadoop 使用者**pdw_user**授與完整讀取和寫入權限給此使用者。 SQL Server PDW 和對應的呼叫，從 SQL Server PDW 一律發出為**pdw_user**。  這是固定的使用者名稱，而且無法在此版本的 Hadoop 連接和 SQL Server PDW 版本中變更。 如果在 Hadoop 上的安全性已停用使用`dfs.permission = false`，則不需要採取任何進一步動作。  
  
8.  決定哪些使用者可以建立 Microsoft Azure blob 儲存體的外部資料來源。 提供給這些使用者的儲存體帳戶名稱以及**ALTER ANY EXTERNAL DATA SOURCE**或**CONTROL SERVER**權限。  
  
9. Hadoop 連線，您可以決定哪些使用者可以建立 Hadoop 的外部資料來源。 提供給這些使用者的 IP 位址和連接埠號碼，每個 Hadoop 名稱節點，並提供他們**ALTER ANY EXTERNAL DATA SOURCE**或者**CONTROL SERVER**權限。  
  
10. 連接到 WASB 也需要應用裝置上設定 DNS 轉送。 若要設定 DNS 轉送，請參閱[使用 DNS 轉寄站來解析非應用裝置的 DNS 名稱 &#40;Analytics Platform System &#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
授權的使用者現在可以建立外部資料來源、 外部檔案格式和外部資料表。 他們可以使用這些來整合多個來源資料包括 Hadoop，Microsoft Azure blob 儲存體和 SQL Server PDW。  

## <a name="kerberos-configuration"></a>Kerberos 設定  
請注意，當 PolyBase，向 Kerberos 受保護的叢集，hadoop.rpc.protection 設定必須設為驗證。 這樣會讓未加密的 Hadoop 節點之間維持資料通訊。 

 若要連接到 [使用 MIT KDC] 的 Kerberos 保護的 Hadoop 叢集：
   
  
1.  尋找 Hadoop 組態目錄中的控制節點上的安裝路徑：  
  
    ```  
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```  
  
2.  尋找資料表中所列之組態機碼的 Hadoop 端組態值。 (在 Hadoop 電腦上，尋找 Hadoop 組態目錄中的檔案)。  
  
3.  將組態值複製到 [控制] 節點上對應檔案中的 value 屬性。  
  
    |**#**|**組態檔**|**組態機碼**|**動作**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|指定 KDC 主機名稱。 例如：kerberos.your-realm.com。|  
    |2|core-site.xml|polybase.kerberos.realm|指定 Kerberos 領域。 例如：YOUR-REALM.COM|  
    |3|core-site.xml|hadoop.security.authentication|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如：KERBEROS<br></br>**安全性注意事項︰** KERBEROS 必須為大寫。 如果為小寫，KERBEROS 可能不會開啟。|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如：10.193.26.174:10020|  
    |7|yarn-site.xml yarn。|yarn.resourcemanager.principal|尋找 Hadoop 端組態並複製到 SQL Server 電腦。 例如： yarn/_HOST@YOUR-REALM.COM|  
  
4. 建立資料庫範圍的認證物件，以指定每個 Hadoop 使用者的驗證資訊。 請參閱 [PolyBase T-SQL objects](../relational-databases/polybase/polybase-t-sql-objects.md)(PolyBase T-SQL 物件)。  

5. 重新啟動 PDW 區域。 若要這樣做，請使用組態管理員工具。 請參閱[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md).
 
## <a name="see-also"></a>另請參閱  
[應用裝置組態 &#40;Analytics Platform System &#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
