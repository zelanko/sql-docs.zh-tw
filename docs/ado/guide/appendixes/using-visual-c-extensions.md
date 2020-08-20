---
description: 使用 Visual C++ Extensions
title: 使用 Visual C++ 擴充功能 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ca7d66c7748658c5ba720b8664d824551da47bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453980"
---
# <a name="visual-c-extensions"></a>Visual C++ 擴充功能
## <a name="the-iadorecordbinding-interface"></a>IADORecordBinding 介面
 適用于 ADO 的 Microsoft Visual C++ 延伸模組會將 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件的欄位與 c/c + + 變數相關聯（或系結）。 每當系結 **記錄集** 的目前資料列變更時，就會將 **記錄集** 內的所有系結欄位複製到 C/c + + 變數。 必要時，複製的資料會轉換成 C/c + + 變數的宣告資料類型。

 **IADORecordBinding**介面的**BindToRecordset**方法會將欄位系結至 c/c + + 變數。 **AddNew**方法會將新的資料列加入至系結的**記錄集**。 **Update**方法會在**記錄集**的新資料列中填入欄位，或以 C/c + + 變數的值來更新現有資料列中的欄位。

 **IADORecordBinding**介面是由**記錄集**物件所執行。 您不需要自行撰寫程式碼。

## <a name="binding-entries"></a>繫結項目
 適用于 ADO 的 Visual C++ 延伸模組會將 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件的欄位對應至 c/c + + 變數。 欄位和變數之間的對應定義稱為系結 *專案*。 宏提供數值、固定長度和可變長度資料的系結專案。 系結專案和 C/c + + 變數是在衍生自 Visual C++ Extensions 類別 **CADORecordBinding**的類別中宣告。 **CADORecordBinding**類別是由系結專案宏在內部定義。

 ADO 會在內部將這些宏的參數對應至 OLE DB **DBBINDING** 結構，並建立 OLE DB **存取** 子物件來管理欄位和變數之間的資料移動和轉換。 OLE DB 定義的資料由三個部分組成：儲存資料的 *緩衝區* ;指出欄位是否成功儲存在緩衝區中，或如何將變數還原至欄位的 *狀態* 。以及資料的 *長度* 。 如需詳細資訊，請參閱 OLE DB 程式設計人員參考中的 [取得和設定資料 (OLE DB) ](https://msdn.microsoft.com/4369708b-c9fb-4d48-a321-bf949b41a369) (。 ) 

## <a name="header-file"></a>標頭檔案
 在您的應用程式中包含下列檔案，以便使用適用于 ADO 的 Visual C++ 延伸模組：

```cpp
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>系結記錄集欄位

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>將記錄集欄位系結至 C/c + + 變數

1.  建立衍生自 **CADORecordBinding** 類別的類別。

2.  在衍生類別中指定系結專案和對應的 C/c + + 變數。 在 **BEGIN_ADO_BINDING** 和 **END_ADO_BINDING** 宏之間的系結專案上括弧。 請勿以逗號或分號結束宏。 每個宏都會自動指定適當的分隔符號。

     針對每個要對應至 C/c + + 變數的欄位，指定一個系結專案。 使用來自 **ADO_FIXED_LENGTH_ENTRY**、 **ADO_NUMERIC_ENTRY**或 **ADO_VARIABLE_LENGTH_ENTRY** 系列宏的適當成員。

3.  在您的應用程式中，建立衍生自 **CADORecordBinding**之類別的實例。 從**記錄集**取得**IADORecordBinding**介面。 然後呼叫 **BindToRecordset** 方法，將 **記錄集** 欄位系結至 C/c + + 變數。

 如需詳細資訊，請參閱 [Visual C++ 擴充功能範例](../../../ado/guide/appendixes/visual-c-extensions-example.md)。

## <a name="interface-methods"></a>介面方法
 **IADORecordBinding**介面有三個方法： **BindToRecordset**、 **AddNew**和**Update**。 每個方法的唯一引數是衍生自 **CADORecordBinding**之類別實例的指標。 因此， **AddNew** 和 **Update** 方法無法指定其 ADO 方法 namesakes 的任何參數。

## <a name="syntax"></a>語法
 **BindToRecordset**方法會將**記錄集**欄位與 c/c + + 變數產生關聯。

```cpp
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew**方法會叫用其同名（ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法），以將新的資料列加入至**記錄集**。

```cpp
AddNew(CADORecordBinding *binding)
```

 **Update**方法會叫用其同名（ADO [Update](../../../ado/reference/ado-api/update-method.md)方法）來更新**記錄集**。

```cpp
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>繫結項目宏
 繫結項目宏會定義 **記錄集** 欄位和變數的關聯。 開始和結束宏會分隔一組系結專案。

 系統會為固定長度的資料（例如 **adDate** 或 **adBoolean**）提供宏系列;數值資料，例如 **adTinyInt**、 **adInteger**或 **adDouble**;和可變長度的資料，例如 **adChar**、 **adVarChar** 或 **adVarBinary**。 除了 **adVarNumeric**以外的所有數數值型別也是固定長度的類型。 每個系列都有一組不同的參數，因此您可以排除不感興趣的系結資訊。

 如需詳細資訊，請參閱 OLE DB 程式設計人員參考的 [附錄 A：資料類型](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6)。

### <a name="begin-binding-entries"></a>開始系結專案
 **BEGIN_ADO_BINDING** (*類別*) 

### <a name="fixed-length-data"></a>固定長度的資料
 **ADO_FIXED_LENGTH_ENTRY** (*序數、DataType、Buffer、Status、Modify*) 

 **ADO_FIXED_LENGTH_ENTRY2** (*序數、資料類型、緩衝區、修改*) 

### <a name="numeric-data"></a>數值資料
 **ADO_NUMERIC_ENTRY** (*序數、DataType、緩衝區、精確度、小數位數、狀態、修改*) 

 **ADO_NUMERIC_ENTRY2** (*序數、資料類型、緩衝區、精確度、小數位數、修改*) 

### <a name="variable-length-data"></a>可變長度資料
 **ADO_VARIABLE_LENGTH_ENTRY** (*序數、DataType、Buffer、Size、Status、LENGTH、Modify*) 

 **ADO_VARIABLE_LENGTH_ENTRY2** (*序數、資料類型、緩衝區、大小、狀態、修改*) 

 **ADO_VARIABLE_LENGTH_ENTRY3** (*序數、資料類型、緩衝區、大小、長度、修改*) 

 **ADO_VARIABLE_LENGTH_ENTRY4** (*序數、資料類型、緩衝區、大小、修改*) 

### <a name="end-binding-entries"></a>End Binding 專案
 **END_ADO_BINDING**()

|參數|描述|
|---------------|-----------------|
|*類別*|定義系結專案和 C/c + + 變數的類別。|
|*序*|與 C/c + + 變數對應之 **記錄集** 欄位的序數，從1開始計算。|
|*DataType*|C/c + + 變數的相等 ADO 資料類型 (如需有效資料類型的清單，請參閱 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)) 。 必要時，[ **記錄集** ] 欄位的值將會轉換為此資料類型。|
|*Buffer*|將儲存 **記錄集** 欄位之 C/c + + 變數的名稱。|
|*大小*|*緩衝區*的大小上限（以位元組為單位）。 如果 *緩衝區* 將包含可變長度的字串，則允許空間供終止的零使用。|
|*狀態*|變數的名稱，這個變數會指出 *緩衝區* 的內容是否有效，以及是否成功將欄位轉換成 *DataType* 。<br /><br /> 此變數最重要的兩個值為 **adFldOK**，表示轉換成功; **adFldNull**，這表示欄位的值會是類型 VT_Null 的變異數，而不只是空的。<br /><br /> *狀態*的可能值會在下一個表格中列出：「狀態值」。|
|*Modify*|布林值旗標;若為 TRUE，表示允許 ADO 以*緩衝區*中包含的值來更新對應的**記錄集**欄位。<br /><br /> 將 [布林值 *修改* ] 參數設定為 [TRUE]，讓 ADO 更新系結欄位，如果您想要檢查欄位但不變更，則為 FALSE。|
|*有效位數*|可以在數值變數中表示的位數。|
|*縮放比例*|數值變數中的小數位數。|
|*長度*|四位元組變數的名稱，這個變數會包含 *緩衝區*中資料的實際長度。|

## <a name="status-values"></a>狀態值
 *Status*變數的值會指出是否已成功將欄位複製到變數。

 設定資料時，可能會將 *狀態* 設定為 **adFldNull** ，以指出 **記錄集** 欄位應該設定為 null。

|常數|值|描述|
|--------------|-----------|-----------------|
|**adFldOK**|0|傳回非 null 的域值。|
|**adFldBadAccessor**|1|系結無效。|
|**adFldCantConvertValue**|2|由於符號不符或資料溢位以外的原因而無法轉換值。|
|**adFldNull**|3|取得欄位時，表示已傳回 null 值。<br /><br /> 設定欄位時，表示當欄位無法將**null**本身編碼時，欄位應該設定為**null** (例如，字元陣列或整數) 。|
|**adFldTruncated**|4|可變長度的資料或數位已被截斷。|
|**adFldSignMismatch**|5|值為帶正負號且變數資料類型不帶正負號。|
|**adFldDataOverFlow**|6|值大於可儲存在變數資料類型中的值。|
|**adFldCantCreate**|7|未知的資料行類型和欄位已開啟。|
|**adFldUnavailable**|8|無法判斷域值（例如，在不含預設值的新、未指派欄位上）。|
|**adFldPermissionDenied**|9|更新時，沒有寫入資料的許可權。|
|**adFldIntegrityViolation**|10|更新時，域值會違反資料行的完整性。|
|**adFldSchemaViolation**|11|更新時，域值會違反資料行架構。|
|**adFldBadStatus**|12|更新時，不正確 status 參數。|
|**adFldDefault**|13|更新時，會使用預設值。|

## <a name="see-also"></a>另請參閱
 [Visual C++ 擴充功能範例](../../../ado/guide/appendixes/visual-c-extensions-example.md) [Visual C++ 延伸模組標頭](../../../ado/guide/appendixes/visual-c-extensions-header.md)
