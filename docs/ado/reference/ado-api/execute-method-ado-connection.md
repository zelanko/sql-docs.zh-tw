---
title: Execute 方法（ADO Connection） |Microsoft Docs
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
ms.openlocfilehash: c2b07bb18aab0cde13a82540226fa477c306f268
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755099"
---
# <a name="execute-method-ado-connection"></a>Execute 方法 (ADO Connection)
執行指定的查詢、SQL 語句、預存程式或提供者特定的文字。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)物件參考。  
  
#### <a name="parameters"></a>參數  
 *CommandText*  
 **字串**值，其中包含要執行的 SQL 語句、預存程式、URL 或提供者特定的文字。 **（選擇性**）只有在提供者為 SQL 感知時，才可以使用資料表名稱。 例如，如果使用「Customers」資料表名稱，ADO 就會自動加上標準 SQL Select 語法來形成，並將「SELECT * FROM Customers」當做語句傳遞 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 給提供者。  
  
 *RecordsAffected*  
 選擇性。 **長**變數，提供者會傳回作業所影響的記錄數目。  
  
 *選項*  
 選擇性。 指出提供者應該如何評估 CommandText 引數的**Long**值。 可以是一個或多個[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)值的位元遮罩。  
  
 **注意**使用**ExecuteOptionEnum**值**adExecuteNoRecords**可將內部處理和從 Visual Basic 6.0 移植的應用程式降至最低，以改善效能。  
  
 請勿將**adExecuteStream**與**Connection**物件的**Execute**方法搭配使用。  
  
 請勿將 adCmdFile 或 adCmdTableDirect 的 CommandTypeEnum 值與 Execute 搭配使用。 這些值只能當做選項，使用**記錄集**的[OPEN 方法（ADO Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)和[Requery 方法](../../../ado/reference/ado-api/requery-method.md)方法。  
  
## <a name="remarks"></a>備註  
 在[Connection 物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)物件上使用**Execute**方法，會執行您在指定連接上的 CommandText 引數中傳遞至方法的任何查詢。 如果 CommandText 引數指定資料列傳回查詢，執行所產生的任何結果都會儲存在新的**記錄集**物件中。 如果命令不是用來傳回結果（例如，SQL UPDATE 查詢），則只要指定選項**adExecuteNoRecords** ，提供者就不會傳回**任何內容**。否則，Execute 會傳回封閉的**記錄集**。  
  
 傳回的**記錄集**物件一律為唯讀、順向資料指標。 如果您需要具有更多功能的**記錄集**物件，請先使用所需的屬性設定建立**記錄集**物件，然後使用**Recordset**物件的[Open 方法（ADO recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法來執行查詢，並傳回所需的資料指標類型。  
  
 *CommandText*引數的內容是提供者所特有，可以是標準 SQL 語法或提供者支援的任何特殊命令格式。  
  
 當此作業結束時，將會發出 ExecuteComplete 事件。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
