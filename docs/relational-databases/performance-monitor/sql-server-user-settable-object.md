---
title: "SQL Server 的 User Settable 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- User Settable object
- SQLServer:User Settable
ms.assetid: 633de3ef-533c-4f0c-9c7b-c105129d8e94
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4d60d2059230ed74f72ef4e5ad7f32a3f91aa40b
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-user-settable-object"></a>SQL Server 的 User Settable 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 **User Settable** 物件可讓您建立自訂計數器執行個體。 使用自訂計數器執行個體來監視現有計數器未監視的伺服器層面，例如您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫獨有的元件 (例如，記錄的客戶訂單數或產品庫存數)。  
  
 **User Settable** 物件包含從 **User counter 1** 到 **User counter 10**這 10 個查詢計數器執行個體。 這些計數器分別對應至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_user_counter1 **到** sp_user_counter10 **的**預存程序。 當使用者應用程式執行這些預存程序時，預存程序所設定的數值將顯示於「系統監視器」內。 計數器可監視任何一個整數值，例如計算特定產品在某天內發生的訂單數的預存程序。  
  
> [!NOTE]  
>  「系統監視器」不會自動輪詢使用者計數器預存程序。 必須由使用者應用程式明確執行，才會更新計數器的值。 請利用觸發程序來自動更新計數器的值。 例如，若要建立計數器來監視資料表的資料列數目，請在資料表建立 INSERT 和 DELETE 觸發程序來執行下列陳述式： `SELECT COUNT(*) FROM table`。 每當資料表因 INSERT 或 DELETE 作業而引發觸發程序時，「系統監視器」計數器就會自動更新。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **User Settable** object.  
  
|SQL Server User Settable 計數器|描述|  
|---------------------------------------|-----------------|  
|**[資料集屬性]**|**User Settable** 物件包含查詢計數器。 使用者可設定查詢物件內的 **User counter** 。|  
  
 下表描述 **Query** 計數器的 **執行個體** 。  
  
|Query 計數器執行個體|描述|  
|-----------------------------|-----------------|  
|**User counter 1**|使用 **sp_user_counter1**來定義。|  
|**使用者計數器 2**|使用 **sp_user_counter2**來定義。|  
|**使用者計數器 3**|使用 **sp_user_counter3**來定義。|  
|…||  
|**User counter 10**|使用 **sp_user_counter10**來定義。|  
  
 若要使用使用者計數器預存程序，只要從您自己的應用程式執行它們，並且以一個整數參數代表計數器的新數值。 例如若要將 **User counter 1** 設成數值 10，可執行下列的 Transact-SQL 陳述式：  
  
```  
EXECUTE sp_user_counter1 10  
```  
  
 可呼叫使用者計數器預存程序的位置和呼叫其他預存程序的位置一樣，像是您自己的預存程序。 例如，您可以建立下列的預存程序，計算自從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體啟動之後的連接數和嘗試連接數。  
  
```  
DROP PROC My_Proc  
GO  
CREATE PROC My_Proc  
AS   
   EXECUTE sp_user_counter1 @@CONNECTIONS  
GO  
```  
  
 @@CONNECTIONS 函式可傳回自從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體啟動之後的連接數或嘗試連接數。 此數值將傳至 **sp_user_counter1** 預存程序作為參數。  
  
> [!IMPORTANT]  
>  盡量讓定義於使用者計數器預存程序的查詢越簡單越好。 執行大量排序或雜湊作業的記憶體密集查詢，或是執行大量 I/O 的查詢，都需要很多資源才能執行，所以可能影響效能。  
  
## <a name="permissions"></a>Permissions  
 **sp_user_counter** 適用於所有使用者，但可以由任何查詢計數器來限制。  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
