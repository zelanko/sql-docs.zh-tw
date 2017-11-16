---
title: MSSQLSERVER_1205 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1205 (Database Engine error)
ms.assetid: 9fe3f67c-df3c-4642-a3a4-ccc0e138b632
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: afbc0f15e52f470d88514a4e3cf865447a4a64fd
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1205"></a>MSSQLSERVER_1205
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|1205|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LK_VICTIM|  
|訊息文字|交易 (處理序識別碼 %d) 在 %.*ls 資源上被另一個處理序鎖死，並已被選為死結的犧牲者。 請重新執行該交易。|  
  
## <a name="explanation"></a>說明  
個別交易上的資源存取順序發生衝突，因而產生死結。 例如：  
  
-   Transaction1 會更新 **Table1.Row1**，而 Transaction2 會更新 **Table2.Row2**。  
  
-   Transaction1 會嘗試更新 **Table2.Row2**，但是卻因為 Transaction2 尚未獲得認可而遭到封鎖。  
  
-   現在 Transaction2 會嘗試更新 **Table1.Row1**，但是因為 Transaction1 尚未獲得認可而遭到封鎖。  
  
-   由於 Transaction1 正在等候 Transaction2 完成執行，而同時 Transaction2 也在等候 Transaction1 執行完成，因此發生死結。  
  
系統將會偵測到這個死結，並選擇其中一個交易做為「犠牲者」，然後發出這則訊息，同時回復犠牲者的交易。  
  
## <a name="user-action"></a>使用者動作  
重新執行交易。 您也可以修訂應用程式以避免死結。 您可以重試系統選擇做為犠牲者的交易，而且該交易可能會成功 (依據同時執行的作業而定)。  
  
若要防止或避免發生死結，請考慮讓所有的交易都以相同的順序來存取資料列 (先存取 **Table1**，然後存取 **Table2**)；如此，雖然可能會發生封鎖，但是不會發生死結。  
  

