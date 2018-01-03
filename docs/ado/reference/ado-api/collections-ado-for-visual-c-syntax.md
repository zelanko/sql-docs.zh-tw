---
title: "集合 (如需 Visual c + + 語法的 ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
dev_langs: C++
helpviewer_keywords:
- ADO for Visual C++ syntax [ADO]
- syntax indexes [ADO], ADO for Visual C++ syntax
- collections [ADO], ADO for Visual C++ syntax
ms.assetid: 6a0109a0-f2d9-4f7c-8e1e-42763f9acaea
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 451fded6bf6f12ef2f5589facb63ed53b2de1ad7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="collections-ado-for-visual-c-syntax"></a>集合 (如需 Visual c + + 語法的 ADO)
## <a name="parameters"></a>參數  
  
### <a name="methods"></a>方法  
  
```  
Append(IDispatch *Object);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 如需詳細資訊，請參閱  
  
-   [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete 方法 (ADO Parameters 集合)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 如需詳細資訊，請參閱  
  
-   [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="fields"></a>欄位  
  
### <a name="methods"></a>方法  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 如需詳細資訊，請參閱  
  
-   [Append 方法 (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
  
-   [Delete 方法 (ADO Parameters 集合)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 如需詳細資訊，請參閱  
  
-   [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="errors"></a>錯誤  
  
### <a name="methods"></a>方法  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 如需詳細資訊，請參閱  
  
-   [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 如需詳細資訊，請參閱  
  
-   [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="properties"></a>屬性  
  
### <a name="methods"></a>方法  
  
```  
Refresh(void);  
```  
  
 如需詳細資訊，請參閱  
  
-   [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 如需詳細資訊，請參閱  
  
-   [Count 屬性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)  
  
-   [Item 屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)  
  
## <a name="see-also"></a>請參閱  
 [錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [參數集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
