---
title: catalog.startup | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a97fe82fffae638cc40fceb8139ba65c080e7955
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854706"
---
# <a name="catalogstartup"></a>catalog.startup
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  執行 SSISDB 目錄之作業狀態的維護。  
  
 預存程序會在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 伺服器執行個體效能降低時，修正正在執行之任何封裝的狀態。  
  
 您可以選擇讓預存程序在每次 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 伺服器執行個體重新啟動時自動執行，方法是選取 [建立目錄] 對話方塊中的 [在 SQL Server 啟動時允許自動執行 Integration Services 預存程序] 選項。  
  
## <a name="syntax"></a>語法  
  
```sql  
catalog.startup  
```  
  
## <a name="return-code-value"></a>傳回碼值  
 0 (成功)  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="permissions"></a>[權限]  
 這個預存程序需要下列其中一個權限：  
  
-   執行執行個體的 READ 和 MODIFY 權限、專案的 READ 和 EXECUTE 權限，以及 (如果適用的話) 參考環境的 READ 權限  
  
-   **ssis_admin** 資料庫角色的成員資格  
  
-   **系統管理員**伺服器角色的成員資格  
  
  
