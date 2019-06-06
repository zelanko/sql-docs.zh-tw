---
title: NextRecordset 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 33cc979e0a3af9b684899cf7563573fd6ac8dadd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707274"
---
# <a name="nextrecordset-method-ado"></a>NextRecordset 方法 (ADO)
清除目前[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件，並傳回下一步**資料錄集**前移透過一系列的命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**資料錄集**物件。 在語法模型中， *recordset1*並*recordset2*可以是相同**資料錄集**物件，或者您可以使用不同的物件。 當使用個別**資料錄集**物件，重設**ActiveConnection**原始屬性**資料錄集**(*recordset1*)之後**NextRecordset**已呼叫會產生錯誤。  
  
#### <a name="parameters"></a>參數  
 *RecordsAffected*  
 選擇性。 A**長**變數提供者會傳回目前的作業影響的記錄數目。  
  
> [!NOTE]
>  這個參數只會傳回作業; 所影響的記錄數目它不會用來產生 select 陳述式傳回的記錄計數**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**NextRecordset**方法，以傳回結果的複合命令陳述式中的下一個命令，或傳回多個結果的預存程序。 如果您開啟**資料錄集**物件會根據複合命令陳述式 (例如，"選取\*從 table1;選取\*從 table2 」) 使用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法[命令](../../../ado/reference/ado-api/command-object-ado.md)或[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**資料錄集**，ADO 執行第一個命令，並傳回結果*資料錄集*。 若要存取之陳述式中的後續命令的結果，請呼叫**NextRecordset**方法。  
  
 只要有其他結果，**資料錄集**包含複合陳述式不在中斷連線，或可跨處理序界限封送處理**NextRecordset**方法將繼續傳回**資料錄集**物件。 如果傳回的資料列的命令執行成功，但會傳回任何記錄，傳回**資料錄集**物件將會開啟但空的。 在此情況下，藉由確認測試[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)並[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性都 **，則為 True**。 如果非資料列傳回命令執行成功，會傳回**Recordset**物件將會關閉，您可以藉由測試確認[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性**資料錄集**. 有沒有更多的結果，當*資料錄集*將會設定為*Nothing*。  
  
 **NextRecordset**方法並不適用於已中斷連接**Recordset**物件，其中[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)已設為**Nothing**(Microsoft Visual Basic 中) 或 NULL （在其他語言）。  
  
 在立即更新模式中進行編輯時，呼叫**NextRecordset**方法會產生錯誤; 呼叫[更新](../../../ado/reference/ado-api/update-method.md)或是[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法第一次。  
  
 若要傳入的複合陳述式中的多個命令的參數，來填入[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合，或藉由傳遞陣列與原始**開啟**或是**Execute**呼叫時，參數必須在其對應的命令，命令序列中相同的順序在集合或陣列。 您必須完成所有結果都讀取前都讀取輸出參數值。  
  
 您的 OLE DB 提供者會決定在複合陳述式中的每個命令執行時。 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，比方說，收到的複合陳述式批次中執行所有命令。 產生**資料錄集**當您呼叫時，只會傳回**NextRecordset**。  
  
 不過，其他提供者可能會執行下一個命令陳述式中稱為 NextRecordset 之後，才。 對於這些提供者，如果您明確地關閉**資料錄集**ADO 永遠不會執行剩餘的命令物件之前先逐步完成整個命令陳述式。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [NextRecordset 方法範例 (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [NextRecordset 方法範例 (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
