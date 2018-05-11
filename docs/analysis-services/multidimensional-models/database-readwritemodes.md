---
title: 資料庫 Readwritemode |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 506d3ed7bbc5664ef974e1d2c3aca0dfb7f3a9b0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="database-readwritemodes"></a>資料庫 ReadWriteMode
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  通常在很多情況下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫管理員 (dba) 會想要將讀取/寫入資料庫變更為唯讀資料庫，反之亦然。 這些情況通常是由商務需求所驅使，例如在許多伺服器之間共用相同的資料庫資料夾，以便向外延展方案並改善效能。 在這些情況下， **ReadWriteMode** 資料庫屬性可讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba 輕易地變更資料庫作業模式。  
  
## <a name="readwritemode-database-property"></a>ReadWriteMode 資料庫屬性  
 **ReadWriteMode** 資料庫屬性會指定資料庫處於讀取/寫入模式或唯讀模式。 此屬性只有這兩種可能的值。 當資料庫處於唯讀模式時，您就無法將任何變更或更新套用至該資料庫。 不過，當資料庫處於讀取/寫入模式時，您就可以進行變更和更新。 **ReadWriteMode** 資料庫屬性定義為唯讀屬性。您只能透過 [連結] 命令來設定它。  
  
 當資料庫處於唯讀模式時，就會產生特定限制，因而影響一般允許對資料庫進行的作業集合。 請參閱下表以便了解這些限制的作業。  
  
|ReadOnly 模式|限制的作業|  
|-------------------|---------------------------|  
|XML/A 命令<br /><br /> <br /><br /> 注意：當您執行其中一個命令時，就會引發錯誤。|**建立**<br /><br /> **Alter**<br /><br /> **Delete**<br /><br /> **處理**<br /><br /> **MergePartitions**<br /><br /> **DesignAggregations**<br /><br /> **CommitTransaction**<br /><br /> **Restore**<br /><br /> **同步處理**<br /><br /> **Insert**<br /><br /> **Update**<br /><br /> **Drop**<br /><br /> <br /><br /> 注意：允許在設定為唯讀的資料庫中進行資料格回寫作業，但是無法認可變更。|  
|MDX 陳述式<br /><br /> <br /><br /> 注意：當您執行其中一個陳述式時，就會引發錯誤。|**COMMIT TRAN**<br /><br /> **CREATE SESSION CUBE**<br /><br /> **ALTER CUBE**<br /><br /> **ALTER DIMENSION**<br /><br /> **CREATE DIMENSION MEMBER**<br /><br /> **DROP DIMENSION MEMBER**<br /><br /> **ALTER DIMENSION**<br /><br /> <br /><br /> 注意：Excel 使用者無法在樞紐資料表中使用群組功能，因為該項功能是使用 **CREATE SESSION CUBE** 命令在內部實作的。|  
|DMX 陳述式<br /><br /> <br /><br /> 注意：當您執行其中一個陳述式時，就會引發錯誤。|**CREATE [SESSION] MINING STRUCTURE**<br /><br /> **ALTER MINING STRUCTURE**<br /><br /> **DROP MINING STRUCTURE**<br /><br /> **CREATE [SESSION] MINING MODEL**<br /><br /> **DROP MINING MODEL**<br /><br /> **IMPORT**<br /><br /> **SELECT INTO**<br /><br /> **INSERT**<br /><br /> **UPDATE**<br /><br /> **DELETE**|  
|背景作業|任何修改資料庫的背景作業都會被停用。 這包括延遲處理以及主動式快取。|  
  
## <a name="readwritemode-usage"></a>ReadWriteMode 使用方式  
 **ReadWriteMode** 資料庫屬性是要當做 **Attach** 資料庫命令的一部分使用。 **Attach** 命令允許此資料庫屬性設定為 **ReadWrite** 或 **ReadOnly**。 您無法直接更新 **ReadWriteMode** 資料庫屬性值，因為此屬性定義為唯讀。 建立資料庫時，其 **ReadWriteMode** 屬性會設定為 **ReadWrite**。 您無法在唯讀模式下建立資料庫。  
  
 若要在 **ReadWrite** 和 **ReadOnly** 之間切換 **ReadWriteMode** 資料庫屬性，您必須發出一連串的 [中斷連結/連結] 命令。  
  
 所有資料庫作業 ( **Attach**除外) 都會將 **ReadWriteMode** 資料庫屬性保持在目前狀態。 例如， **Alter**、 **Backup**、 **Restore**和 **Synchronize** 等作業會保留 **ReadWriteMode** 值。  
  
> [!NOTE]  
>  您可以從唯讀資料庫建立本機 Cube。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加和卸離 Analysis Services 資料庫](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [移動 Analysis Services 資料庫](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Detach 元素](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Attach 元素](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  
