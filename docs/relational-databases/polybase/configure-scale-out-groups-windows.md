---
title: 改善 Windows 上的 PolyBase 相應放大群組 | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: polybase
ms.topic: tutorial
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b9294d9208b9cafc3610a9682c13cebcc970669e
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51672937"
---
# <a name="improve-polybase-scale-out-groups-on-windows"></a>改善 Windows 上的 PolyBase 相應放大群組

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文描述如何在 Windows 上設定 [PolyBase 相應放大群組](polybase-scale-out-groups.md)。 這會建立 SQL Server 執行個體叢集，以相應放大方式處理來自外部資料來源 (例如 Hadoop 或 Azure Blob 儲存體) 的大型資料集，以提高查詢效能。

## <a name="prerequisites"></a>Prerequisites
  
- 相同網域內有一部以上的電腦  
  
- 一個執行 PolyBase 服務的網域使用者帳戶  
  
## <a name="process-overview"></a>程序概觀

下列步驟摘要建立 PolyBase 相應放大群組的程序。 下一節會提供每個步驟更詳細的逐步解說。
  
1. 在 N 部電腦上安裝同一個含有 PolyBase 的 SQL Server 版本。
  
2. 選取一個 SQL Server 執行個體做為前端節點。 只可在執行 SQL Server Enterprise 的執行個體中指定前端節點。
  
3. 使用 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)，加入其餘的 SQL Server 執行個體作為計算節點。

4. 使用 [sys.dm_exec_compute_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md) 監視群組中的節點。

5. 選擇性。 使用 [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md) 移除運算節點。

## <a name="example-walk-through"></a>範例逐步解說

這會使用下列項目逐步設定 PolyBase 群組︰  
  
1. 位於網域 *PQTH4A* 中的兩部電腦 電腦名稱為︰  
  
   - PQTH4A-CMP01  
  
   - PQTH4A-CMP02  
  
2. 網域帳戶︰*PQTH4A\PolyBaseUse*r  

## <a name="install-sql-server-with-polybase-on-all-machines"></a>在所有電腦上安裝包含 PolyBase 的 SQL Server

1. 執行 setup.exe。
  
2. 在 [功能選取] 頁面上，選取 [適用於外部資料的 PolyBase 查詢服務]。
  
3. 在 [伺服器設定] 頁面上，針對 SQL Server PolyBase 引擎和 SQL Server PolyBase 資料移動服務，請使用**網域帳戶** PQTH4A\PolyBaseUser。
  
4. 在 [PolyBase 組態] 頁面上，選取 [Use the SQL Server instance as part of a PolyBase scale-out group (使用此 SQL Server 執行個體作為 PolyBase 向外延展群組的一部分)]。 這會開啟防火牆，以允許 PolyBase 服務的連入連線。
  
5. 安裝程式完成之後，執行 **services.msc**。 確認 SQL Server、PolyBase Engine 和 PolyBase Data Movement Service 正在執行中。
  
   ![PolyBase 服務](../../relational-databases/polybase/media/polybase-services.png "PolyBase 服務")  
  
## <a name="select-one-sql-server-as-head-node"></a>選取一個 SQL Server 作為前端節點  
  
安裝程式完成之後，這兩部電腦可用來做為 PolyBase 群組前端節點。 在此範例中，我們將選擇 PQTH4A-CMP01 上的 "MSSQLSERVER" 做為前端節點。
  
## <a name="add-other-sql-server-instances-as-compute-nodes"></a>新增其他 SQL Server 節點作為計算節點  
  
1. 連接到 PQTH4A-CMP02 上的 SQL Server。
  
2. 執行預存程序 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)。

   ```sql
   -- Enter head node details:
   -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';
   ```  

3. 在計算節點 (PQTH4A-CMP02) 上執行 services.msc。
  
4. 關閉 PolyBase Engine 並重新啟動 PolyBase Data Movement Service。
  
## <a name="optional-remove-a-compute-node"></a>選擇性：移除計算節點  
  
1. 連接到計算節點 SQL Server (PQTH4A-CMP02)。
  
2. 執行預存程序 sp_polybase_leave_group。
  
    ```sql  
    EXEC sp_polybase_leave_group;  
    ```  
  
3. 在已移除的計算節點 (PQTH4A-CMP02) 上執行 services.msc。
  
4. 啟動 PolyBase Engine。 重新啟動 PolyBase Data Movement Service。
  
5. 在 PQTH4A-CMP01 上執行 DMV sys.dm_exec_compute_nodes，確認節點已移除。 現在，PQTH4A-CMP02 將可用來做為獨立的前端節點  
  
## <a name="next-steps"></a>後續步驟  

如需疑難排解，請參閱 [PolyBase troubleshooting with dynamic management views](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)。
  
如需 PolyBase 的詳細資訊，請參閱 [PolyBase 概觀](../../relational-databases/polybase/polybase-guide.md)。
