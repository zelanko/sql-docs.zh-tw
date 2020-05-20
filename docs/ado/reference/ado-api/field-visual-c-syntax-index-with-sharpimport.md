---
title: 'Field （具有 #import 的 Visual C++ 語法索引） |Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 13e2c57f4e00b4a4dae03a11ee357dd8f1d6398e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758774"
---
# <a name="field-visual-c-syntax-index-with-import"></a>Field （使用 #import Visual C++ 語法索引）
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
