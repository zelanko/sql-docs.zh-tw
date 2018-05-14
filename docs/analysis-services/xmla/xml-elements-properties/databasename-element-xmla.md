---
title: DatabaseName 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9cbf32fcc67c7a9e08d45d6099bf58bf521be6e2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="databasename-element-xmla"></a>DatabaseName 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  識別[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]父系所要還原的資料庫[還原](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)命令。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Restore>  
   ...  
   <DatabaseName>...</DatabaseName>  
   ...  
</Restore>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **DatabaseName**元素會識別資料庫所在**還原**命令還原的備份檔案。 如果您沒有指定這個元素，或者它包含空字串，系統就會使用備份檔案中包含的資料庫名稱。  
  
 如果資料庫已經存在目標執行個體上，除非發生錯誤**AllowOverwrite**父項目**還原**命令設定為**True**。  
  
## <a name="see-also"></a>另請參閱  
 [AllowOverwrite 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)   
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
