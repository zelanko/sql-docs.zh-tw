---
title: File 元素 (DTA)
description: 在 DTA 公用程式中，File 元素會指定工作負載檔案，其中包含要針對資料庫微調而執行的 Transact-SQL 陳述式。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- File element
ms.assetid: 73dce835-9a80-4aef-8e0f-9dcf07dd5b80
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 557501bb02cdb3a0b29c1f9654b5414bff6134b5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785973"
---
# <a name="file-element-dta"></a>File 元素 (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

指定工作負載檔。 工作負載是針對需要微調的一或多個資料庫來執行的一組 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 工作負載檔可以是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼 (.sql) 或追蹤檔 (.trc)。 如需詳細資訊，請參閱[啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
  <Server>...</Server>  
  <Workload>  
    <File>...</File>  
  </Workload>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|請利用 **string** 資料類型來指定工作負載檔的目錄路徑。 例如：<br /><br /> `<File>C:\Tuning\tun.sql</File>`<br /><br /> 請注意，伺服器會強制實施長度限制。|  
|**預設值**|無。|  
|**出現次數**|如果未指定任何其他工作負載類型，便需要使用這個元素一次。 您必須指定 **EventString**父系的 **File**、 **Database** 或 **Workload** 子元素，但只能使用一種類型。 例如，如果您利用 **File** 元素指定了工作負載，便不能在相同 XML 輸入檔中，同時利用 **Database** 元素來指定工作負載。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[Workload 元素 &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**子元素**|無。|  
  
## <a name="example"></a>範例  
 如需此元素的使用範例，請參閱[簡單 XML 輸入檔範例 &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
