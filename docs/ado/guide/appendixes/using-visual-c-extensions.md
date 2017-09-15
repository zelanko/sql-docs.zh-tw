---
title: "使用 Visual c + + 擴充功能 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 90ef5f49740a7e9e750ade714f0571f2642f0d47
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="visual-c-extensions"></a>Visual c + + 擴充功能
## <a name="the-iadorecordbinding-interface"></a>IADORecordBinding 介面
 Microsoft Visual c + + 擴充功能之 ADO 關聯或繫結欄位[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)C/c + + 變數的物件。 每當繫結的目前資料列**資料錄集**變更時中的所有繫結的欄位**資料錄集**會複製到 C/c + + 變數。 如有必要，複製的資料會轉換成 C/c + + 變數宣告的資料類型。

 **BindToRecordset**方法**IADORecordBinding**介面欄位繫結至 C/c + + 變數。 **AddNew**方法會將新的資料列加入繫結**資料錄集**。 **更新**方法填入新的資料列中的欄位**資料錄集**，或使用 C/c + + 變數的值更新現有的資料列中的欄位。

 **IADORecordBinding**介面由實作**資料錄集**物件。 您沒有編碼實作。

## <a name="binding-entries"></a>繫結項目
 Visual c + + 擴充功能，用於 ADO 的欄位對應[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)C/c + + 變數的物件。 欄位和變數之間的對應的定義就稱為*繫結項目*。 巨集提供數值、 固定長度和可變長度的資料繫結項目。 Visual c + + 擴充功能的類別，衍生類別中宣告的繫結項目和 C/c + + 變數**CADORecordBinding**。 **CADORecordBinding**類別在內部定義的繫結項目巨集。

 ADO 在內部將在這些巨集參數對應至 OLE DB **DBBINDING**結構，並建立 OLE DB**存取子**管理移動和資料欄位和變數之間轉換的物件。 OLE DB 定義為包含資料的三個部分： A*緩衝區*其中的資料會儲存;*狀態*，指出欄位是否已成功儲存在緩衝區或變數應該如何還原成欄位;和*長度*的資料。 (請參閱[取得和設定資料 (OLE DB)](http://msdn.microsoft.com/en-us/4369708b-c9fb-4d48-a321-bf949b41a369)在 OLE DB 程式設計人員參考中，如需詳細資訊。)

## <a name="header-file"></a>標頭檔
 若要針對 ADO 使用 Visual c + + 擴充功能的應用程式中包含下列檔案：

```
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>繫結資料錄集欄位

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>資料錄集欄位繫結至 C/c + + 變數

1.  建立衍生自類別**CADORecordBinding**類別。

2.  在衍生類別中，指定繫結項目和對應的 C/c + + 變數。 括號之間的繫結項目**BEGIN_ADO_BINDING**和**END_ADO_BINDING**巨集。 請勿終止使用逗號或分號的巨集。 每個巨集會自動指定適當的分隔符號。

     指定一個繫結項目，每個欄位對應至 C/c + + 變數。 使用適當的成員從**ADO_FIXED_LENGTH_ENTRY**， **ADO_NUMERIC_ENTRY**，或**ADO_VARIABLE_LENGTH_ENTRY**系列巨集。

3.  應用程式中建立衍生自類別的執行個體**CADORecordBinding**。 取得**IADORecordBinding**介面從**資料錄集**。 然後呼叫**BindToRecordset**繫結方法**資料錄集**C/c + + 變數的欄位。

 如需詳細資訊，請參閱[Visual c + + 擴充功能範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)。

## <a name="interface-methods"></a>介面方法
 **IADORecordBinding**介面有三個方法： **BindToRecordset**， **AddNew**，和**更新**。 每個方法的唯一引數是指向衍生自類別的執行個體的**CADORecordBinding**。 因此， **AddNew**和**更新**方法不能指定任何其 ADO 方法 namesakes 參數。

## <a name="syntax"></a>語法
 **BindToRecordset**方法相關聯**資料錄集**C/c + + 變數的欄位。

```
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew**方法會叫用其 namesake，ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，以加入新的資料列**資料錄集**。

```
AddNew(CADORecordBinding *binding)
```

 **更新**方法會叫用其 namesake，ADO[更新](../../../ado/reference/ado-api/update-method.md)方法，來更新**資料錄集**。

```
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>繫結項目巨集
 繫結項目巨集會定義的關聯**資料錄集**欄位和變數。 開始與結束的巨集分隔繫結項目的集。

 系列的巨集可供固定長度的資料，例如**adDate**或**adBoolean**; 數值資料，例如**adTinyInt**， **adInteger**，或**adDouble**; 和可變長度資料，例如**adChar**， **adVarChar**或**adVarBinary**。 所有數字類型，除了**adVarNumeric**，也是固定長度類型。 每個家族有不同的參數集，因此您可以排除不感興趣的繫結資訊。

 如需詳細資訊，請參閱[附錄 a： 資料型別](http://msdn.microsoft.com/en-us/e3a0533a-2196-4eb0-a31e-92fe9556ada6)，OLE DB 程式設計人員參考。

### <a name="begin-binding-entries"></a>開始繫結項目
 **BEGIN_ADO_BINDING**(*類別*)

### <a name="fixed-length-data"></a>固定長度的資料
 **ADO_FIXED_LENGTH_ENTRY**(*序數、 資料型別、 緩衝區、 狀態 」 修改*)

 **ADO_FIXED_LENGTH_ENTRY2**(*序數、 資料型別，緩衝區，修改*)

### <a name="numeric-data"></a>數值資料
 **ADO_NUMERIC_ENTRY**(*序數、 資料型別、 緩衝區、 有效位數、 小數位數、 狀態 」 修改*)

 **ADO_NUMERIC_ENTRY2**(*序數、 資料型別、 緩衝區、 Precision，Scale，修改*)

### <a name="variable-length-data"></a>可變長度的資料
 **ADO_VARIABLE_LENGTH_ENTRY**(*序數、 資料型別、 緩衝區、 大小、 狀態、 長度、 修改*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*序數、 資料型別、 緩衝區、 大小、 狀態 」 修改*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*序數、 資料型別、 緩衝區、 大小、 長度、 修改*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*序數、 資料型別、 緩衝區大小，修改*)

### <a name="end-binding-entries"></a>結束繫結項目
 **END_ADO_BINDING**（)

|參數|Description|
|---------------|-----------------|
|*類別*|類別定義的繫結項目和 C/c + + 變數。|
|*Ordinal*|序號，從一個、 算起的**資料錄集**欄位對應至您的 C/c + + 變數。|
|*資料類型*|C/c + + 變數的對等的 ADO 資料類型 (請參閱[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)取得一份有效的資料類型)。 值**資料錄集**欄位會被轉換成這個資料類型，如有必要。|
|*緩衝區*|C/c + + 變數的名稱位置**資料錄集**欄位將會儲存。|
|*大小*|以位元組為單位的大小上限*緩衝區*。 如果*緩衝區*將包含可變長度字串，讓有終止零的空間。|
|*狀態*|會指出變數的名稱是否的內容*緩衝區*有效，以及是否要的欄位轉換*DataType*成功。<br /><br /> 最重要的兩個值，這個變數會**adFldOK**，這表示轉換是否成功; 和**adFldNull**，這表示欄位的值會是變數類型 VT_NULL 並不只是空的。<br /><br /> 可能值*狀態*會列在下一個資料表中，「 狀態值 」。|
|*修改*|布林值旗標。如果為 TRUE，表示允許 ADO 來更新對應**資料錄集**欄位中包含的值取代*緩衝區*。<br /><br /> 設定布林值*修改*為了讓 ADO 更新繫結的欄位，則為 TRUE 和 FALSE，如果您想要檢查該欄位，但無法變更它的參數。|
|*有效位數*|可以用來表示數值變數的數字的數目。|
|*小數位數*|中的數值變數的小數位數。|
|*長度*|將包含在資料的實際長度的四個位元組變數名稱*緩衝區*。|

## <a name="status-values"></a>狀態值
 值*狀態*變數會指出欄位是否已成功地複製到變數。

 設定資料時,*狀態*可能會設定為**adFldNull**表示**資料錄集**梇糔飶為 null。

|常數|值|Description|
|--------------|-----------|-----------------|
|**adFldOK**|0|傳回非 null 的欄位值。|
|**adFldBadAccessor**|1|繫結無效。|
|**adFldCantConvertValue**|2|由於符號不符或資料溢位以外的原因而無法轉換值。|
|**adFldNull**|3|當取得某個欄位時，表示傳回了 null 值。<br /><br /> 當設定的欄位，表示欄位應設**NULL**欄位無法編碼時**NULL**本身 （例如，字元陣列或整數）。|
|**adFldTruncated**|4|已截斷可變長度的資料或數字。|
|**adFldSignMismatch**|5|值為 signed，而不帶正負號的變數資料類型。|
|**adFldDataOverFlow**|6|值是大於可儲存在變數資料類型。|
|**adFldCantCreate**|7|未知的資料行類型和欄位已經開啟。|
|**adFldUnavailable**|8|無法判斷欄位值 — 例如，在新的、 未指派的欄位，而且沒有預設值。|
|**adFldPermissionDenied**|9|在更新時，沒有寫入資料的權限。|
|**adFldIntegrityViolation**|10|更新時，欄位值違反資料行的完整性。|
|**adFldSchemaViolation**|11|更新時，欄位值違反資料行的結構描述。|
|**adFldBadStatus**|12|在更新時，無效的狀態參數。|
|**adFldDefault**|13|更新時，使用預設值。|

## <a name="see-also"></a>另請參閱
 [Visual c + + 擴充功能範例](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual c + + 擴充功能的標頭](../../../ado/guide/appendixes/visual-c-extensions-header.md)

