---
title: '集合 (VisualC++含 #import 語法索引) |Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f761a0d65954e104be0849f10c786cc709085a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718245"
---
# <a name="collections-visual-c-syntax-index-with-import"></a>集合 (VisualC++含 #import 語法索引)
您最好知道集合繼承某些常用的方法和屬性。  
  
 所有集合都繼承**計數**屬性並**重新整理**方法，以及所有集合加入**項目**屬性。 **錯誤**集合加入**清除**方法。 **參數**集合繼承**附加**並**刪除**方法，而**欄位**集合加入**Append**，**刪除**，和**更新**方法。  
  
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
 [Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [參數集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
