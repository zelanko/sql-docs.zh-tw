---
title: Field （ADO-WFC 語法） |Microsoft Docs
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
ms.openlocfilehash: 583e6de7dc8c3ea05d61dda53c3e630d05e4d5f9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918754"
---
# <a name="field-ado---wfc-syntax"></a>Field (ADO - WFC 語法)
## <a name="package-commswfcdata"></a>封裝 .com. wfc. 資料  
  
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
  
 （如需詳細資訊，請參閱 IDataFormat 介面的檔。）  
  
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
 [Field](../../../ado/reference/ado-api/field-object.md)物件的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性會取得或設定該物件的內容。 內容會以 VARIANT 表示，這是一種可指派值的物件類型，以及數種資料類型的任何一種。  
  
 ADO/WFC 會使用**getValue**方法來執行**Value**屬性，它會傳回 VARIANT 物件;和**setValue**方法，其採用 VARIANT 做為引數。 在某些語言（例如 Microsoft Visual Basic）中，變體非常有效率。  
  
 除了**Value**屬性，ADO/WFC 還提供使用 JAVA 資料類型的*存取*子方法，以取得和設定**欄位**物件的內容。 這些方法大多都具有格式為**get**_datatype_或**set**_datatype_的名稱。  
  
 有兩個值得注意的例外狀況：其中一個**getObject**方法會傳回已強制轉型為指定類別的物件。 沒有**getNull**屬性;相反地，有一個**isNull**屬性會傳回布林值，指出欄位是否為 null。  
  
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
