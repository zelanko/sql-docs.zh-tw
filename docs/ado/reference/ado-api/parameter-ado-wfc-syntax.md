---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d39d181190d6bc28fa94271c7be787735e0515dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703981"
---
# <a name="parameter-ado---wfc-syntax"></a>Parameter (ADO - WFC 語法)
## <a name="package-commswfcdata"></a>package com.ms.wfc.data  
  
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
 [值](../../../ado/reference/ado-api/value-property-ado.md)屬性[參數](../../../ado/reference/ado-api/parameter-object.md)物件取得或設定該物件的內容。 內容被以一種可以指派值的物件和數種資料類型的 VARIANT。  
  
 ADO/WFC 實作**值**屬性**getValue**方法，以傳回 VARIANT 的物件; 而**setValue**方法，後者會採用當做引數的 VARIANT。 變化是以特定語言，例如 Microsoft Visual Basic 高效率。  
  
 除了**值**屬性，ADO/WFC 提供*存取子*來取得和設定的內容中使用 Java 資料類型的方法**參數**物件。 大部分的這些方法都有名稱格式**取得**_資料類型_或是**設定**_DataType_。  
  
 還有一個值得注意的例外狀況：沒有任何**getNull**屬性; 相反地，沒有**isNull**傳回布林值，指出欄位是否為 null 的屬性。  
  
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
 [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)
