---
description: Parameter (ADO - WFC 語法)
title: 參數 (ADO-WFC 語法) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
author: rothja
ms.author: jroth
ms.openlocfilehash: 09d345a0f08d9fa2e9e3696941aba1ef49443efd
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773467"
---
# <a name="parameter-ado---wfc-syntax"></a>Parameter (ADO - WFC 語法)
## <a name="package-commswfcdata"></a>封裝 .com. 資料  
  
### <a name="constructor"></a>建構函式  
  
```  
public Parameter()  
public Parameter(String name)  
public Parameter(String name, int type)  
public Parameter(String name, int type, int dir)  
public Parameter(String name, int type, int dir, int size)  
public Parameter(String name, int type, int dir, int size, Object value)  
```  
  
### <a name="methods"></a>方法  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
```  
  
### <a name="properties"></a>屬性  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getDirection()  
public void setDirection(int dir)  
public String getName()  
public void setName(String name)  
public int getNumericScale()  
public void setNumericScale(int scale)  
public int getPrecision()  
public void setPrecision(int prec)  
public int getSize()  
public void setSize(int size)  
public int getType()  
public void setType(int type)  
public com.ms.com.Variant getValue()  
public void setValue(Object v)  
public AdoProperties getProperties()  
```  
  
## <a name="parameter-accessor-methods"></a>參數存取子方法  
 [參數](./parameter-object.md)物件的[Value](./value-property-ado.md)屬性會取得或設定該物件的內容。 內容會表示為 VARIANT、可以指派值的物件類型，以及數個資料類型的任一個。  
  
 ADO/WFC 會使用**getValue**方法來實**值**屬性，此方法會傳回 VARIANT 物件;和**setValue**方法，它會採用 VARIANT 作為引數。 Variant 在某些語言（例如 Microsoft Visual Basic）中具有高效率。  
  
 除了 **Value** 屬性之外，ADO/WFC 也提供 *存取* 子方法，這些方法會使用 JAVA 資料類型來取得和設定 **參數** 物件的內容。 這些方法大多都有格式的 **get**_datatype_ 或 **set**_datatype_。  
  
 有一個值得注意的例外狀況：沒有 **getNull** 屬性;相反地，有一個 **isNull** 屬性會傳回布林值，指出欄位是否為 null。  
  
```  
public boolean getBoolean()  
public void setBoolean(boolean v)  
public byte getByte()  
public void setByte(byte v)  
public double getDouble()  
public void setDouble(double v)  
public float getFloat()  
public void setFloat(float v)  
public int getInt()  
public void setInt(int v)  
public long getLong()  
public void setLong(long v)  
public short getShort()  
public void setShort(short v)  
public String getString()  
public void setString(String v)  
public boolean isNull()  
public void setNull()  
```  
  
## <a name="see-also"></a>另請參閱  
 [Parameter 物件](./parameter-object.md)