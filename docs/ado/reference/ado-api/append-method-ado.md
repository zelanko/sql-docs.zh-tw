---
description: Append 方法 (ADO)
title: " (ADO) 的 Append 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
author: rothja
ms.author: jroth
ms.openlocfilehash: 84969b95751726579bdc7d4a61aee311b95b6108
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976079"
---
# <a name="append-method-ado"></a>Append 方法 (ADO)
將物件附加至集合。 如果集合是 [欄位](./fields-collection-ado.md)，就可以在附加至集合之前，先建立新的 [欄位](./field-object.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>參數  
 *collection*  
 集合物件。  
  
 *欄位*  
 **Fields**集合。  
  
 *object*  
 物件變數，表示要附加的物件。  
  
 *名稱*  
 包含新**欄位**物件名稱的**字串**值，而且不能與*欄位*中的任何其他物件名稱相同。  
  
 *類型*  
 [DataTypeEnum](./datatypeenum.md)值，其預設值為**adEmpty**，指定新欄位的資料類型。 ADO 不支援下列資料類型，而且不應該在將新欄位附加至 [記錄集物件時使用， (ado) ](./recordset-object-ado.md)： **adIDispatch**、 **adIUnknown**、 **adVariant**。  
  
 *DefinedSize*  
 選擇性。 **Long**值，表示新欄位的定義大小（以字元或位元組為單位）。 此參數的預設值是衍生自 *類型*。 *DefinedSize*大於255個位元組的欄位會被視為可變長度資料行。 未指定 *DefinedSize* 的預設值。  
  
 *Attrib*  
 選擇性。 [FieldAttributeEnum](./fieldattributeenum.md)值，其預設值為**adFldDefault**，指定新欄位的屬性。 如果未指定此值，欄位將會包含衍生自 *類型*的屬性。  
  
 *FieldValue*  
 選擇性。 表示新欄位值的 **Variant** 。 如果未指定，則會以 null 值附加欄位。  
  
## <a name="remarks"></a>備註  
  
## <a name="parameters-collection"></a>Parameters 集合  
 您必須先設定[參數](./parameter-object.md)物件的[型](./type-property-ado.md)別屬性，然後再將它附加至[Parameters](./parameters-collection-ado.md)集合。 如果您選取可變長度的資料類型，您也必須將 [ [大小](./size-property-ado-parameter.md) ] 屬性設定為大於零的值。  
  
 使用預存程式或參數化查詢時，自行描述參數可將對提供者的呼叫降至最低，進而改善效能。 不過，您必須知道要呼叫的預存程式或參數化查詢相關聯之參數的屬性。  
  
 您可以使用 [CreateParameter](./createparameter-method-ado.md) 方法，以適當的屬性設定來建立 **參數** 物件，並使用 **Append** 方法將它們加入至 [Parameters](./parameters-collection-ado.md) 集合。 這可讓您設定和傳回參數值，而不需要呼叫提供者取得參數資訊。 如果您要寫入未提供參數資訊的提供者，則必須使用此方法手動填入 **參數** 集合，才能使用參數。  
  
## <a name="fields-collection"></a>Fields 集合  
 *FieldValue*參數只有在將**欄位**物件加入至[記錄](./record-object-ado.md)物件時才有效，而不是**記錄集**物件。 您可以使用 **記錄** 物件來附加欄位，並同時提供值。 使用 **記錄集** 物件時，您必須在 **記錄集** 關閉時建立欄位，然後開啟 **記錄集** 並將值指派給欄位。  
  
> [!NOTE]
>  針對附加至**Record**物件之**Fields**集合的新**欄位**物件，必須先設定[Value](./value-property-ado.md)屬性，才能指定任何其他**欄位**屬性。 首先，必須已指派**value**屬性的特定值，並在呼叫的**Fields**集合上[更新](./update-method.md)。 然後，可以存取其他屬性，例如 [類型](./type-property-ado.md) 或 [屬性](./attributes-property-ado.md) 。 下列資料類型的**欄位**物件 (**DataTypeEnum**) 無法附加至**Fields**集合，而且會導致錯誤發生： **adArray**、 **adChapter**、 **adEmpty**、 **adPropVariant**和**adUserDefined**。 此外，ADO 不支援下列資料類型： **adIDispatch**、 **adIUnknown**和 **adIVariant**。 針對這些類型，附加時不會發生錯誤，但使用方式可能會產生無法預測的結果，包括記憶體流失。  
  
## <a name="recordset"></a>資料錄集  
 如果您在呼叫**Append**方法之前未設定[CursorLocation](./cursorlocation-property-ado.md)屬性， **CursorLocation**將會設定為**adUseClient** (當呼叫[記錄集](./recordset-object-ado.md)物件的[Open](./open-method-ado-recordset.md)方法時，會自動) [CursorLocationEnum](./cursorlocationenum.md)值。  
  
 如果在開啟的**記錄集**的**Fields**集合上，或在已設定[ActiveConnection](./activeconnection-property-ado.md)屬性的**記錄集**上呼叫**Append**方法，就會發生執行階段錯誤。 您只能將欄位附加至未開啟的 **記錄集** ，而且尚未連接至資料來源。 當 **記錄集** 物件是以 [CreateRecordset](../rds-api/createrecordset-method-rds.md) 方法制造或指派給物件變數時，通常就會發生這種情況。  
  
## <a name="record"></a>Record  
 如果在開啟**記錄**的**Fields**集合上呼叫**Append**方法，則不會發生執行階段錯誤。 新欄位就會加入至**Record**物件的**Fields**集合中。 如果**記錄**衍生自記錄**集**，新的欄位就不會出現在**記錄集**物件的**Fields**集合中。  
  
 您可以建立欄位物件的值，並將其附加至 **Fields** 集合，就像該欄位已經存在於集合中一樣。 指派將會觸發自動建立和附加 **欄位** 物件，然後將完成指派。  
  
 將**欄位**附加至**Record**物件的**fields**集合之後，請呼叫**fields**集合的**Update**方法來儲存變更。  
  
## <a name="applies-to"></a>套用至  
  
- [Fields 集合 (ADO)](./fields-collection-ado.md)  
- [Parameters 集合 (ADO)](./parameters-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [附加和 CreateParameter 方法範例 (VB) ](./append-and-createparameter-methods-example-vb.md)   
 [附加和 CreateParameter 方法範例 (VC + +) ](./append-and-createparameter-methods-example-vc.md)   
 [ (ADO) 的 CreateParameter 方法 ](./createparameter-method-ado.md)   
 [ (ADO Fields 集合) 的 Delete 方法 ](./delete-method-ado-fields-collection.md)   
 [Delete 方法 (ADO Parameters 集合) ](./delete-method-ado-parameters-collection.md)   
 [ (ADO 記錄集的 Delete 方法) ](./delete-method-ado-recordset.md)   
 [Update 方法](./update-method.md)