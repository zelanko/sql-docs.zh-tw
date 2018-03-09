---
title: "Execute 方法 （ADO 命令中） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7f16d3c01fb219bdbe7f52bbc39d3c410b5de918
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="execute-method-ado-command"></a>Execute 方法 （ADO 命令中）
執行查詢、 SQL 陳述式或預存程序中指定[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性[命令物件](../../../ado/reference/ado-api/command-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件參考、 資料流，或**Nothing**。  
  
#### <a name="parameters"></a>參數  
 *RecordsAffected*  
 選擇性。 A**長**變數提供者傳回的作業影響的記錄數目。 *RecordsAffected*參數只適用於執行查詢或預存程序。 *RecordsAffected*不會傳回的結果傳回查詢或預存程序所傳回的記錄數目。 若要取得這項資訊，請使用[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)屬性。 **Execute**方法不會傳回正確的資訊與搭配使用時**adAsyncExecute**，只要時以非同步方式執行命令，因為受影響的記錄數目可能還不會知道在此方法會傳回的時間。  
  
 *參數*  
 選擇性。 A **Variant**搭配輸入的字串或資料流中指定的參數值的陣列**CommandText**或**CommandStream**。 （輸出參數不會傳回正確的值，這個引數傳遞時）。  
  
 *選項。*  
 選擇性。 A**長**值，指出提供者應該如何評估[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。 可以是所使用的位元遮罩值[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)及/或[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值。 例如，您可以使用**adCmdText**和**adExecuteNoRecords**組合，如果您想要評估的值的 ADO **CommandText**屬性做為文字，並表示命令應該捨棄，並不會傳回執行命令文字時，可能會產生任何記錄。  
  
> [!NOTE]
>  使用**的執行方式**值**adExecuteNoRecords**來改善效能，藉由減少內部處理。 如果**adExecuteStream**已指定選項**adAsyncFetch**和**adAsynchFetchNonBlocking**都會被忽略。 請勿使用**CommandTypeEnum**值**adCmdFile**或**adCmdTableDirect**與**Execute**。 這些值只用於做為選項與[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)和[Requery](../../../ado/reference/ado-api/requery-method.md)方法**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**Execute**方法**命令**物件執行指定的查詢**CommandText**屬性或**CommandStream**物件的屬性。  
  
 結果會傳回**資料錄集**（依預設） 或資料流的二進位資訊。 若要取得的二進位資料流，請指定**adExecuteStream**中*選項*，然後藉由設定中提供的資料流**Command.Properties （「 輸出資料流 」）**。 ADO**資料流**物件可以指定要接收結果，或您可以指定另一個資料流物件，例如 IIS 回應物件。 如果沒有資料流之前先呼叫指定**Execute**與**adExecuteStream**，就會發生錯誤。 從傳回資料流的位置**Execute**是特定提供者。  
  
 如果命令不是傳回的結果 （例如，SQL 更新查詢） 提供者會傳回**Nothing**只要選項**adExecuteNoRecords**指定; 否則執行傳回關閉**資料錄集**。 某些應用程式語言可讓您忽略這個傳回值，如果沒有**資料錄集**想要使用。  
  
 **執行**如果使用者指定的值就會引發錯誤**CommandStream**時**CommandType**是**adCmdStoredProc**， **adCmdTable**，或**adCmdTableDirect**。  
  
 如果查詢包含參數，目前值**命令**物件的參數可用，除非您覆寫這些參數的值通過，但與**Execute**呼叫。 可以省略的一些參數的新值，呼叫時覆寫的參數子集**Execute**方法。 您可以在其中指定參數的順序是在其中的方法將它們傳送的相同順序。 例如，如果還有四個 （或以上） 的參數，而且您想要將新的值，只有第一個和第四個參數傳遞，您可以傳遞`Array(var1,,,var4)`為*參數*引數。  
  
> [!NOTE]
>  輸出參數不會傳回正確的值時傳入*參數*引數。  
  
 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)結束時，這項作業時，就會發出事件。  
  
> [!NOTE]
>  當發出命令包含 Url，使用 http 配置將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [執行，請重新查詢，並清除方法範例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [執行，請重新查詢，並清除方法範例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [執行，請重新查詢，並清除方法範例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream 屬性 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute 方法 （ADO 連接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete 事件 (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
