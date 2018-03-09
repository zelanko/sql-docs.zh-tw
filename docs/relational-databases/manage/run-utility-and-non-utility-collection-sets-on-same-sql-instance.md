---
title: "在相同 SQL 執行個體上執行公用程式和非公用程式收集組 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a5e2b31d4fd6a92421ae701f7d25ebf451db654
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="run-utility-and-non-utility-collection-sets-on-same-sql-instance"></a>在相同 SQL 執行個體上執行公用程式和非公用程式收集組
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組與非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組會一起受到支援。 也就是說，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的成員時，可以受到其他收集組的監視。 但是，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式時，您必須停用非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資料收集功能。  
  
 當使用 UCP 註冊此執行個體之後，您必須重新啟動非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組。 但是請注意，Managed 執行個體上的所有收集組都會將其資料上傳到公用程式管理資料倉儲 (UMDW)；UMDW 檔案名稱為 sysutility_mdw。  
  
 若要將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組與非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組並存執行，請考量以下幾點：  
  
-   並存的收集組有受到支援。  
  
-   將執行個體註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式時，您必須停用現有的資料收集器。  
  
-   若要通過驗證需求，當您建立 UCP 之前，您必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行下列預存程序，而將它註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式之前，必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上：  
  
    ```  
    exec msdb.dbo.sp_syscollector_set_warehouse_database_name NULL  
    exec msdb.dbo.sp_syscollector_set_warehouse_instance_name NULL  
    ```  
  
     如果在您啟動建立 UCP 精靈或新增 Managed 執行個體精靈之前並未執行這些預存程序，此作業將會失敗。  
  
-   您必須針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體上的所有收集組使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公用程式 UMDW (sysutility_mdw)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [設定公用程式控制點資料倉儲 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  
