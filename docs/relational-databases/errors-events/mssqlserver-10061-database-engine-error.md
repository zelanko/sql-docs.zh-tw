---
title: MSSQLSERVER_10061 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: "10061"
helpviewer_keywords: 10061 (Database Engine error)
ms.assetid: 729602f3-08df-474c-8740-8dea13c1eee3
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2fd332b8fb849ae9fc364d081e31b731a78113d3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10061"></a>MSSQLSERVER_10061
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10061|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|建立伺服器的連接時發生錯誤。  連接到 SQL Server 時，可能因為在預設的設定下 SQL Server 不允許遠端連接而引起此失敗。 (提供者: TCP 提供者，錯誤: 0 - 無法連線，因為目標電腦拒絕連線。) (Microsoft SQL Server，錯誤: 10061)|  
  
## <a name="explanation"></a>說明  
伺服器並未回應用戶端要求。 發生這個錯誤可能是因為伺服器尚未啟動。  
  
## <a name="user-action"></a>使用者動作  
請確定伺服器已經啟動。  
  
## <a name="see-also"></a>另請參閱  
[管理 Database Engine Services](~/database-engine/configure-windows/manage-the-database-engine-services.md)  
[設定用戶端通訊協定](~/database-engine/configure-windows/configure-client-protocols.md)  
[網路通訊協定和網路程式庫](~/sql-server/install/network-protocols-and-network-libraries.md)  
[用戶端網路組態](~/database-engine/configure-windows/client-network-configuration.md)  
[設定用戶端通訊協定](~/database-engine/configure-windows/configure-client-protocols.md)  
[啟用或停用伺服器網路通訊協定](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
