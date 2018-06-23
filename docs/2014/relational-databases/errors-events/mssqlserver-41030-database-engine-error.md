---
title: MSSQLSERVER_41030 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 41030 (Database Engine error)
ms.assetid: c85341ae-0fbf-42ae-9275-4cfe678238f0
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7a823405ff23184459a7057aae61267754d6a3aa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145411"
---
# <a name="mssqlserver41030"></a>MSSQLSERVER_41030
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41030|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|OPEN_CLUSTER_SUB_KEY|  
|訊息文字|無法開啟 Windows Server 容錯移轉叢集登錄子機碼 '%.*ls' (錯誤碼 %d)。  父機碼是叢集根目錄機碼。  WSFC 服務可能不在執行中、無法以目前狀態存取，或指定的引數無效。 如果已卸除對應的可用性群組，就會發生這種錯誤。 如需有關這個錯誤碼的資訊，請參閱 Windows 開發文件中的＜系統錯誤碼＞(System Error Codes)。|  
  
## <a name="explanation"></a>說明  
 如果 WSFC 叢集已終結，它會移除與 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 相關的所有登錄機碼。  
  
## <a name="user-action"></a>使用者動作  
 在重新建立 WSFC 叢集之後，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體已啟用 AlwaysOn 的每個叢集節點上停用然後重新啟用 AlwaysOn。 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來執行此工作。  
  
## <a name="see-also"></a>另請參閱  
 [啟用和停用 AlwaysOn 可用性群組&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [SQL Server 的 Windows Server 容錯移轉叢集 &#40;WSFC&#41;](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  