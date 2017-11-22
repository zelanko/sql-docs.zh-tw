---
title: "欄位 (ADO-WFC 語法) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb583ec535744dc394f700279dd104f3be6a810d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="field-ado---wfc-syntax"></a>欄位 (ADO-WFC 語法)
## <a name="package-commswfcdata"></a>封裝 com.ms.wfc.data  
  
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
 [值](../../../ado/reference/ado-api/value-property-ado.md)屬性[欄位](../../../ado/reference/ado-api/field-object.md)物件取得或設定該物件的內容。 被表示為 VARIANT，可指派值的物件類型及數種資料類型的內容。  
  
 ADO/WFC 實作**值**屬性**getValue**方法，這個方法會傳回 VARIANT 的物件; 而**setValue**採用做為引數的 VARIANT 的方法。 Variant 則高效率的某些語言，例如 Microsoft Visual Basic 中。  
  
 除了**值**屬性 ADO/WFC 提供*存取子*用於取得及設定的內容中的 Java 資料類型方法**欄位**物件。 大部分的這些方法會有的名稱格式**取得***DataType*或**設定***DataType*。  
  
 有兩個值得注意的例外狀況： 其中一個**getObject**方法會傳回強制轉型為指定之類別的物件。 沒有任何**getNull**屬性; 相反地，沒有**isNull**傳回布林值，指出欄位是否為 null 的屬性。  
  
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
  
## <a name="see-also"></a>請參閱＜  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)
