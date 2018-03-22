---
title: NextRecordset 方法 (ADO) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4e0e38fc9c01a65916d7979fddfae929d43acf1
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="nextrecordset-method-ado"></a>NextRecordset 方法 (ADO)
清除目前[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，並傳回下一個**資料錄集**往前移透過一系列的命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**資料錄集**物件。 在語法模型中， *recordset1*和*recordset2*可以是相同**資料錄集**物件，或者您可以使用不同的物件。 當使用個別**資料錄集**物件，重設**ActiveConnection**原始屬性**資料錄集**(*recordset1*)之後**NextRecordset**已呼叫會產生錯誤。  
  
#### <a name="parameters"></a>參數  
 *RecordsAffected*  
 選擇性。 A**長**變數提供者會傳回目前的作業受到影響的記錄數目。  
  
> [!NOTE]
>  這個參數只會傳回受影響的作業; 記錄數目不會傳回記錄的計數從 select 陳述式，用來產生**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**NextRecordset**方法以傳回結果的複合命令陳述式中的下一個命令或預存程序傳回多個結果。 如果您開啟**資料錄集**複合命令陳述式為基礎的物件 (例如，「 選取\*從 table1;選取\*從 table2") 使用[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)方法[命令](../../../ado/reference/ado-api/command-object-ado.md)或[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**資料錄集**，ADO 執行只有第一個命令，並傳回結果*資料錄集*。 若要存取之陳述式中的後續命令的結果，請呼叫**NextRecordset**方法。  
  
 只要有其他結果和**資料錄集**包含複合陳述式不在中斷連線，或可封送處理跨處理序界限**NextRecordset**方法將繼續傳回**資料錄集**物件。 如果傳回資料列的命令執行成功，但未傳回資料錄，傳回**資料錄集**物件將會開啟但空的。 測試此案例藉由確認[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)和[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性都**True**。 如果未傳回資料列的命令執行成功，傳回**資料錄集**物件將會關閉，您可以藉由測試來確認其[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性**資料錄集**. 當沒有其他結果時，*資料錄集*會設定為*Nothing*。  
  
 **NextRecordset**方法並不適用於已中斷連線**資料錄集**物件，其中[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)已設定為**Nothing**(在 Microsoft Visual Basic) 或 NULL （在其他語言）。  
  
 如果編輯正在進行立即更新模式中，呼叫**NextRecordset**方法會產生錯誤; 呼叫[更新](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法第一次。  
  
 複合陳述式中傳遞多個命令的參數，來填入[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合，或藉由傳遞陣列與原始**開啟**或**Execute**呼叫時，參數必須以陣列或集合中做為其對應的命令，命令序列中相同的順序。 您必須完成所有結果都讀取前都讀取輸出參數值。  
  
 您的 OLE DB 提供者會決定在複合陳述式中的每個命令執行時。 [Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)，例如，在收到複合陳述式批次中執行所有命令。 產生**資料錄集**會直接傳回，當您呼叫**NextRecordset**。  
  
 但是，其他提供者可能會執行下一個命令陳述式中呼叫 NextRecordset 之後，才。 對於這些提供者，如果您明確地關閉**資料錄集**ADO 絕不會執行其餘的命令之前逐步整個命令陳述式的物件。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [NextRecordset 方法範例 (VB)](../../../ado/reference/ado-api/nextrecordset-method-example-vb.md)   
 [NextRecordset 方法範例 (VC++)](../../../ado/reference/ado-api/nextrecordset-method-example-vc.md)   
