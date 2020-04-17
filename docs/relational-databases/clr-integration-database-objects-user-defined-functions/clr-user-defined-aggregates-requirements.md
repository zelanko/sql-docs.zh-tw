---
title: CLR 使用者定義的聚合要求 |微軟文件
description: SQL Server CLR 集成允許您在託管代碼中創建自定義聚合函數。 它們必須實現所需的聚合協定。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dd27cf3751400d3902ddd4199daee8aeef78b80
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487931"
---
# <a name="clr-user-defined-aggregates---requirements"></a>CLR 使用者定義彙總 - 需求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 Common Language Runtime (CLR) 組件中的類型只要實作需要的彙總合約，就可以註冊為使用者定義彙總函式。 此協定由**SqlUser 定義聚合**屬性和聚合協定方法組成。 聚合協定包括保存聚合中間狀態的機制,以及累積新值的機制,該機制包括四種方法 **:Init、****累積**、**合併**和**終止**。 滿足這些要求后,您將能夠充分利用中的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶定義的聚合。 本主題的下列章節提供關於如何建立和使用使用者定義彙總的其他相關資訊。 例如,請參閱呼叫[CLR 使用者定義的聚合函數](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)。  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 有關詳細資訊,請參閱[SqlUser 定義的集合屬性](https://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="aggregation-methods"></a>彙總方法  
 註冊為使用者定義彙總的類別應該會支援下列執行個體方法。 查詢處理器用以計算彙總的方法：  
  
|方法|語法|描述|  
|------------|------------|-----------------|  
|**Init**|`public void Init();`|查詢處理器使用這個方法將彙總計算初始化。 這個方法針對查詢處理器正在彙總的每個群組叫用一次。 查詢處理器為了計算多個群組彙總，可能選擇重複使用彙總類別之相同執行個體。 **Init**方法應根據需要執行此實例以前使用的任何清理,並使其能夠重新啟動新的聚合計算。|  
|**積累**|`public void Accumulate ( input-type value[, input-type value, ...]);`|代表函數參數的一個或多個參數。 *input_type*應是與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*input_sqltype*在**CREATE**聚合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語句中指定的本機數據類型等效的託管數據類型。 關於詳細資訊,請參閱映射[CLR 參數資料](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。<br /><br /> 如果是使用者定義型別 (UDT)，輸入類型則是 UDT 類型。 查詢處理器使用這個方法來累積彙總值。 在群組中正在彙總的每一個值都會叫用一次。 查詢處理器始終僅在在聚合類的給定實例上調用**Init**方法后才調用此方法。 這個方法的實作應該會更新執行個體的狀態，以反映傳入的引數值之累積狀況。|  
|**合併**|`public void Merge( udagg_class value);`|這個方法可用於將此彙總類別的其他執行個體與目前的執行個體合併。 查詢處理器使用這個方法合併多個不完全的彙總計算。|  
|**終止**|`public return_type Terminate();`|這個方法會完成彙總計算，並傳回彙總的結果。 *return_type*應為託管[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]數據類型,該類型與**CREATE 聚合**語句中指定的*return_sqltype*的託管等效。 *return_type*也可以是使用者定義的類型。|  
  
### <a name="table-valued-parameters"></a>資料表值參數  
 資料表值參數 (TVP) 是使用者定義資料表類型，會傳入到程序或函數中，提供有效的方式將資料的多個資料列傳遞到伺服器。 雖然 TVP 提供相似的功能給參數陣列，但是也提供更大的彈性和與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更緊密的整合。 它們也能夠協助您獲得更佳的效能。 TVP 也減少與伺服器之間的往返次數。 除了傳送多個要求到伺服器 (例如夾帶純量參數的清單)，資料能以 TVP 的形式傳送到伺服器。 使用者定義資料表類型無法以資料表值參數的形式傳遞到 Managed 預存程序或在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中執行的函數，也無法從該預存程序或函數傳回。 此外，TVP 也無法在內容連接範圍內使用。 但是，如果 TVP 用於非內容連接中，就可以在 Managed 預存程序或在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中所執行的函數裡與 SqlClient 使用。 該連接可連接至執行 Managed 程序或函數的相同伺服器。 有關 TVP 的詳細資訊,請參閱[使用表值參數&#40;資料庫引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|更新了**累積**方法的說明;它現在接受多個參數。|  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義類型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [叫用 CLR 使用者定義彙總函式](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
  
  
