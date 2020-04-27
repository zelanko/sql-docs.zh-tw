---
title: Analysis Services 中的資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 910be4f4-3010-41cd-9fdc-f0a79a0ce823
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ecdc64918e582f25f0e017d263c66e78c0d1bee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62725382"
---
# <a name="data-types-in-analysis-services"></a>Analysis Services 中的資料類型
  對於所有<xref:Microsoft.AnalysisServices.DataItem>物件， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]都支援下列的子集`System.Data.OleDb.OleDbType`。 若要設定或讀取資料類型，請使用[DataItem 資料類型 &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/data-type/dataitem-data-type-assl)。  
  
## <a name="supported-data-types"></a>支援的資料類型  
  
|||  
|-|-|  
|BigInt|64 位元帶正負號的整數。 *BigInt*數值型別代表值範圍從負值9223372036854775808到正9223372036854775807的整數。|  
|Binary|**Byte**類型的二進位資料資料流程。 **Byte**是代表不帶正負號整數值的實值型別，範圍介於0到255之間。|  
|Boolean|這個類型的執行個體具有 `true` 或 `false` 值。|  
|貨幣|*貨幣*值，範圍從-922337203685477.5808 到 + 922337203685477.5807，精確度為貨幣單位的萬分之一（四位數）。|  
|日期|日期和時間資料，儲存為雙精確度浮點數。 整數部分為自 1899 年 12 月 30 日起的天數，而分數部分則為一天的分數部分或當天的時間。|  
|Double|浮點數，範圍在 -1.79769313486232E +308 到 1.79769313486232E +308 之間。 Double 值儲存最多有效位數為 15 個小數位數的數字資訊。|  
|整數|32 位元帶正負號的整數，代表範圍從複數 2,147,483,648 到正數 2,147,483,647 的帶正負號的整數值。|  
|Single|浮點數，範圍在 - 3.4028235E +38 到 3.4028235E +38 之間。 Single 值儲存最多有效位數為 7 個小數位數的數字資訊。|  
|Smallint|16 位元帶正負號的整數。 *Smallint*實數值型別代表帶正負號的整數值，範圍從負32768到正數32767。|  
|Tinyint|8 位元帶正負號的整數。 Tinyint 值類型代表範圍從負數 128 到正數 127 的整數值。|  
|UnsignedBigInt|64 位元不帶正負號的整數。 *UnsignedBigInt*數值型別代表不帶正負號的整數，其值的範圍從0到18446744073709551615。|  
|UnsignedInt|32 位元不帶正負號的整數。 *UnsignedInt*數值型別代表不帶正負號的整數，其值範圍介於0到4294967295之間。|  
|UnsignedSmallInt|16 位元不帶正負號的整數。 *UnsignedSmallInt*數值型別代表不帶正負號的整數，其值範圍介於0到65535之間。|  
|UnsignedTinyInt|8 位元不帶正負號的整數。 *UnsignedTinyInt*數值型別代表不帶正負號的整數，其值的範圍從0到255|  
|WChar|Unicode 字元的以 Null 結束資料流。 *WChar*是 Unicode 字元的連續集合，用來代表文字。|  
  
## <a name="amo-validations-on-data-types"></a>資料類型的 AMO 驗證  
 下表列出分析管理物件 (AMO) 對某些繫結所做的額外驗證：  
  
|Object|繫結|允許的資料類型|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|二進位以外的所有資料類型|  
||NameColumn|僅 WChar|  
||SkippedLevelsColumn|僅限整數類型：BigInt、整數、SmallInt、TinyInt、UnsignedBigInt、UnsignedInt、UnsignedSmallInt、UnsignedTinyInt|  
||CustomRollupColumn|僅 WChar|  
||CustomRollupPropertiesColumn|僅 WChar|  
||UnaryOperatorColumn|僅 WChar|  
||ValueColumn|全部|  
|AttributeTranslation|CaptionColumn|僅 WChar|  
|ScalarMiningStructureColumn|KeyColumns|二進位以外的所有資料類型|  
||NameColumn|僅 WChar|  
|TableMiningStructureColumn|ForeignKeyColumns|二進位以外的所有資料類型|  
|MeasureGroupAttribute|KeyColumns|二進位以外的所有資料類型|  
|相異計數量值|來源|BigInt、貨幣、Double、整數、Single、SmallInt、TinyInt、UnsignedBigInt、UnsignedInt、UnsignedSmallInt、UnsignedTinyInt|  
  
  
