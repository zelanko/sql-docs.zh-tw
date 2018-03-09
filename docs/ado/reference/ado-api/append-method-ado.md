---
title: "Append 方法 (ADO) |Microsoft 文件"
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
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9a192286d39660580968305d16cb159480b6a09a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-ado"></a>Append 方法 (ADO)
將物件附加至集合。 如果集合是[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)，新[欄位](../../../ado/reference/ado-api/field-object.md)可以先建立物件，會附加至集合。  
  
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
  
 *物件*  
 物件變數，表示要附加的物件。  
  
 *名稱*  
 A**字串**包含新的名稱值**欄位**物件，而且不可以是相同的名稱中的任何其他物件*欄位*。  
  
 *型別*  
 A [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)值，其預設值是**adEmpty**，指定新欄位的資料類型。 下列資料類型不受 ADO 中，並應該不時，使用附加的新欄位[資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md): **adIDispatch**， **adIUnknown**， **adVariant**。  
  
 *DefinedSize*  
 選擇性。 A**長**表示的定義的大小，以字元或位元組，新欄位的值。 這個參數的預設值衍生自*類型*。 有的欄位*DefinedSize*大於 255 個位元組會被視為可變長度資料行。 預設值為*DefinedSize*未指定。  
  
 *Attrib*  
 選擇性。 A [FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)值，其預設值是**adFldDefault**，指定新的欄位屬性。 如果未指定此值，此欄位會包含衍生自屬性*類型*。  
  
 *FieldValue*  
 選擇性。 A **Variant** ，代表新欄位的值。 如果未指定，欄位會附加 null 值。  
  
## <a name="remarks"></a>備註  
  
## <a name="parameters-collection"></a>Parameters 集合  
 您必須設定[類型](../../../ado/reference/ado-api/type-property-ado.md)屬性[參數](../../../ado/reference/ado-api/parameter-object.md)之前附加到物件[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 如果您選取的可變長度資料類型，您也必須設定[大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)屬性設為大於零的值。  
  
 描述參數自行將呼叫提供者，而且當您使用預存程序或參數化的查詢，因此可改善效能。 不過，您必須知道參數的屬性與預存程序相關聯，或您想要呼叫的查詢參數化。  
  
 使用[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)方法來建立**參數**具有適當的屬性設定和使用物件**附加**方法將其新增至[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 這可讓您設定和傳回參數值，而不必呼叫提供者之參數資訊。 如果您要寫入的提供者，並不提供參數資訊，您必須使用這個方法來手動填入**參數**才能完全使用參數的集合。  
  
## <a name="fields-collection"></a>Fields 集合  
 *FieldValue*參數才有效，當加入**欄位**物件[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件時，無法供**資料錄集**物件。 與**記錄**物件，您可以新增欄位，並提供在相同的時間值。 與**資料錄集**物件，您必須建立欄位時**資料錄集**是關閉的狀態，並開啟**資料錄集**並將值指派給欄位。  
  
> [!NOTE]
>  對於新**欄位**已附加至的物件**欄位**集合**記錄**物件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性必須設定在任何其他**欄位**可以指定屬性。 首先，為特定值**值**指派屬性必須與[更新](../../../ado/reference/ado-api/update-method.md)上**欄位**稱為集合。 然後，其他屬性，例如[類型](../../../ado/reference/ado-api/type-property-ado.md)或[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)可以存取。 **欄位**下列資料類型的物件 (**DataTypeEnum**) 無法附加至**欄位**集合，且會導致發生錯誤： **adArray**， **adChapter**， **adEmpty**， **adPropVariant**，和**adUserDefined**。 此外，下列資料類型不受 ADO: **adIDispatch**， **adIUnknown**，和**adIVariant**。 針對這些類型，不會發生錯誤時附加，但使用方式可能會產生無法預期的結果，包括記憶體流失。  
  
## <a name="recordset"></a>資料錄集  
 如果您未設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性，然後再呼叫**附加**方法， **CursorLocation**會設定為**adUseClient** ([CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)值) 時，自動[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)稱為物件。  
  
 如果會發生執行階段錯誤**附加**上呼叫方法**欄位**的開放集合**資料錄集**，或在**資料錄集**其中[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性已設定。 您可以只將附加欄位**資料錄集**，並未開啟，且尚未連接到資料來源。 通常是當**資料錄集**物件會傳遞具有[CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)方法或指派給物件變數。  
  
## <a name="record"></a>記錄  
 如果不會發生執行階段錯誤**附加**上呼叫方法**欄位**的開放集合**記錄**。 新欄位加入**欄位**集合**記錄**物件。 如果**記錄**衍生自**資料錄集**，新的欄位不會出現在**欄位**集合**資料錄集**物件。  
  
 您可以建立及附加至不存在欄位**欄位**將此值指派至欄位物件，如同它已存在於集合的集合。 指派將會觸發自動建立並附加的**欄位**物件，然後按一下 指派將會完成。  
  
 附加之後**欄位**至**欄位**集合**記錄**物件，呼叫**更新**方法**欄位**集合，以儲存變更。  
  
## <a name="applies-to"></a>適用於  
  
- [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
- [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [附加和 CreateParameter 方法範例 (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [附加和 CreateParameter 方法範例 （VC + +）](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Delete 方法 （ADO 欄位集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 參數集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
