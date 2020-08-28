---
description: AffectEnum
title: AffectEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
author: rothja
ms.author: jroth
ms.openlocfilehash: 9673567c17cda79c93fba4e74b104bd0cb42edd7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976139"
---
# <a name="affectenum"></a>AffectEnum
指定作業會影響哪些記錄。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|如果沒有將 [篩選](./filter-property.md) 套用至 **記錄集**，會影響所有記錄。<br /><br /> 如果 **Filter** 屬性設定為字串準則 (例如 "Author = ' Smith '" ) ，則作業會影響目前章節中的可見記錄。<br /><br /> 如果 **Filter** 屬性設定為 [FilterGroupEnum](./filtergroupenum.md) 的成員或書簽的陣列，則作業會影響 **記錄集**的所有資料列。 **注意： adAffectAll** 會隱藏在 Visual Basic 的物件瀏覽器中。|  
|**adAffectAllChapters**|4|會影響 **記錄集**之所有同級章節中的所有記錄，包括無法透過目前套用的任何 **篩選** 來顯示的記錄。|  
|**adAffectCurrent**|1|只會影響目前的記錄。|  
|**adAffectGroup**|2|只會影響符合目前 [篩選](./filter-property.md) 屬性設定的記錄。 您必須將 **Filter** 屬性設定為 **FilterGroupEnum** 值或 **書簽** 陣列，才能使用此選項。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums 會影響。全部|  
|AdoEnums 會影響 ALLCHAPTERS|  
|AdoEnums 會影響目前的|  
|AdoEnums 會影響到群組|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [CancelBatch 方法 (ADO)](./cancelbatch-method-ado.md)  
        [Delete 方法 (ADO Recordset)](./delete-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [Resync 方法](./resync-method.md)  
        [UpdateBatch 方法](./updatebatch-method.md)  
    :::column-end:::
:::row-end:::