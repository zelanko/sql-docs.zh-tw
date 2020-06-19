---
title: SQL Server 的相同實例上執行公用程式和非公用程式收集組的考慮 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f34dfa48e9962e445aa8848399980331899065f1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023203"
---
# <a name="considerations-for-running-utility-and-non-utility-collection-sets-on-the-same-instance-of-sql-server"></a>在相同 SQL Server 執行個體上執行公用程式和非公用程式收集組的考量事項
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組與非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組會一起受到支援。 也就是說，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的成員時，可以受到其他收集組的監視。 但是，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式時，您必須停用非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資料收集功能。  
  
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
 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)   
 [設定公用程式控制點資料倉儲 &#40;SQL Server 公用程式&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  
