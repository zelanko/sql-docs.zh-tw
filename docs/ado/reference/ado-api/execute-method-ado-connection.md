---
description: Execute 方法 (ADO Connection)
title: " (ADO 連接) 的 Execute 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
author: rothja
ms.author: jroth
ms.openlocfilehash: 1acbdc4966f46d5e155dab3fac059568699d4727
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443910"
---
# <a name="execute-method-ado-connection"></a>Execute 方法 (ADO Connection)
執行指定的查詢、SQL 語句、預存程式或提供者特定的文字。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 [ (ADO) 物件參考的記錄集物件 ](../../../ado/reference/ado-api/recordset-object-ado.md) 。  
  
#### <a name="parameters"></a>參數  
 *CommandText*  
 **字串**值，包含要執行的 SQL 語句、預存程式、URL 或提供者特定的文字。 **（選擇性**）您可以使用資料表名稱，但僅限於提供者為 SQL 感知時。 例如，如果使用的是 "Customers" 資料表名稱，則 ADO 會自動在標準 SQL Select 語法前面加上 "SELECT * FROM Customers" 當做 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 語句傳遞給提供者。  
  
 *RecordsAffected*  
 選擇性。 **長**變數，提供者會傳回作業受影響的記錄數目。  
  
 *選項*  
 選擇性。 **Long**值，指出提供者應該如何評估 CommandText 引數。 可以是一個或多個 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 或 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 值的位元遮罩。  
  
 **注意** 使用 **ExecuteOptionEnum** 值 **adExecuteNoRecords** 可將內部處理和您從 Visual Basic 6.0 移植的應用程式降至最低，以改善效能。  
  
 請勿使用**adExecuteStream**搭配**連接**物件的**Execute**方法。  
  
 請勿搭配 Execute 使用 adCmdFile 或 adCmdTableDirect 的 CommandTypeEnum 值。 這些值只能當做具有 Open 方法的選項使用， [ (ADO 記錄集) ](../../../ado/reference/ado-api/open-method-ado-recordset.md)和[查詢](../../../ado/reference/ado-api/requery-method.md)**記錄集**的方法方法。  
  
## <a name="remarks"></a>備註  
 在連線物件上使用 **Execute** 方法 [ (ADO) ](../../../ado/reference/ado-api/connection-object-ado.md) 物件會執行您傳遞至指定連接上 CommandText 引數中之方法的任何查詢。 如果 CommandText 引數指定傳回資料列的查詢，則執行產生的任何結果都會儲存在新的 **記錄集** 物件中。 如果命令並非用來傳回結果 (例如，SQL UPDATE 查詢) 提供者只要指定選項**adExecuteNoRecords** ，就不會傳回**任何**專案。否則，Execute 會傳回已關閉的**記錄集**。  
  
 傳回的 **記錄集** 物件一律為唯讀、順向資料指標。 如果您需要具有更多功能的 **記錄集** 物件，請先使用所需的屬性設定來建立 **記錄集** 物件，然後使用 **記錄集** 物件的 [Open 方法 (ADO 記錄集) ](../../../ado/reference/ado-api/open-method-ado-recordset.md) 方法來執行查詢並傳回所需的資料指標類型。  
  
 *CommandText*引數的內容是提供者專屬的，而且可以是標準 SQL 語法或提供者所支援的任何特殊命令格式。  
  
 當此作業結束時，將會發出 ExecuteComplete 事件。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
