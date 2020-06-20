---
title: 設定容錯移轉叢集上的 FILESTREAM | Microsoft 文件
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], setting up on a failover cluster
ms.assetid: 6721f780-20b7-4109-8ddb-ac327310699e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ddc4021866d6b6622d6ad4aaacd00389da40ca0
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970818"
---
# <a name="set-up-filestream-on-a-failover-cluster"></a>設定容錯移轉叢集上的 FILESTREAM
  此主題描述如何在容錯移轉叢集上設定 FILESTREAM。 在您嘗試進行這個程序之前，應該先了解 [容錯移轉叢集](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) 並啟用 FILESTREAM。 如需如何啟用 FILESTREAM 的相關資訊，請參閱 [啟用及設定 FILESTREAM](enable-and-configure-filestream.md)。  
  
### <a name="to-set-up-filestream-on-a-failover-cluster"></a>在容錯移轉叢集上設定 FILESTREAM  
  
1.  設定容錯移轉叢集的主要節點。  
  
     設定完成之後，請使用 [SQL Server 組態管理員]  ，在主要節點上啟用 FILESTREAM。 這樣就會啟用需要 Windows Admin 權限的設定。 如果需要進行遠端存取，請選取 [允許遠端用戶端具有 FILESTREAM 資料的資料流存取權]  。 這樣將會建立檔案共用叢集資源。  
  
2.  設定被動節點。  
  
     設定完成之後，請使用 [SQL Server 組態管理員]  ，在被動節點上啟用 FILESTREAM。 您針對 [Windows 共用名稱]  指定的名稱必須在叢集的所有節點中相同。  
  
3.  若要加入更多被動節點，請重複步驟 2。  
  
4.  加入所有節點之後，請在每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上執行 sp_configure 預存程序，完成此程序。  
  
5.  若要隨時在叢集中加入並啟用其他節點，您可以重複步驟 2、3 和 4。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [建立新的 SQL Server 容錯移轉叢集 &#40;安裝程式&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [移除 SQL Server 容錯移轉叢集執行個體 &#40;安裝程式&#41;](../../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)   
 [在 SQL Server 容錯移轉叢集中新增或移除節點 &#40;安裝程式&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
  
