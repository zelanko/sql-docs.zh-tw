---
title: 遠端管理員連接伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- administrator connections [SQL Server]
- DAC
- connections [SQL Server], dedicated administrator
- remote admin connections option
- dedicated administrator connections [SQL Server]
ms.assetid: bf32b60a-7a48-401f-b6be-b5e2e46c413f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4e4894fa7e05c863095fdca7b26f448efe176216
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62781457"
---
# <a name="remote-admin-connections-server-configuration-option"></a>遠端管理員連接伺服器組態選項
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供專用管理員連接 (DAC)。 DAC 可讓系統管理員存取執行中的伺服器，如此一來，即使伺服器遭到鎖定或在異常狀態下執行，而且未回應 [!INCLUDE[tsql](../../includes/tsql-md.md)] 連接時，也能執行診斷功能或 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 陳述式，或針對伺服器上的問題進行疑難排解。 依預設，只能從伺服器上的用戶端使用 DAC。 若要讓遠端電腦上的用戶端應用程式使用 DAC，請使用 sp_configure 的 remote admin connections 選項。  
  
 根據預設，DAC 只會接聽回送 IP 位址 (127.0.0.1)、通訊埠 1434。 如果無法使用 TCP 通訊埠 1434，當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 啟動時，會自動指派 TCP 通訊埠。 在電腦上安裝多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，請檢查錯誤記錄檔以取得 TCP 通訊埠編號。  
  
 下表列出 remote admin connections 選項的可能值。  
  
|值|描述|  
|-----------|-----------------|  
|0|表示只允許使用 DAC 的本機連接。|  
|1|表示允許使用 DAC 的遠端連接。|  
  
## <a name="example"></a>範例  
 下列範例會從遠端電腦啟用 DAC。  
  
```  
sp_configure 'remote admin connections', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫管理員的診斷連接](diagnostic-connection-for-database-administrators.md)  
  
  
