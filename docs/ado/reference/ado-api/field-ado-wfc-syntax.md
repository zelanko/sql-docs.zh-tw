---
title: 欄位 (ADO-WFC 語法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea2245c3f57b5ad3b14847f15791575afde1043c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63031966"
---
# <a name="field-ado---wfc-syntax"></a>Field (ADO - WFC 語法)
## <a name="package-commswfcdata"></a>package com.ms.wfc.data  
  
### <a name="methods"></a>方法  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 （如需詳細資訊，請參閱 com.ms.wfc.data.IDataFormat 介面的文件）。  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>欄位存取子方法  
 [值](../../../ado/reference/ado-api/value-property-ado.md)屬性[欄位](../../../ado/reference/ado-api/field-object.md)物件取得或設定該物件的內容。 內容被以一種可以指派值的物件和數種資料類型的 VARIANT。  
  
 ADO/WFC 實作**值**屬性**getValue**方法，以傳回 VARIANT 的物件; 而**setValue**方法，後者會採用當做引數的 VARIANT。 變化是以特定語言，例如 Microsoft Visual Basic 高效率。  
  
 除了**值**屬性，ADO/WFC 提供*存取子*來取得和設定的內容中使用 Java 資料類型的方法**欄位**物件。 大部分的這些方法都有名稱格式**取得**_資料類型_或是**設定**_DataType_。  
  
 有兩個值得注意的例外狀況：其中一個**getObject**方法會傳回強制轉型為指定的類別的物件。 沒有任何**getNull**屬性; 相反地，沒有**isNull**傳回布林值，指出欄位是否為 null 的屬性。  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)
