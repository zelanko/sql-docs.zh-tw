---
title: 集合（ADO for Visual C++ 語法） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f18884c7a1aabe138408cca7eb529f4f21120330
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919915"
---
# <a name="collections-ado-for-visual-c-syntax"></a>Collections (ADO for Visual C++ 語法)
## <a name="parameters"></a>參數  
  
### <a name="methods"></a>方法  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 如需相關資訊，請參閱  
  
-   [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete 方法 (ADO Parameters 集合)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 如需相關資訊，請參閱  
  
-   [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>欄位  
  
### <a name="methods"></a>方法  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 如需相關資訊，請參閱  
  
-   [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete 方法 (ADO Parameters 集合)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 如需相關資訊，請參閱  
  
-   [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>Errors  
  
### <a name="methods"></a>方法  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 如需相關資訊，請參閱  
  
-   [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 如需相關資訊，請參閱  
  
-   [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>屬性  
  
### <a name="methods"></a>方法  
  
```  
Refresh(void);  
```  
  
 如需相關資訊，請參閱  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 如需相關資訊，請參閱  
  
-   [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Errors 集合（ADO）](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Fields 集合（ADO）](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Parameters 集合（ADO）](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
