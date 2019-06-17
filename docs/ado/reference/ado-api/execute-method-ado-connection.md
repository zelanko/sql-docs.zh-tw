---
title: Execute 方法 (ADO Connection) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0489bb43ee3b41ebf4334da0d6b8045e117acc39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695372"
---
# <a name="execute-method-ado-connection"></a>Execute 方法 (ADO Connection)
執行指定的查詢，SQL 陳述式、 預存程序或提供者特定的文字。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)物件參考。  
  
#### <a name="parameters"></a>參數  
 *CommandText*  
 A**字串**包含 SQL 陳述式、 預存程序、 URL 或提供者特定文字執行的值。 **選擇性地**，如果提供者是 SQL 知道，可以但僅限於使用資料表名稱。 例如，如果資料表名稱的 「 客戶 」 會使用，ADO 會自動在前面加上形成，並傳遞 「 選取 * 從客戶 」 的標準 SQL Select 語法為[!INCLUDE[tsql](../../../includes/tsql-md.md)]給提供者的陳述式。  
  
 *RecordsAffected*  
 選擇性。 A**長**變數提供者所傳回的作業影響的記錄數目。  
  
 *選項。*  
 選擇性。 A**長**值，指出提供者應該如何評估 CommandText 引數。 可以是下列其中一個或多個的位元遮罩[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或是[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值。  
  
 **附註**使用**的執行方式**值**adExecuteNoRecords**來提升效能，藉由減少內部處理，以及您要移植從 Visual Basic 6.0 的應用程式。  
  
 請勿使用**adExecuteStream**具有**Execute**方法**連接**物件。  
  
 請勿使用 Execute 時使用 adCmdFile 或 adCmdTableDirect CommandTypeEnum 值。 這些值只可用來當做選項搭配[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)並[Requery 方法](../../../ado/reference/ado-api/requery-method.md)方法**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**Execute**方法[連線物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)物件執行任何您傳遞至 CommandText 引數中的方法指定的連接的查詢。 如果 CommandText 引數會指定傳回資料列的查詢，執行會產生任何結果會儲存在新**資料錄集**物件。 如果命令不會用來傳回結果 （例如，SQL 更新查詢） 提供者會傳回**Nothing**只要選項**adExecuteNoRecords**指定，否則執行傳回關閉**資料錄集**。  
  
 傳回**資料錄集**物件永遠是唯讀、 順向資料指標。 如果您需要**Recordset**物件更多的功能，請先建立**資料錄集**物件的所需的屬性設定，然後使用**資料錄集**物件的[Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法來執行查詢並傳回所需的資料指標類型。  
  
 內容*CommandText*引數是提供者特定的而且可以是標準 SQL 語法或任何提供者支援的特殊命令格式。  
  
 這項作業結束時，就會發出 ExecuteComplete 事件。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
