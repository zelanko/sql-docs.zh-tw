---
title: Analysis Services DAX 屬性 |Microsoft Docs
ms.date: 10/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 20a6df833f8c525c24abdf3bb51278d0067db951
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62509646"
---
# <a name="dax-properties"></a>DAX 屬性
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

   Msmdsrv.ini 的 DAX 區段包含用來控制 Analysis Services 中的特定查詢行為，例如 DAX 查詢結果集中所傳回的資料列數目上限的設定。

  針對非常大型的資料列集 (例如 DirectQuery 模型中所傳回的資料列集)，一百萬個資料列的預設值可能不足。 您知道是否需要調整，如果您收到這個錯誤限制：「 外部資料來源的查詢的結果集已超過允許的 '1000000' 的資料列的大小上限。 」

若要增加上限，請指定 **MaxIntermediateRowSize** 組態設定。 您必須手動將整個元素加入組態檔的 DAX 區段。 加入前，檔案中不會有此設定。

## <a name="configuration-snippet"></a>組態程式碼片段

```
<ConfigurationSettings>
. . .
<DAX>
  <PredicateCheckSpoolCardinalityThreshold>5000
  </PredicateCheckSpoolCardinalityThreshold>
  <DQ>
     <MaxIntermediateRowsetSize>1000000
     </MaxIntermediateRowsetSize>
  </DQ>
</DAX>
. . .
```

## <a name="property-descriptions"></a>屬性描述

設定 |值 |描述
--------|-------|-----------
MaxIntermediateRowsetSize | 1000000 | DAX 查詢中所傳回的最大資料列數目。 手動將此項目加入 msmdsrv.ini 檔案，如果預設值太低，請增加此值。
PredicateCheckSpoolCardinalityThreshold| 5000 | 此為進階屬性，除非在 Microsoft 支援人員的指導之下，否則不應隨意變更。

如需其他伺服器屬性以及如何設定伺服器屬性的詳細資訊，請參閱 [Analysis Services 中的伺服器屬性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。
