---
description: '使用 #import) Visual C++ 語法索引的集合 ('
title: '使用 #import)  (Visual C++ 語法索引的集合 |Microsoft Docs'
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
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
author: rothja
ms.author: jroth
ms.openlocfilehash: 58f7761cc67cd1320594988ba50bfcc79bcfc0d9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450910"
---
# <a name="collections-visual-c-syntax-index-with-import"></a>使用 #import) Visual C++ 語法索引的集合 (
知道集合會繼承某些常見的方法和屬性，會很有用。  
  
 所有集合都會繼承 **Count** 屬性和 **Refresh** 方法，而所有集合都會加入 **Item** 屬性。 **Errors**集合會加入**Clear**方法。 **Parameters**集合會繼承**append**和**delete**方法，而**Fields**集合則會加入**append**、 **delete**和**Update**方法。  
  
## <a name="properties-collection"></a>屬性集合  
  
### <a name="methods"></a>方法  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>屬性  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>錯誤集合  
  
### <a name="methods"></a>方法  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>屬性  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Parameters 集合  
  
### <a name="methods"></a>方法  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>屬性  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>Fields 集合  
  
### <a name="methods"></a>方法  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>屬性  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 收集錯誤 ](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [ (ADO) 的欄位集合 ](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [ (ADO) 的參數集合 ](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
