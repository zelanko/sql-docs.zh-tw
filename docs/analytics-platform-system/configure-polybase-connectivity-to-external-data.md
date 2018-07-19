---
title: 設定 PolyBase 連線能力-Analytics Platform System |Microsoft Docs
description: 說明如何設定連接至外部 Hadoop 或 Microsoft Azure 儲存體 blob 資料來源的平行處理資料倉儲的 PolyBase。 若要執行查詢來整合資料的多個來源，包括 Hadoop、 Azure blob 儲存體和平行處理資料倉儲使用 PolyBase。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 26eeffb1d2a27ee49f01114b015ab4051b145d64
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909868"
---
# <a name="configure-polybase-connectivity-to-external-data"></a>設定 PolyBase 連線到外部資料
說明如何設定連接至外部 Hadoop 或 Microsoft Azure 儲存體 blob 資料來源的平行處理資料倉儲的 PolyBase。 若要執行查詢來整合資料的多個來源，包括 Hadoop、 Azure blob 儲存體和平行處理資料倉儲使用 PolyBase。  
  
### <a name="to-configure-connectivity"></a>若要設定連線  
  
1.  開啟查詢工具，例如 sqlcmd 或 SQL Server Data Tools (SSDT)，並執行 sp_configure 來檢視目前的 'hadoop connectivity' 設定。  
  
    ![hadoop 連接性設定](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  決定哪些需求，以及是否需要變更目前的設定，請設定您的 Hadoop 連線能力。 此選項適用於整個 SQL Server PDW 區域。 如需完整的組態設定和版本清單，請參閱 < [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
3.  若要變更 'hadoop connectivity' 設定，請使用 RECONFIGURE 執行 sp_configure。 以下是一些範例。  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP) or HDInsight’s Microsoft Azure blob storage  
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
  
    使用 RECONFIGURE 執行 sp_configure 設定組態值。 若要設定的執行的值需要重新啟動區域。 因為必須重新啟動後接下來, 也，您不需要在下一步 的步驟中，變更 core-site.xml 之前，請重新啟動。  
  
4.  若要啟用 Microsoft Azure blob 儲存體，做為外部資料來源，請先 PDW core-site.xml 檔案中加入一或多個 Microsoft Azure 儲存體帳戶存取金鑰。 若要新增的機碼：  
  
    1.  尋找您的 Microsoft Azure 儲存體帳戶名稱。 若要檢視您的儲存體帳戶，登入[Azure 入口網站](https://portal.azure.com)然後按一下**儲存體帳戶 （傳統）**。  
  
        ![Windows Azure 儲存體帳戶名稱](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  尋找您的 Azure 儲存體帳戶存取金鑰。 若要這樣做，請按一下 儲存體帳戶名稱，並在 設定 刀鋒視窗上按一下 **金鑰**。 這會顯示您的帳戶名稱和儲存體金鑰。  
  
        ![Windows Azure 儲存體帳戶存取金鑰](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  開啟 PDW 控制節點的遠端桌面連線。  
  
    4.  開啟檔案 C:\Program Files\Microsoft SQL Server 平行資料 Warehouse\100\Hadoop\conf\core-site.xml。  
  
    5.  將具有名稱和值屬性的下列屬性新增至 core-site.xml。  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        此範例會使用先前所示的帳戶名稱和存取金鑰。  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > 之前 core-site.xml 中儲存的存取金鑰所採取的安全預防措施。 任何具有 CONTROL SERVER 或 ALTER ANY EXTERNAL DATA SOURCE 權限的使用者可以建立外部資料來源來存取此帳戶。 外部資料來源建立後，所有 SQL Server PDW 具有都 CREATE TABLE 權限的使用者可以都建立外部資料表來存取此儲存體帳戶。 使用者可以存取帳戶的資料然後使用帳戶中的資源。  
  
    6.  Core-site.xml 中儲存的變更。  
  
5.  您可以將 yarn.application.classpath 屬性和值加入 yarn-site.xml 檔案。  
  
    如果您要連接至外部 Hadoop 1.3，請略過此步驟。  
  
    從 Hadoop 2.0 開始，yarn-site.xml 檔案包含 Hadoop YARN 架構的組態設定。 這個檔案位於 [控制] 節點底下**C:\program files\Microsoft SQL Server 平行資料 Warehouse\100\Hadoop\conf\\**。  
  
    若要在 Windows 或 Linux 上，針對外部 Hadoop 2.0 叢集執行 PolyBase 查詢，您需要設定 yarn.application.classpath 屬性和值可與外部 Hadoop 叢集上的 yarn-site.xml 設定一致。 即使外部 Hadoop 叢集使用的預設設定，不需要此組態。  
  
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
  
    一旦 yarn-site.xml 中定義任何屬性之後，PolyBase 針對 Hadoop 執行查詢時，就會使用這些屬性設定。 如果您打算在 Windows 上，針對 Azure 儲存體 Blob 和外部 Hadoop 2.0 叢集中執行 PolyBase 查詢時，必須在所有 yarn-site.xml 檔案之間的一致性，否則 PolyBase 查詢將會失敗。  
   
6.  重新啟動的 PDW 區域。 若要這樣做，請使用組態管理員工具。 請參閱[啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
7.  驗證 Hadoop 連線的安全性的設定。 如果**弱式驗證**在 Hadoop 上使用啟用戶端`dfs.permission = true`，您必須建立的 Hadoop 使用者**pdw_user**授與完整的讀取和寫入權限給這位使用者。 SQL Server PDW 和對應的呼叫，從 SQL Server PDW 一律都以發出**pdw_user**。  這是固定的使用者名稱，而且無法在這個版本的 Hadoop 連線能力] 和 [SQL Server PDW 發行變更。 如果使用已停用在 Hadoop 上的安全性`dfs.permission = false`，則不需要採取任何進一步的動作。  
  
8.  決定哪些使用者可以建立 Microsoft Azure blob 儲存體外部資料來源。 讓這些使用者的每個儲存體帳戶名稱和也**ALTER ANY EXTERNAL DATA SOURCE**或是**CONTROL SERVER**權限。  
  
9. Hadoop 連線，您可以決定哪些使用者可以建立 Hadoop 的外部資料來源。 讓這些使用者的每個 IP 位址和連接埠號碼，每個 Hadoop 名稱節點，並提供他們**ALTER ANY EXTERNAL DATA SOURCE**或是**CONTROL SERVER**權限。  
  
10. 連接到 WASB 也需要在設備上設定 DNS 轉送。 若要設定 DNS 轉送，請參閱[使用 DNS 轉寄站解析非設備 DNS 名稱&#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)。  
  
授權的使用者現在可以建立外部資料來源、 外部檔案格式和外部資料表。 他們可以使用這些來將資料從多個來源，包括 Hadoop、 整合 Microsoft Azure blob 儲存體和 SQL Server PDW。  

## <a name="kerberos-configuration"></a>Kerberos 設定  
請注意，向 Kerberos 受保護的叢集驗證 PolyBase 時, hadoop.rpc.protection 設定必須設定驗證。 這會導致 Hadoop 節點之間的資料通訊未加密。 

 若要連線到受 Kerberos 保護的 Hadoop 叢集 [使用 MIT KDC]:
   
  
1.  在控制節點上的安裝路徑中，尋找 Hadoop 組態目錄：  
  
    ```  
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```  
  
2.  尋找資料表中所列之組態機碼的 Hadoop 端組態值。 (在 Hadoop 電腦上，尋找 Hadoop 組態目錄中的檔案)。  
  
3.  將組態值複製到控制節點上的對應檔案中的 value 屬性中。  
  
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

5. 重新啟動的 PDW 區域。 若要這樣做，請使用組態管理員工具。 請參閱[啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。
 
## <a name="see-also"></a>另請參閱  
[設備設定&#40;Analytics Platform System&#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
