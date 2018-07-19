---
title: MaxActiveConnections 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d8543a36b12bbbbc1bf5427ae8960ac5c634b7ab
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34033815"
---
# <a name="maxactiveconnections-element-assl"></a>MaxActiveConnections 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含衍生自項目所允許的同時連線數目上限[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)資料型別。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSource>  
   ...  
   <MaxActiveConnections>...</MaxActiveConnections>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|Integer|  
|預設值|**10**|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果這個元素的值設定為零，最大並行連接數目就會由用來存取資料來源的資料夾決定。 如果這個元素的值設定為負值，最大並行連接數目就是無限制。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
