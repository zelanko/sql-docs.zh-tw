---
description: Banner 元素 (ssbdiagnose)
title: Banner 元素
diagnose: In SQL Server, the Banner element identifies which utility generated the ssbdiagnose output XML file.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- banner element
- XML output file format [ssbdiagnose], banner element
- ssbdiagnose
ms.assetid: cc6cd49a-acf0-4cfb-8c6a-554692b89de2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: dae521477b4255c6e4f697631960d4647e736f01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484941"
---
# <a name="banner-element-ssbdiagnose"></a>Banner 元素 (ssbdiagnose)


 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

識別產生 **ssbdiagnose** 輸出 XML 檔的公用程式。  
  
## <a name="syntax"></a>語法  
  
```  
  
<Banner  
    title="..."   
    product="..."   
    version="..." />  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|**title**|識別產生 **ssbdiagnose** XML 輸出檔的公用程式。|  
|**product**|識別產生 **ssbdiagnose** XML 輸出檔的產品。|  
|**version**|識別產生 XML 輸出檔的公用程式版本。|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 **ssbdiagnose** 輸出 XML 檔各出現一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[DiagnosticInformation 元素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 這是 banner 元素的範例。  
  
```  
<Banner title="Service Broker Diagnostics Utility" product="Microsoft SQL Server" version="10.0.1073.0" />  
```  
  
## <a name="see-also"></a>另請參閱  
 [ssbdiagnose 公用程式 &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
