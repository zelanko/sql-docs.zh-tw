---
title: 遠端管理員連接伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
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
manager: jroth
ms.openlocfilehash: 43fc46517ffbf639cfc9328510ad4550e048cbc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66772067"
---
# <a name="remote-admin-connections-server-configuration-option"></a>遠端管理員連接伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供專用管理員連接 (DAC)。 DAC 可讓系統管理員存取執行中的伺服器，如此一來，即使伺服器遭到鎖定或在異常狀態下執行，而且未回應 [!INCLUDE[tsql](../../includes/tsql-md.md)] 連接時，也能執行診斷功能或 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 陳述式，或針對伺服器上的問題進行疑難排解。 依預設，只能從伺服器上的用戶端使用 DAC。 若要讓遠端電腦上的用戶端應用程式使用 DAC，請使用 sp_configure 的 remote admin connections 選項。  
  
 根據預設，DAC 只會接聽回送 IP 位址 (127.0.0.1)、通訊埠 1434。 如果無法使用 TCP 通訊埠 1434，當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 啟動時，會自動指派 TCP 通訊埠。 在電腦上安裝多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，請檢查錯誤記錄檔以取得 TCP 通訊埠編號。  
  
 下表列出 remote admin connections 選項的可能值。  
  
|ReplTest1|Description|  
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
 [資料庫管理員的診斷連接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
