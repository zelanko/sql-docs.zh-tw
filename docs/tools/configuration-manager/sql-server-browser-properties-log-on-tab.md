---
title: "SQL Server Browser 屬性 （登入 索引標籤） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c77871ec-c2f4-4e4a-9a10-5aeb4ae70507
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: acc99f6cace37453d01cbe5a0f3ea790ace7d927
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-browser-properties-log-on-tab"></a>SQL Server Browser 屬性 (登入索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 程式會執行為服務的伺服器上。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會接聽 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源的內送要求，並提供有關電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資訊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器會接聽 UDP 通訊埠，並接受使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) 的未驗證要求。  
  
 帳戶密碼的變更會立即生效，不需要重新啟動服務。  
  
## <a name="options"></a>選項。  
 **本機系統帳戶**  
 在本機系統帳戶的安全性內容執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。 如果可能的話，請另外使用權限較低的帳戶來執行。  
  
 **這個帳戶**  
 指定使用 Windows 驗證的本機或網域使用者帳戶。 建議您使用具有最少服務權限的網域使用者帳戶。 如需有關選取帳戶的資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜設定 Windows 服務帳戶＞。  
  
 **瀏覽**  
 瀏覽使用者或內建的安全性主體。  
  
> [!IMPORTANT]  
>  請使用低權限的帳戶。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務所需權限的資訊，請參閱 [SQL Server Browser 服務](../../tools/configuration-manager/sql-server-browser-service.md)的＜安全性＞一節。  
  
 **密碼**  
 輸入安全性主體的密碼。  
  
 **確認密碼**  
 確認安全性主體的密碼。  
  
 **服務狀態**  
 表示這項服務為執行中、已停止或已停用。 "" 表示狀態變更已暫止。  
  
 **啟動**  
 啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器服務。  
  
 **停止**  
 停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
 **暫停**  
 暫停 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。  
  
 **繼續**  
 繼續已暫停的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器服務。  
  
## <a name="see-also"></a>請參閱  
 [SQL Server Browser 服務](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
