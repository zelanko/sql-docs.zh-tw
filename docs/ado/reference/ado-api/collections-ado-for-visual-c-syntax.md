---
description: Collections (ADO for Visual C++ 語法)
title: Visual C++ 語法的 (ADO 集合) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b4bc59facd753bf6d36c3a79d06a4efe29e7c235
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975379"
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
  
-   [Append 方法 (ADO)](./append-method-ado.md)  
  
-   [Delete 方法 (ADO Parameters 集合)](./delete-method-ado-parameters-collection.md)  
  
-   [Refresh 方法 (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, _ADOParameter **ppvObject);  
```  
  
 如需相關資訊，請參閱  
  
-   [Count 屬性 (ADO)](./count-property-ado.md)  
  
-   [Item 屬性 (ADO)](./item-property-ado.md)  
  
## <a name="fields"></a>欄位  
  
### <a name="methods"></a>方法  
  
```  
Append(BSTR bstrName, DataTypeEnum Type, long DefinedSize, FieldAttributeEnum Attrib);  
Delete(VARIANT Index);  
Refresh(void);  
```  
  
 如需相關資訊，請參閱  
  
-   [Append 方法 (ADO)](./append-method-ado.md)  
  
-   [Delete 方法 (ADO Parameters 集合)](./delete-method-ado-parameters-collection.md)  
  
-   [Refresh 方法 (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOField **ppvObject);  
```  
  
 如需相關資訊，請參閱  
  
-   [Count 屬性 (ADO)](./count-property-ado.md)  
  
-   [Item 屬性 (ADO)](./item-property-ado.md)  
  
## <a name="errors"></a>Errors  
  
### <a name="methods"></a>方法  
  
```  
Clear(void);  
Refresh(void);  
```  
  
 如需相關資訊，請參閱  
  
-   [Clear 方法 (ADO)](./clear-method-ado.md)  
  
-   [Refresh 方法 (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOError **ppvObject);  
```  
  
 如需相關資訊，請參閱  
  
-   [Count 屬性 (ADO)](./count-property-ado.md)  
  
-   [Item 屬性 (ADO)](./item-property-ado.md)  
  
## <a name="properties"></a>屬性  
  
### <a name="methods"></a>方法  
  
```  
Refresh(void);  
```  
  
 如需相關資訊，請參閱  
  
-   [Refresh 方法 (ADO)](./refresh-method-ado.md)  
  
### <a name="properties"></a>屬性  
  
```  
get_Count(long *c);  
get_Item(VARIANT Index, ADOProperty **ppvObject);  
```  
  
 如需相關資訊，請參閱  
  
-   [Count 屬性 (ADO)](./count-property-ado.md)  
  
-   [Item 屬性 (ADO)](./item-property-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 收集錯誤 ](./errors-collection-ado.md)   
 [ (ADO) 的欄位集合 ](./fields-collection-ado.md)   
 [ (ADO) 的參數集合 ](./parameters-collection-ado.md)   
 [Properties 集合 (ADO)](./properties-collection-ado.md)