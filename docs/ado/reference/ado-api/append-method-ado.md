---
title: Append 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 4d0d94cf40a397ca030a9ea975a02962d6ab9489
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746913"
---
# <a name="append-method-ado"></a>Append 方法 (ADO)
將物件附加至集合。 如果集合是[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)，則可以建立新的[Field](../../../ado/reference/ado-api/field-object.md)物件，然後再將它附加至集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>參數  
 *集合*  
 集合物件。  
  
 *欄位*  
 **Fields**集合。  
  
 *物件*  
 物件變數，表示要附加的物件。  
  
 *名稱*  
 **字串**值，其中包含新**欄位**物件的名稱，而且不得與*欄位*中的任何其他物件名稱相同。  
  
 *類型*  
 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值，其預設值為**adEmpty**，指定新欄位的資料類型。 ADO 不支援下列資料類型，而且不應在將新欄位附加至[記錄集物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)時使用： **adIDispatch**、 **adIUnknown**、 **adVariant**。  
  
 *DefinedSize*  
 選擇性。 **Long**值，表示新欄位的定義大小（以字元或位元組為單位）。 這個參數的預設值是衍生自*類型*。 *DefinedSize*大於255個位元組的欄位會被視為可變長度的資料行。 未指定*DefinedSize*的預設值。  
  
 *Attrib*  
 選擇性。 [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值，其預設值為**adFldDefault**，指定新欄位的屬性。 如果未指定此值，欄位會包含衍生自*類型*的屬性。  
  
 *FieldValue*  
 選擇性。 **Variant** ，表示新欄位的值。 如果未指定，則會以 null 值附加欄位。  
  
## <a name="remarks"></a>備註  
  
## <a name="parameters-collection"></a>Parameters 集合  
 您必須先設定[參數](../../../ado/reference/ado-api/parameter-object.md)物件的[Type](../../../ado/reference/ado-api/type-property-ado.md)屬性，再將它附加至[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 如果您選取可變長度的資料類型，也必須將[Size](../../../ado/reference/ado-api/size-property-ado-parameter.md)屬性設定為大於零的值。  
  
 描述參數會自行減少對提供者的呼叫，因此當您使用預存程式或參數化查詢時，會改善效能。 不過，您必須知道與您要呼叫的預存程式或參數化查詢相關聯之參數的屬性。  
  
 使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法來建立具有適當屬性設定的**參數**物件，並使用**Append**方法將它們新增至[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 這可讓您設定和傳回參數值，而不需要為參數資訊呼叫提供者。 如果您要寫入未提供參數資訊的提供者，您必須使用此方法來手動填入**參數**集合，才能使用參數。  
  
## <a name="fields-collection"></a>Fields 集合  
 只有在將**欄位**物件加入至[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，而不是**記錄集**物件時， *FieldValue*參數才有效。 使用**記錄**物件時，您可以附加欄位並同時提供值。 使用**記錄集**物件時，您必須在**記錄集**關閉時建立欄位，然後開啟**記錄集**並將值指派給欄位。  
  
> [!NOTE]
>  對於已附加至**Record**物件之**Fields**集合的新**欄位**物件，必須先設定[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，才能指定任何其他**欄位**屬性。 首先，必須已指派**value**屬性的特定值，並在呼叫的**Fields**集合上進行[更新](../../../ado/reference/ado-api/update-method.md)。 然後，可以存取其他屬性，例如[類型](../../../ado/reference/ado-api/type-property-ado.md)或[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)。 下列資料類型（**DataTypeEnum**）的**欄位**物件無法附加至**Fields**集合，而且會導致發生錯誤： **adArray**、 **adChapter**、 **adEmpty**、 **adPropVariant**和**adUserDefined**。 此外，ADO 不支援下列資料類型： **adIDispatch**、 **adIUnknown**和**adIVariant**。 針對這些類型，附加時不會發生錯誤，但使用方式可能會產生無法預測的結果，包括記憶體流失。  
  
## <a name="recordset"></a>資料錄集  
 如果您在呼叫**Append**方法之前未設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性，則在呼叫[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法時， **CursorLocation**會自動設定為**adUseClient** （ [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值）。  
  
 如果在開啟的**記錄集**的**Fields**集合或已設定[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性的**記錄集**上呼叫**Append**方法，就會發生執行階段錯誤。 您只能將欄位附加至尚未開啟，而且尚未連接至資料來源的**記錄集**。 這通常是使用[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)方法制造**記錄集**物件或指派給物件變數時的情況。  
  
## <a name="record"></a>Record  
 如果在開啟**記錄**的**Fields**集合上呼叫**Append**方法，就不會發生執行階段錯誤。 新的欄位將會加入至**Record**物件的**Fields**集合。 如果**記錄**衍生自**記錄集**，新的欄位將不會出現在**記錄集**物件的**Fields**集合中。  
  
 您可以建立不存在的欄位，並將其附加至**Fields**集合，方法是將值指派給 field 物件，就像它已經存在於集合中一樣。 指派會觸發自動建立和附加**欄位**物件，然後指派將會完成。  
  
 將**欄位**附加至**Record**物件的**fields**集合之後，請呼叫**Fields**集合的**Update**方法來儲存變更。  
  
## <a name="applies-to"></a>套用至  
  
- [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Append 和 CreateParameter 方法範例（VB）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Append 和 CreateParameter 方法範例（VC + +）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter 方法（ADO）](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete 方法（ADO Fields 集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法（ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法（ADO Recordset）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
