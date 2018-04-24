---
title: Execute 方法 （ADO 連接） |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 05d1df49596da99bc98fba9cef7999772ea78f40
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="execute-method-ado-connection"></a>Execute 方法 （ADO 連接）
執行指定的查詢、 SQL 陳述式、 預存程序或提供者特有的文字。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)物件參考。  
  
#### <a name="parameters"></a>參數  
 *CommandText*  
 A**字串**包含 SQL 陳述式、 預存程序、 URL 或提供者特有的文字執行的值。 **選擇性地**，如果提供者是 SQL 注意，可以但僅限於使用資料表名稱。 例如，如果資料表名稱的 「 客戶 」 會使用，ADO 會自動在前面加上表單，並傳遞 「 選取 * 從客戶 」 的標準 SQL Select 語法為[!INCLUDE[tsql](../../../includes/tsql_md.md)]陳述式的提供者。  
  
 *RecordsAffected*  
 選擇性。 A**長**變數提供者傳回的作業影響的記錄數目。  
  
 *選項。*  
 選擇性。 A**長**值，指出提供者應該如何評估 CommandText 引數。 可以是下列其中一個或多個的位元遮罩[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)或[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值。  
  
 **請注意**使用**的執行方式**值**adExecuteNoRecords**來改善效能，藉由減少內部處理以及您移植從 Visual Basic 6.0 的應用程式。  
  
 請勿使用**adExecuteStream**與**Execute**方法**連接**物件。  
  
 請勿使用 Execute 與 adCmdFile 或 adCmdTableDirect CommandTypeEnum 值。 這些值只用於做為選項與[Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)和[Requery 方法](../../../ado/reference/ado-api/requery-method.md)方法**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**Execute**方法[連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)物件執行任何您傳遞給方法的 CommandText 引數中指定的連接的查詢。 如果 CommandText 引數會指定傳回資料列的查詢，執行會產生任何結果會儲存在新**資料錄集**物件。 如果命令不是傳回的結果 （例如，SQL 更新查詢） 提供者會傳回**Nothing**只要選項**adExecuteNoRecords**指定; 否則執行傳回關閉**資料錄集**。  
  
 傳回**資料錄集**物件永遠是唯讀、 順向資料指標。 如果您需要**資料錄集**物件更多的功能，請先建立**資料錄集**物件具有所需的屬性設定，然後使用**資料錄集**物件的[Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法來執行查詢並傳回所需的資料指標類型。  
  
 內容*CommandText*引數的提供者特有的而且可以是標準 SQL 語法或任何提供者支援的特殊命令格式。  
  
 這項作業結束時，將會發出 ExecuteComplete 事件。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
