---
title: CLR 使用者定義匯總的需求 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 31b22b1dce53bb82f85ae946290024408d2facd3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874474"
---
# <a name="requirements-for-clr-user-defined-aggregates"></a>CLR 使用者定義彙總的需求
  在 Common Language Runtime (CLR) 組件中的類型只要實作需要的彙總合約，就可以註冊為使用者定義彙總函式。 此合約由 `SqlUserDefinedAggregate` 屬性及彙總合約方法組成。 彙總合約包括儲存彙總中繼狀態的機制，以及累積新值的機制，它是由四種方法組成：`Init`、`Accumulate`、`Merge` 和 `Terminate`。 當您符合這些需求時，您將能夠充分利用中[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的使用者定義匯總。 本主題的下列章節提供關於如何建立和使用使用者定義彙總的其他相關資訊。 如需範例，請參閱叫用[CLR 使用者定義彙總函式](clr-user-defined-aggregate-invoking-functions.md)。  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 如需詳細資訊，請參閱[SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="aggregation-methods"></a>彙總方法  
 註冊為使用者定義彙總的類別應該會支援下列執行個體方法。 查詢處理器用以計算彙總的方法：  
  
|方法|語法|描述|  
|------------|------------|-----------------|  
|`Init`|public void Init （）;|查詢處理器使用這個方法將彙總計算初始化。 這個方法針對查詢處理器正在彙總的每個群組叫用一次。 查詢處理器為了計算多個群組彙總，可能選擇重複使用彙總類別之相同執行個體。 
  `Init` 方法應該會視需要針對上次使用的此執行個體執行清除作業，並讓它重新啟動新的彙總計算。|  
|`Accumulate`|public void 累積（輸入類型值 [，輸入類型值，...]）;|代表函數參數的一個或多個參數。 *input_type* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]應該是 managed 資料類型，相當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]于`CREATE AGGREGATE`語句中*input_sqltype*所指定的原生資料類型。 如需詳細資訊，請參閱[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。<br /><br /> 如果是使用者定義型別 (UDT)，輸入類型則是 UDT 類型。 查詢處理器使用這個方法來累積彙總值。 在群組中正在彙總的每一個值都會叫用一次。 查詢處理器一定只會在給定的彙總類別執行個體上呼叫 `Init` 方法後才會呼叫這些值。 這個方法的實作應該會更新執行個體的狀態，以反映傳入的引數值之累積狀況。|  
|`Merge`|public void Merge （udagg_class 值）;|這個方法可用於將此彙總類別的其他執行個體與目前的執行個體合併。 查詢處理器使用這個方法合併多個不完全的彙總計算。|  
|`Terminate`|public return_type Terminate （）;|這個方法會完成彙總計算，並傳回彙總的結果。 *Return_type*應該是 managed [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型，這是`CREATE AGGREGATE`語句中所指定*return_sqltype*的 managed 對應項。 *Return_type*也可以是使用者定義型別。|  
  
### <a name="table-valued-parameters"></a>資料表值參數  
 資料表值參數 (TVP) 是使用者定義資料表類型，會傳入到程序或函數中，提供有效的方式將資料的多個資料列傳遞到伺服器。 雖然 TVP 提供相似的功能給參數陣列，但是也提供更大的彈性和與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更緊密的整合。 它們也能夠協助您獲得更佳的效能。 TVP 也減少與伺服器之間的往返次數。 除了傳送多個要求到伺服器 (例如夾帶純量參數的清單)，資料能以 TVP 的形式傳送到伺服器。 使用者定義資料表類型無法以資料表值參數的形式傳遞到 Managed 預存程序或在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中執行的函數，也無法從該預存程序或函數傳回。 此外，TVP 也無法在內容連接範圍內使用。 但是，如果 TVP 用於非內容連接中，就可以在 Managed 預存程序或在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中所執行的函數裡與 SqlClient 使用。 該連接可連接至執行 Managed 程序或函數的相同伺服器。 如需 Tvp 的詳細資訊，請參閱[使用資料表值參數 &#40;資料庫引擎&#41;](../tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|已更新 `Accumulate` 方法的說明；該方法現在接受一個以上的參數。|  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義類型](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [叫用 CLR 使用者定義彙總函式](clr-user-defined-aggregate-invoking-functions.md)  
  
  
