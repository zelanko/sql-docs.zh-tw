---
title: PolyBase 疑難排解 | Microsoft Docs
ms.custom: ''
ms.date: 8/29/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- PolyBase, monitoring
- PolyBase, performance monitoring
helpviewer_keywords:
- PolyBase, troubleshooting
ms.assetid: f119e819-c3ae-4e0b-a955-3948388a9cfe
caps.latest.revision: 22
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cadcbeb8e0c81afb9d56df7bf03f17214e400b3c
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="polybase-troubleshooting"></a>PolyBase, 疑難排解
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可使用您在本主題中找到的技術，為 PolyBase 的問題疑難排解。  
  
## <a name="catalog-views"></a>目錄檢視  
 使用此處所列的類別目錄檢視管理 PolyBase 作業。  
  
|||  
|-|-|  
|檢視|描述|  
|[sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)|指定外部資料表。|  
|[sys.external_data_sources &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)|指定外部資料來源。|  
|[sys.external_file_formats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)|指定外部檔案格式。|  
  
## <a name="dynamic-management-views"></a>動態管理檢視  
  
|||  
|-|-|  
|[sys.dm_exec_compute_node_errors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-errors-transact-sql.md)|[sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md)|  
|[sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|[sys.dm_exec_distributed_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)|  
|[sys.dm_exec_distributed_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-requests-transact-sql.md)|[sys.dm_exec_distributed_sql_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-sql-requests-transact-sql.md)|  
|[sys.dm_exec_dms_services &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)|[sys.dm_exec_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)|  
|[sys.dm_exec_external_operations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)|[sys.dm_exec_external_work &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)|  
  
  PolyBase 查詢會分成 sys.dm_exec_distributed_request_steps 內的一系列步驟。 下表提供步驟名稱與相關聯 DMV 的對應。
  
 |PolyBase 步驟|相關聯的 DMV|  
 |-|-| 
 |HadoopJobOperation | sys.dm_exec_external_operations|
 |RandomIdOperation | sys.dm_exec_distributed_request_steps|
 |HadoopRoundRobinOperation | sys.dm_exec_dms_workers|
 |StreamingReturnOperation | sys.dm_exec_dms_workers|
 |OnOperation | sys.dm_exec_distributed_sql_requests |
  
  
## <a name="to-monitor-polybase-queries-using-dmvs"></a>使用 DMV 監視 PolyBase 查詢  
 使用下列 DMV 監視及為 PolyBase 查詢的問題疑難排解。  
  
1.  **尋找執行時間最長的查詢**  
  
     記錄執行時間最長之查詢的執行識別碼。  
  
    ```sql  
     -- Find the longest running query  
    SELECT execution_id, st.text, dr.total_elapsed_time  
    FROM sys.dm_exec_distributed_requests  dr  
         cross apply sys.dm_exec_sql_text(sql_handle) st  
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
2.  **尋找執行時間最長的分散式查詢步驟**  
  
     使用在上個步驟記錄的執行識別碼。 記錄執行時間最長之步驟索引。  
  
     檢查執行時間最長之步驟的 location_type:  
  
    -   前端或計算：暗示 SQL 作業。 繼續執行步驟 3a。  
  
    -   DMS：暗示 PolyBase 資料移動服務作業。 繼續執行步驟 3b。  
  
    ```sql  
    -- Find the longest running step of the distributed query plan  
    SELECT execution_id, step_index, operation_type, distribution_type,   
    location_type, status, total_elapsed_time, command   
    FROM sys.dm_exec_distributed_request_steps   
    WHERE execution_id = 'QID4547'   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
3.  **尋找執行時間最長之步驟的執行進度**  
  
    1.  **尋找 SQL 步驟的執行進度**  
  
         使用先前步驟所記錄的執行識別碼與步驟索引。 使用先前步驟所記錄的執行識別碼與步驟索引。  
  
        ```sql  
        -- Find the execution progress of SQL step    
        SELECT execution_id, step_index, distribution_id, status,   
        total_elapsed_time, row_count, command   
        FROM sys.dm_exec_distributed_sql_requests   
        WHERE execution_id = 'QID4547' and step_index = 1;  
  
        ```  
  
    2.  **尋找 DMS 步驟的執行進度**  
  
         使用先前步驟所記錄的執行識別碼與步驟索引。  
  
        ```sql  
        -- Find the execution progress of DMS step    
        SELECT execution_id, step_index, dms_step_index, status,   
        type, bytes_processed, total_elapsed_time  
        FROM sys.dm_exec_dms_workers   
        WHERE execution_id = 'QID4547'   
        ORDER BY total_elapsed_time DESC;  
  
        ```  
  
4.  **尋找外部 DMS 作業的相關資訊**  
  
     使用先前步驟所記錄的執行識別碼與步驟索引。  
  
    ```sql  
    SELECT execution_id, step_index, dms_step_index, compute_node_id,   
    type, input_name, length, total_elapsed_time, status   
    FROM sys.dm_exec_external_work   
    WHERE execution_id = 'QID4547' and step_index = 7   
    ORDER BY total_elapsed_time DESC;  
  
    ```  
  
## <a name="to-view-the--polybase-query-plan"></a>檢視 PolyBase 查詢計劃  
  
1.  在 SSMS 中，啟用 [包括實際執行計畫] (Ctrl + M) 並執行查詢。  
  
2.  按一下 [執行計劃] 索引標籤。  
  
     ![PolyBase 查詢計畫](../../relational-databases/polybase/media/polybase-query-plan.png "PolyBase 查詢計畫")  
  
3.  在 [遠端查詢運算子] 上按一下滑鼠右鍵，然後選取 [屬性]。  
  
4.  複製遠端查詢值，並將其貼至文字編輯器，以檢視 XML 遠端查詢計劃。  下列為範例。  
  
    ```xml  
  
    <dsql_query number_nodes="1" number_distributions="8" number_distributions_per_node="8">  
      <sql>ExecuteMemo explain query</sql>  
      <dsql_operations total_cost="0" total_number_operations="6">  
        <dsql_operation operation_type="RND_ID">  
          <identifier>TEMP_ID_74</identifier>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_74] ([SensorKey] INT NOT NULL, [CustomerKey] INT NOT NULL, [GeographyKey] INT, [Speed] FLOAT(53) NOT NULL, [YearMeasured] INT NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">EXEC [tempdb].[sys].[sp_addextendedproperty] @name=N'IS_EXTERNAL_STREAMING_TABLE', @value=N'true', @level0type=N'SCHEMA', @level0name=N'dbo', @level1type=N'TABLE', @level1name=N'TEMP_ID_74'</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">UPDATE STATISTICS [tempdb].[dbo].[TEMP_ID_74] WITH ROWCOUNT = 2401, PAGECOUNT = 7</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
        <dsql_operation operation_type="MULTI">  
          <dsql_operation operation_type="STREAMING_RETURN">  
            <operation_cost cost="1" accumulative_cost="1" average_rowsize="24" output_rows="5762.1" />  
            <location distribution="AllDistributions" />  
            <select>SELECT [T1_1].[SensorKey] AS [SensorKey],  
           [T1_1].[CustomerKey] AS [CustomerKey],  
           [T1_1].[GeographyKey] AS [GeographyKey],  
           [T1_1].[Speed] AS [Speed],  
           [T1_1].[YearMeasured] AS [YearMeasured]  
    FROM   (SELECT [T2_1].[SensorKey] AS [SensorKey],  
                   [T2_1].[CustomerKey] AS [CustomerKey],  
                   [T2_1].[GeographyKey] AS [GeographyKey],  
                   [T2_1].[Speed] AS [Speed],  
                   [T2_1].[YearMeasured] AS [YearMeasured]  
            FROM   [tempdb].[dbo].[TEMP_ID_74] AS T2_1  
            WHERE  ([T2_1].[Speed] > CAST (6.50000000000000000E+001 AS FLOAT))) AS T1_1</select>  
          </dsql_operation>  
          <dsql_operation operation_type="ExternalRoundRobinMove">  
            <operation_cost cost="16.594848" accumulative_cost="17.594848" average_rowsize="24" output_rows="19207" />  
            <external_uri>hdfs://10.193.26.177:8020/Demo/car_sensordata.tbl/</external_uri>  
            <destination_table>[TEMP_ID_74]</destination_table>  
          </dsql_operation>  
        </dsql_operation>  
        <dsql_operation operation_type="ON">  
          <location permanent="false" distribution="AllDistributions" />  
          <sql_operations>  
            <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_74]</sql_operation>  
          </sql_operations>  
        </dsql_operation>  
      </dsql_operations>  
    </dsql_query>  
    ```  
  
## <a name="to-monitor-nodes-in-a-polybase-group"></a>監視 PolyBase 群組中的節點  
 設定 PolyBase 相應放大群組中的電腦之後，即可監視這些電腦的狀態。 如需建立相應放大群組的詳細資料，請參閱 [PolyBase 相應放大群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。  
  
1.  連接到群組前端節點上的 SQL Server。  
  
2.  執行 DMV [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) ，以檢視 PolyBase 群組中的所有節點。  
  
3.  執行 DMV [sys.dm_exec_compute_node_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-node-status-transact-sql.md) ，以檢視 PolyBase 群組中所有節點的狀態。  
  
 ## <a name="known-limitations"></a>已知限制
 
 PolyBase 具有下列限制： 
 - 可能的最大資料列大小 (包括變數長度資料行的完整長度) 在 SQL Server 中不能超過 32 KB，而在 Azure SQL 資料倉儲中則不能超過 1 MB。 
 - PolyBase 不支援 Hive 0.12 以上的資料類型 (也就是 Char()、VarChar())   
 - 將資料從 SQL Server 或 Azure SQL 資料倉儲匯出為 ORC 檔案格式時，可以將具有大量文字的資料行限制為最少 50 個資料行，因為會發生 Java 記憶體不足錯誤。 若要解決這個問題，只需要匯出資料行的子集。
 - 無法讀取或寫入在 Hadoop 中靜止加密的資料， 包括 HDFS 加密區域或透明加密。
 - 如果已啟用 KNOX，PolyBase 就無法連接至 Hortonworks 執行個體。 
 - 若您使用 Hive 資料表，且 transactional = true，PolyBase 就無法存取 Hive 資料表目錄中的資料。 


[將節點新增至 SQL Server 2016 容錯移轉叢集時，不會安裝 PolyBase](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)

## <a name="hadoop-name-node-high-availability"></a>Hadoop 名稱節點的高可用性
PolyBase 不會與名稱節點 HA 服務互動，例如目前的 Zookeeper 或 Knox。 不過，有一個經證實有效的因應措施可以提供這項功能。 

因應措施：使用 DNS 名稱，將連線重新路由到作用中的名稱節點。 若要這樣做，您必須確認外部資料來源是使用 DNS 名稱來與名稱節點通訊。 發生名稱節點容錯移轉時，您必須變更與外部資料來源定義中所用的 DNS 名稱建立關聯的 IP 位址。 如此即會將所有新的連線重新路由至正確的名稱節點。 發生容錯移轉時，現有的連線將會失敗。 若要自動化此程序，「活動訊號」可 Ping 到作用中的名稱節點。 如果活動訊號失敗，我們就可以假設發生過容錯移轉，並自動切換至次要的 IP 位址。


## <a name="error-messages-and-possible-solutions"></a>錯誤訊息與可能的解決方案

若要針對外部資料表錯誤進行疑難排解，請參閱 Murshed Zaman 的部落格 [https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/](https://blogs.msdn.microsoft.com/sqlcat/2016/06/21/polybase-setup-errors-and-possible-solutions/ "PolyBase setup errors and possible solutions") (PolyBase 安裝程式錯誤和可能的解決方案)。

## <a name="see-also"></a>另請參閱
[對 PolyBase Kerberos 的連線問題進行疑難排解](polybase-troubleshoot-connectivity.md)
