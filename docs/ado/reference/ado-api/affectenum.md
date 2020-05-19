---
title: AffectEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 06d3234317e38177defeacdf6f258bc2301dde9e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747043"
---
# <a name="affectenum"></a>AffectEnum
指定哪些記錄會受到作業影響。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|如果沒有套用到**記錄集**的[篩選](../../../ado/reference/ado-api/filter-property.md)，會影響所有記錄。<br /><br /> 如果**Filter**屬性設定為字串準則（例如 "Author = ' Smith '"），則作業會影響目前章節中的可見記錄。<br /><br /> 如果**Filter**屬性設定為[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)或書簽陣列的成員，則作業將會影響**記錄集**的所有資料列。 **注意：** Visual Basic 物件瀏覽器中會隱藏 adAffectAll。|  
|**adAffectAllChapters**|4|會影響**記錄集**所有同輩章節中的所有記錄，包括無法透過目前套用的任何**篩選器**看到的所有記錄。|  
|**adAffectCurrent**|1|只會影響目前的記錄。|  
|**adAffectGroup**|2|只會影響符合目前[篩選](../../../ado/reference/ado-api/filter-property.md)屬性設定的記錄。 您必須將**Filter**屬性設定為**FilterGroupEnum**值或**書簽**陣列，才能使用此選項。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums。會影響所有|  
|AdoEnums。會影響 ALLCHAPTERS|  
|AdoEnums。會影響目前的|  
|AdoEnums。影響群組|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|[Delete 方法 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|  
|[Resync 方法](../../../ado/reference/ado-api/resync-method.md)|[UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)|
