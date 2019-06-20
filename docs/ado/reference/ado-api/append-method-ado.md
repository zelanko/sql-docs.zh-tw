---
title: Append 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 987b7d7006ff448a92eee1926a2c60c3b7ae039e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696675"
---
# <a name="append-method-ado"></a>Append 方法 (ADO)
將物件附加至集合。 如果集合很[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)，新[欄位](../../../ado/reference/ado-api/field-object.md)可以先建立物件，它會附加至集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>參數  
 *collection*  
 集合物件。  
  
 *fields*  
 A**欄位**集合。  
  
 *object*  
 物件變數，表示要附加的物件。  
  
 *名稱*  
 A**字串**值，包含新名稱**欄位**物件，而且不可以是相同的名稱中的任何其他物件*欄位*。  
  
 *型別*  
 A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值，其預設值是**adEmpty**，表示新欄位的資料型別。 ADO 中，不支援下列資料類型，以及應該不時，使用附加至新的欄位[資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**， **adIUnknown**， **adVariant**。  
  
 *DefinedSize*  
 選擇性。 A**長**表示定義的大小，以字元或位元組，新欄位的值。 此參數的預設值衍生自*型別*。 有的欄位*DefinedSize*大於 255 個位元組會被視為可變長度資料行。 預設值*DefinedSize*未指定。  
  
 *Attrib*  
 選擇性。 A [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值，其預設值是**adFldDefault**，，指定新欄位的屬性。 如果未指定此值，此欄位會包含衍生自屬性*型別*。  
  
 *FieldValue*  
 選擇性。 A **Variant** ，代表新欄位的值。 如果未指定，欄位會附加 null 值。  
  
## <a name="remarks"></a>備註  
  
## <a name="parameters-collection"></a>Parameters 集合  
 您必須設定[型別](../../../ado/reference/ado-api/type-property-ado.md)屬性[參數](../../../ado/reference/ado-api/parameter-object.md)之前附加到物件[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 如果您選取的可變長度資料類型時，您也必須設定[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)屬性設為小於或等於零的值。  
  
 描述您自己的參數到提供者的機會降到最低，因此可改善效能，當您使用預存程序或參數化的查詢。 不過，您必須知道與預存程序相關聯，或參數化您想要呼叫的查詢參數的屬性。  
  
 使用  [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法來建立**參數**具有適當的屬性設定和使用物件**附加**方法，將其新增至[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 這可讓您設定和傳回參數值，而不需要呼叫提供者之參數資訊。 如果您要寫入未提供參數資訊的提供者，您必須使用這個方法來手動填入**參數**才能完全使用參數的集合。  
  
## <a name="fields-collection"></a>Fields 集合  
 *FieldValue*參數才有效，當加入**欄位**物件[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，不**資料錄集**物件。 具有**記錄**物件，您可以附加欄位，並同時提供值。 具有**Recordset**物件，您必須建立欄位時**資料錄集**會關閉，然後開啟**資料錄集**並將值指派給欄位。  
  
> [!NOTE]
>  對新**欄位**附加到的物件**欄位**集合**記錄**物件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性必須設定在任何其他**欄位**可以指定的屬性。 首先，為特定值如**值**必須獲指派的屬性和[更新](../../../ado/reference/ado-api/update-method.md)上**欄位**呼叫的集合。 然後，這類的其他屬性[型別](../../../ado/reference/ado-api/type-property-ado.md)或是[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)可以存取。 **欄位**的下列資料類型的物件 (**DataTypeEnum**) 無法附加至**欄位**集合，且會導致發生錯誤： **adArray**，**adChapter**， **adEmpty**， **adPropVariant**，以及**adUserDefined**。 此外，下列資料類型不受 ADO: **adIDispatch**， **adIUnknown**，並**adIVariant**。 針對這些類型，附加時，就會發生任何錯誤，但使用方式可能會產生無法預期的結果，包括記憶體流失。  
  
## <a name="recordset"></a>資料錄集  
 如果您未設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性，然後再呼叫**附加**方法**CursorLocation**將會設定為**adUseClient** ([CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值) 時，自動[開放](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)呼叫物件。  
  
 如果會發生執行階段錯誤**Append**上呼叫方法**欄位**開啟集合**資料錄集**，或在**資料錄集**何處[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性已設定。 您可以只將附加欄位**資料錄集**，並未開啟，且尚未連接到資料來源。 這通常是因為當**資料錄集**物件會傳遞具有[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)方法或指派給物件變數。  
  
## <a name="record"></a>記錄  
 若是執行階段錯誤將不會**Append**上呼叫方法**欄位**開啟集合**記錄**。 新的欄位會加入至**欄位**的集合**記錄**物件。 如果**記錄**衍生自**Recordset**，新的欄位不會出現在**欄位**集合**資料錄集**物件。  
  
 可以建立並附加至不存在的欄位**欄位**藉由指派值給欄位的物件，如同它已存在於集合的集合。 自動建立和附加的將會觸發工作分派**欄位**物件，然後按一下 指派將會完成。  
  
 之後附加**欄位**要**欄位**集合**記錄**物件，請呼叫**更新**方法**欄位**集合，以儲存變更。  
  
## <a name="applies-to"></a>適用於  
  
- [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [附加和 CreateParameter 方法範例 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [附加和 CreateParameter 方法範例 （VC + +）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete 方法 (ADO Fields 集合)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
