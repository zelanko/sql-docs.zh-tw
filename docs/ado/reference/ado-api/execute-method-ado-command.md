---
title: Execute 方法 (ADO Command) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9508b85bc73ebbec82ad7d3bea5af5148d7c674
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184804"
---
# <a name="execute-method-ado-command"></a>Execute 方法 (ADO 命令)
執行查詢、 SQL 陳述式或預存程序中指定[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或是[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性[命令物件](../../../ado/reference/ado-api/command-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件的參考、 資料流，或**Nothing**。  
  
#### <a name="parameters"></a>參數  
 *RecordsAffected*  
 選擇性。 A**長**變數提供者所傳回的作業影響的記錄數目。 *RecordsAffected*參數僅適用於動作的查詢或預存程序。 *RecordsAffected*不會傳回的結果傳回查詢或預存程序所傳回的記錄數目。 若要取得這項資訊，請使用[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)屬性。 **Execute**方法將不會傳回正確的資訊搭配使用時**adAsyncExecute**，只要時以非同步方式執行命令，因為受影響的記錄數目可能不明在此方法會傳回的時間。  
  
 *參數*  
 選擇性。 A **Variant**搭配的輸入的字串或資料流中所指定的參數值的陣列**CommandText**或是**CommandStream**。 （輸出參數不會傳回正確的值，這個引數傳遞時）。  
  
 *選項。*  
 選擇性。 A**長**值，指出提供者應該如何評估[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。 可以是使用位元遮罩值[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)及/或[的執行方式](../../../ado/reference/ado-api/executeoptionenum.md)值。 比方說，您可以使用**adCmdText**並**adExecuteNoRecords**組合，如果您要評估的值的 ADO **CommandText**屬性為文字，及指出命令應該捨棄，並不會傳回執行命令文字時，可能會產生任何記錄。  
  
> [!NOTE]
>  使用**的執行方式**值**adExecuteNoRecords**內部處理，進而改善效能。 如果**adExecuteStream**已指定選項**adAsyncFetch**並**adAsynchFetchNonBlocking**都會被忽略。 請勿使用**CommandTypeEnum**的值**adCmdFile**或是**adCmdTableDirect**具有**Execute**。 這些值只可用來當做選項搭配[開放](../../../ado/reference/ado-api/open-method-ado-recordset.md)並[Requery](../../../ado/reference/ado-api/requery-method.md)方法**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**Execute**方法**命令**物件執行查詢中指定**CommandText**屬性或**CommandStream**物件的屬性。  
  
 結果會傳回**資料錄集**（依預設） 或資料流的二進位資訊。 若要取得二進位資料流，請指定**adExecuteStream**中*選項*，然後藉由設定中提供的資料流**Command.Properties (「 輸出 Stream")**。 ADO **Stream**物件可以指定要接收結果，或者可以指定另一個資料流物件，例如 IIS 回應物件。 如果沒有資料流指定再呼叫**Execute**具有**adExecuteStream**，就會發生錯誤。 在傳回時從資料流的位置**Execute**是特定提供者。  
  
 如果命令不會用來傳回結果 （例如，SQL 更新查詢） 提供者會傳回**Nothing**只要選項**adExecuteNoRecords**指定，否則執行傳回關閉**資料錄集**。 某些應用程式語言，可讓您忽略此傳回值，如果沒有**資料錄集**想要使用。  
  
 **執行**會引發錯誤，如果使用者指定的值**CommandStream**當**CommandType**是**adCmdStoredProc**， **adCmdTable**，或**adCmdTableDirect**。  
  
 如果查詢有參數，目前值**命令**除非您覆寫這些與傳遞的參數值，會使用物件的參數**Execute**呼叫。 您可以藉由省略的部分參數的新值，就呼叫時覆寫參數的子集**Execute**方法。 您可以在其中指定參數的順序是在其中，方法會將它們的順序相同。 例如，如果還有四個 （含） 以上的參數，而且您想要將新的值，只有第一個和第四個參數傳遞，您會傳遞`Array(var1,,,var4)`作為*參數*引數。  
  
> [!NOTE]
>  輸出參數將不會傳回正確的值，在傳入時會*參數*引數。  
  
 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)這項作業結束時，就會發出事件。  
  
> [!NOTE]
>  當發出包含 Url 的命令，使用 http 配置會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Execute、 Requery 和 Clear 方法範例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、 Requery 和 Clear 方法範例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、 Requery 和 Clear 方法範例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream 屬性 (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute 方法 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete 事件 (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
