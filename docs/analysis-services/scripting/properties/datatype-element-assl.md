---
title: DataType 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b8d083b3899c92b662984c05ceb54e9a69268f1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="datatype-element-assl"></a>DataType 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義相關聯元素的資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataItem> <!-- or Measure -->  
   ...  
   <DataType>...</DataType>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)，[量值](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**DataType**中定義**System.Data.OleDb.OleDbType**列舉型別。 不過，只有下表中的列舉值中的有效值**DataType**項目。  
  
|Value|Description|  
|-----------|-----------------|  
|*BigInt*|64 位元帶正負號的整數。 此資料類型會對應至**Int64**中的資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)]OLE DB 中的.NET Framework 和的 DBTYPE_I8 資料類型。|  
|*bool*|布林值。 此資料類型會對應至**布林**.NET Framework 和 OLE DB 中的 DBTYPE_BOOL 資料類型中的資料型別。|  
|*貨幣*|貨幣值，範圍從-2<sup>63</sup> （或-922,337,203,685,477.5808） 到 2<sup>63</sup>-1 （或 + 922337203685，477.5807），正確率為貨幣單位的千分之十。 此資料類型會對應至**十進位**.NET Framework 和 OLE DB 中的 DBTYPE_CY 資料類型中的資料型別。|  
|*日期*|儲存成雙精確度浮點數的日期資料。 整數部分為自 1899 年 12 月 30 日起的天數，而分數部分則為一天的分數部分。 此資料類型會對應至**DateTime** .NET Framework 和 OLE DB 中的 DBTYPE_DATE 資料類型中的資料型別。|  
|*Double*|在 -1.79E +308 到 1.79E +308 範圍中的雙精確度浮點數。 此資料類型會對應至**Double** .NET Framework 和 OLE DB 中的 DBTYPE_R8 資料類型中的資料型別。|  
|*Integer*|32 位元帶正負號的整數。 此資料類型會對應至**Int32** .NET Framework 和 OLE DB 中的 DBTYPE_I4 資料類型中的資料型別。|  
|*Single*|在 -3.40E +38 到 3.40E +38 範圍中的單精確度浮點數。 此資料類型會對應至**單一**.NET Framework 和 OLE DB 中的 DBTYPE_R4 資料類型中的資料類型。|  
|*SmallInt*|16 位元帶正負號的整數。 此資料類型會對應至**Int16** .NET Framework 和 OLE DB 中的 DBTYPE_I2 資料類型中的資料型別。|  
|*TinyInt*|8 位元帶正負號的整數。 此資料類型會對應至**SByte** .NET Framework 和 OLE DB 中的 DBTYPE_I1 資料類型中的資料型別。|  
|*UnsignedBigInt*|64 位元不帶正負號的整數。 此資料類型會對應至**UInt64** .NET Framework 和 OLE DB 中的 DBTYPE_UI8 資料類型中的資料類型。|  
|*unsignedInt*|32 位元不帶正負號的整數。 此資料類型會對應至**UInt32** .NET Framework 和 OLE DB 中的 DBTYPE_UI4 資料類型中的資料型別。|  
|*UnsignedSmallInt*|16 位元不帶正負號的整數。 此資料類型會對應至**UInt16** .NET Framework 和 OLE DB 中的 DBTYPE_UI2 資料類型中的資料型別。|  
|*WChar*|Unicode 字元的以 Null 結束資料流。 此資料類型會對應至**字串**.NET Framework 和 OLE DB 中的 DBTYPE_WSTR 資料類型中的資料型別。|  
|*繼承*|資料型別**DataItem**中包含[來源](../../../analysis-services/scripting/properties/source-element-measure-assl.md)元素**量值**項目。<br /><br /> 注意： 僅適用於**量值**項目。|  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
