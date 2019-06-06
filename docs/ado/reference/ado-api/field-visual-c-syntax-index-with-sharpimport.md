---
title: '欄位 (VisualC++含 #import 語法索引) |Microsoft Docs'
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
- 'Field collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 90cb636a-9416-48a4-b4eb-bb11bbd40950
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 14255d0fc7a073f7a69f0373c009b4b948888151
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695085"
---
# <a name="field-visual-c-syntax-index-with-import"></a>欄位 (VisualC++含 #import 語法索引)
## <a name="methods"></a>方法  
  
```  
HRESULT AppendChunk( const _variant_t & Data );  
  
_variant_t GetChunk( long Length );  
```  
  
## <a name="properties"></a>屬性  
  
```  
long GetActualSize( );  
__declspec(property(get=GetActualSize)) long ActualSize;  
  
long GetAttributes( );  
void PutAttributes( long pl );  
__declspec(property(get=GetAttributes,put=PutAttributes)) long     Attributes;  
  
IUnknownPtr GetDataFormat( );  
void PutRefDataFormat( IUnknown * ppiDF );  
__declspec(property(get=GetDataFormat,put=PutRefDataFormat)) IunknownPtr  
    DataFormat;  
  
long GetDefinedSize( );  
void PutDefinedSize( long pl );  
__declspec(property(get=GetDefinedSize,put=PutDefinedSize)) long  
    DefinedSize;  
  
_bstr_t GetName( );  
__declspec(property(get=GetName)) _bstr_t Name;  
  
unsigned char GetNumericScale( );  
void PutNumericScale( unsigned char pbNumericScale );  
__declspec(property(get=GetNumericScale,put=PutNumericScale)) unsigned  
    char NumericScale;  
  
_variant_t GetOriginalValue( );  
__declspec(property(get=GetOriginalValue)) _variant_t OriginalValue;  
  
unsigned char GetPrecision( );  
void PutPrecision( unsigned char pbPrecision );  
__declspec(property(get=GetPrecision,put=PutPrecision)) unsigned char  
    Precision;  
  
enum DataTypeEnum GetType( );  
void PutType( enum DataTypeEnum pDataType );  
__declspec(property(get=GetType,put=PutType)) enum DataTypeEnum Type;  
  
_variant_t GetUnderlyingValue( );  
__declspec(property(get=GetUnderlyingValue)) _variant_t UnderlyingValue;  
  
_variant_t GetValue( );  
void PutValue( const _variant_t & pvar );  
__declspec(property(get=GetValue,put=PutValue)) _variant_t Value;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)
