---
title: 工作負載元素（DTA） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e81ea0aac9cfe7676abba18bc7dffb2e1561597b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62678716"
---
# <a name="workload-element-dta"></a>Workload 元素 (DTA)
  指定微調工作階段所用的工作負載。  
  
## <a name="syntax"></a>語法  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|**資料類型和長度**|無。|  
|**預設值**|無。|  
|**出現次數**|每個 `DTAInput` 元素需要使用這個元素一次。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|--------------|  
|**父元素**|[啟動及使用 Database Engine Tuning Advisor](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**子元素**|[File 元素 &#40;DTA&#41;](file-element-dta.md)<br /><br /> [工作負載的 Database 元素 &#40;DTA&#41;](database-element-for-workload-dta.md)<br /><br /> [EventString 元素 &#40;DTA&#41;](eventstring-element-dta.md)|  
  
## <a name="remarks"></a>備註  
 工作負載是針對需要微調的一或多個資料庫來執行的一組 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 Database Engine Tuning Advisor 可以利用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼、追蹤檔和追蹤資料表來作為工作負載。  
  
 如果您在 XML 輸入檔中指定工作負載，以及在命令列中利用 **dta** 工具來指定工作負載，就會利用命令列所指定的工作負載來進行微調。 命令列所指定的所有微調選項都會覆寫 XML 輸入檔中所指定的微調選項。 XML 輸入檔中以評估模式輸入的使用者指定組態是唯一例外。 例如，如果在 XML 輸入檔的 `Configuration` 元素中輸入了某項組態，`EvaluateConfiguration` 元素也指定成某個微調選項，XML 輸入檔所指定的微調選項會覆寫在命令列中輸入的任何微調選項。  
  
 每個微調工作階段都必須指定一個工作負載。  
  
## <a name="example"></a>範例  
 下列程式碼範例會指定`Workload`元素的**MyDatabase. mydatabase.mydbowner.tuningtable001. TuningTable001**追蹤資料表。 搭配 SQL Server Profiler 使用微調範本來建立 **TuningTable001** ，並將這份追蹤輸出儲存成一份資料表。  
  
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
 [XML 輸入檔參考XML Input File ReferenceDatabase Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
