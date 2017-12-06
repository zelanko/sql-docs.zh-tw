---
title: "Workload 元素 (DTA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b4f3f970e0239367de10389f103d74e08f5ae90
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="workload-element-dta"></a>Workload 元素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]指定要用於微調工作階段的工作負載。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 **DTAInput** 元素需要使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**子元素**|[File 元素 &#40;DTA&#41;](../../tools/dta/file-element-dta.md)<br /><br /> [工作負載的 Database 元素 &#40;DTA&#41;](../../tools/dta/database-element-for-workload-dta.md)<br /><br /> [EventString 元素 &#40;DTA&#41;](../../tools/dta/eventstring-element-dta.md)|  
  
## <a name="remarks"></a>備註  
 工作負載是針對需要微調的一或多個資料庫來執行的一組 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 Database Engine Tuning Advisor 可以利用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼、追蹤檔和追蹤資料表來作為工作負載。  
  
 如果您在 XML 輸入檔中指定工作負載，以及在命令列中利用 **dta** 工具來指定工作負載，就會利用命令列所指定的工作負載來進行微調。 命令列所指定的所有微調選項都會覆寫 XML 輸入檔中所指定的微調選項。 XML 輸入檔中以評估模式輸入的使用者指定組態是唯一例外。 例如，如果在 XML 輸入檔的 **Configuration** 元素中輸入了某項組態， **EvaluateConfiguration** 元素也指定成一個微調選項，XML 輸入檔所指定的微調選項會覆寫在命令列中輸入的任何微調選項。  
  
 每個微調工作階段都必須指定一個工作負載。  
  
## <a name="example"></a>範例  
 下列程式碼範例指定 **Workload** 元素的 **MyDatabase.MyDBOwner.TuningTable001** 追蹤資料表。 搭配 SQL Server Profiler 使用微調範本來建立 **TuningTable001** ，並將這份追蹤輸出儲存成一份資料表。  
  
```  
<DTAXML ...>  
  <DTAInput>  
    <Server>  
...code removed here...  
    </Server>  
    <Workload>  
      <Database>  
        <Name>MyDatabase</Name>  
        <Schema>  
          <Name>MyDBOwner</Name>  
            <Table>  
              <Name>TuningTable001</Name>  
            </Table>  
        </Schema>  
      </Database>  
    </Workload>  
...code removed here...  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>另請參閱  
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
