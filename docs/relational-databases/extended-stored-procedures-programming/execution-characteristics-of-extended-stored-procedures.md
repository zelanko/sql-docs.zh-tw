---
title: 擴充預存程序的執行特性 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], executing
- executing extended stored procedures [SQL Server]
ms.assetid: 6fe1f7e8-cc02-49df-8a2a-d47a96ec3567
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 93cb1b63e768623e39bcd5267c029a4ccb550c6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62742414"
---
# <a name="execution-characteristics-of-extended-stored-procedures"></a>擴充預存程序的執行特性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 擴充預存程序的執行具有下列特性：  
  
-   安全性內容下執行擴充預存程序函式[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   擴充預存程序函數會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的處理序空間中執行。  
  
-   與擴充預存程序執行相關聯的執行緒與用於用戶端連接的執行緒相同。  
  
    > [!IMPORTANT]  
    >  將擴充預存程序加入伺服器，並將執行權限授與其他使用者之前，系統管理員應徹底檢閱每個擴充預存程序，以確定其中不含任何有害或惡意的程式碼。  
  
-  
  
 擴充預存程序載入 DLL 之後，DLL 仍保持載入狀態之前的伺服器的位址空間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已停止或系統管理員明確卸載 DLL 使用 DBCC *DLL_name* （免費）。  
  
 擴充預存程序可以使用 EXECUTE 陳述式，從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 當做預存程序執行：  
  
```  
EXECUTE @retval = xp_extendedProcName @param1, @param2 OUTPUT  
```  
  
## <a name="parameters"></a>參數  
 \@ *retval*  
 這是傳回值。  
  
 \@ *param1*  
 這是輸入參數。  
  
 \@ *param2*  
 這是輸入/輸出參數。  
  
> [!CAUTION]  
>  擴充預存程序會提供效能增強功能並擴充 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。 不過，由於擴充預存程序 DLL 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用相同的位址空間，因此問題程序可能會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 運作造成不利的影響。 雖然擴充預存程序 DLL 擲回的例外會由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理，還是有可能使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料區域受損。 基於安全性考量，只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員可以將擴充預存程序加入到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些程序應該經過徹底測試，才能進行安裝。  
  
## <a name="see-also"></a>另請參閱  
 [擴充預存程序程式設計](../../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)   
 [查詢 SQL Server 中安裝的擴充預存程序](../../relational-databases/extended-stored-procedures-programming/querying-extended-stored-procedures-installed-in-sql-server.md)  
  
  
