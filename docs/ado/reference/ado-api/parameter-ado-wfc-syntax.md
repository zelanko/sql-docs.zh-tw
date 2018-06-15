---
title: 參數 (ADO-WFC 語法) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb5ee000ca00031f35f27ec23dec3e284656f56a
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280587"
---
# <a name="parameter-ado---wfc-syntax"></a>參數 (ADO-WFC 語法)
## <a name="package-commswfcdata"></a>封裝 com.ms.wfc.data  
  
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
 [值](../../../ado/reference/ado-api/value-property-ado.md)屬性[參數](../../../ado/reference/ado-api/parameter-object.md)物件取得或設定該物件的內容。 被表示為 VARIANT，可指派值的物件類型及數種資料類型的內容。  
  
 ADO/WFC 實作**值**屬性**getValue**方法，這個方法會傳回 VARIANT 的物件; 而**setValue**採用做為引數的 VARIANT 的方法。 Variant 則高效率的某些語言，例如 Microsoft Visual Basic 中。  
  
 除了**值**屬性 ADO/WFC 提供*存取子*用於取得及設定的內容中的 Java 資料類型方法**參數**物件。 大部分的這些方法會有的名稱格式 **取得 * * * DataType*或 **設定 * * * DataType*。  
  
 還有一個值得注意的例外狀況： 沒有任何**getNull**屬性; 相反地，沒有**isNull**傳回布林值，指出欄位是否為 null 的屬性。  
  
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
