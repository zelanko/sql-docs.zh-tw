---
description: Execute 方法 (ADO 命令)
title: " (ADO 命令) 的 Execute 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
author: rothja
ms.author: jroth
ms.openlocfilehash: b33ada4ce6ac53c1caafbec80c19d1fd31deb6ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443890"
---
# <a name="execute-method-ado-command"></a>Execute 方法 (ADO 命令)
執行[命令物件](../../../ado/reference/ado-api/command-object-ado.md)的[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性中指定的查詢、SQL 語句或預存程式。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件參考、資料流程或 **Nothing**。  
  
#### <a name="parameters"></a>參數  
 *RecordsAffected*  
 選擇性。 **長**變數，提供者會傳回作業受影響的記錄數目。 *RecordsAffected*參數僅適用于動作查詢或預存程式。 *RecordsAffected* 不會傳回結果傳回的查詢或預存程式所傳回的記錄數目。 若要取得此資訊，請使用 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) 屬性。 與**adAsyncExecute**搭配使用時， **Execute**方法不會傳回正確的資訊，只是因為以非同步方式執行命令時，受影響的記錄數目在方法傳回時可能還不知道。  
  
 *參數*  
 選擇性。 參數值的 **Variant** 陣列，搭配 **CommandText** 或 **CommandStream**中指定的輸入字串或資料流程使用。 在這個引數中傳遞時， (輸出參數不會傳回正確的值。 )   
  
 *選項*  
 選擇性。 **Long**值，指出提供者應該如何評估[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[命令](../../../ado/reference/ado-api/command-object-ado.md)物件的[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性。 可以是使用 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 和/或 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 值所建立的位元遮罩值。 例如，如果您想要讓 ADO 將**CommandText**屬性的值評估為文字，則可以使用**adCmdText**和**adExecuteNoRecords** ，並指出命令應該捨棄，且不會傳回命令文字執行時可能產生的任何記錄。  
  
> [!NOTE]
>  您可以使用 **ExecuteOptionEnum** 值 **adExecuteNoRecords** ，藉由最小化內部處理來改善效能。 如果指定了 **adExecuteStream** ，則會忽略 **adAsyncFetch** 和 **adAsynchFetchNonBlocking** 選項。 請勿搭配**Execute**使用**adCmdFile**或**adCmdTableDirect**的**CommandTypeEnum**值。 這些值只能當做選項來使用**記錄集**的[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)和重新[查詢](../../../ado/reference/ado-api/requery-method.md)方法。  
  
## <a name="remarks"></a>備註  
 在**命令**物件上使用**Execute**方法會執行物件的**CommandText**屬性或**CommandStream**屬性中指定的查詢。  
  
 根據預設，結果會在 **記錄集中** 傳回 () 或作為二進位資訊的資料流程。 若要取得二進位資料流程，請在 [*選項*] 中指定**adExecuteStream** ，然後在 **[輸出資料流程] ) **中設定命令以提供資料流程 (。 您可以指定 ADO **資料流程** 物件來接收結果，也可以指定其他資料流程物件（例如 IIS 回應物件）。 如果在使用**adExecuteStream**呼叫**Execute**之前未指定任何資料流程，就會發生錯誤。 從 **Execute** 傳回的資料流程位置是提供者特有的。  
  
 如果命令並非用來傳回結果 (例如，SQL UPDATE 查詢) 提供者只要指定選項**adExecuteNoRecords** ，就不會傳回**任何**專案。否則，Execute 會傳回已關閉的**記錄集**。 某些應用程式語言可讓您在沒有任何 **記錄集** 時，忽略此傳回值。  
  
 當**CommandType**是**adCmdStoredProc**、 **adCmdTable**或**adCmdTableDirect**時，如果使用者指定**CommandStream**的值，**執行**就會引發錯誤。  
  
 如果查詢具有參數，除非您以**Execute**呼叫傳遞的參數值覆寫這些參數，否則會使用**命令**物件參數的目前值。 呼叫 **Execute** 方法時，您可以省略某些參數的新值，藉以覆寫參數的子集。 您指定參數的順序與方法傳遞這些參數的順序相同。 例如，如果有四個 (或多個) 的參數，而且您只想要傳遞第一個和第四個參數的新值，則會傳遞 `Array(var1,,,var4)` 做為 *參數* 引數。  
  
> [!NOTE]
>  輸出參數在 *參數* 引數中傳遞時，不會傳回正確的值。  
  
 當此作業結束時，將會發出 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) 事件。  
  
> [!NOTE]
>  發出包含 Url 的命令時，使用 HTTP 配置的命令會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的 Execute、Requery 和 Clear 方法範例) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery 和 Clear 方法範例 (VBScript) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery 和 Clear 方法範例 (VC + +) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [ (ADO) 的 CommandStream 屬性 ](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [ (ADO) 的 CommandText 屬性 ](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [ (ADO 連接) 的 Execute 方法 ](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete 事件 (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
