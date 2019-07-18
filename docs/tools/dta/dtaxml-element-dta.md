---
title: DTAXML 元素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DTAXML element
ms.assetid: 3d9942ed-8a27-40db-a7c9-808984d914a2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8bc5977952c32fdf4fa6b81bae20068ab47bb97a
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729415"
---
# <a name="dtaxml-element-dta"></a>DTAXML 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Database Engine Tuning Advisor XML 輸入或輸出檔的根元素， **DTAXML** 包含說明 Database Engine Tuning Advisor 所產生之微調輸入和微調輸出的所有元素。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAXML   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
    xmlns="https://schemas.microsoft.com/sqlserver/2004/07/dta">  
    ...code removed here...  
</DTAXML>  
```  
  
## <a name="element-attributes"></a>元素屬性  
  
|attribute|Description|  
|---------------|-----------------|  
|**xmlns:xsi**|必要。 識別 XML 結構描述執行個體命名空間。 這個命名空間的屬性用來參考驗證 Database Engine Tuning Advisor XML 檔時所用的結構描述。<br /><br /> 必要值：[http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)|  
|**xmlns**|必要。 識別 Database Engine Tuning Advisor 命名空間。<br /><br /> 如果您利用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 XML 編輯器來編輯 Database Engine Tuning Advisor，[F1 說明和動態說明] 便會利用這個值，在《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中，尋找可能的參考主題。<br /><br /> 必要值：<br /><br /> [Database Engine Tuning Advisor XML 結構描述](https://go.microsoft.com/fwlink/?LinkId=43100) 命名空間|  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|Description|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 DTA XML 檔需要使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|None|  
|**子元素**|[DTAInput 元素 &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)<br /><br /> **DTAOutput** 元素 (相關資訊請參閱 [Database Engine Tuning Advisor XML 結構描述](https://schemas.microsoft.com/sqlserver/))|  
  
## <a name="remarks"></a>Remarks  
 如需有關 XML 命名空間的詳細資訊，請參閱 [MSDN Library 中的＜](https://go.microsoft.com/fwlink/?LinkId=7341) XML 文件中的命名空間 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ＞(英文)。  
  
## <a name="example"></a>範例  
 如需一般 **DTAXML** 元素的範例，請參閱 [XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考 &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)   
 [啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)  
  
  
