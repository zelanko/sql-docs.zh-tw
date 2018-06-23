---
title: 資料庫 Readwritemode |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], read/write
- databases [Analysis Services], read-only
ms.assetid: 03d7cb5c-7ff0-4e15-bcd2-7075d1b0dd69
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f8a655c379f512f882534166a8c561524e02ce88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033123"
---
# <a name="database-readwritemodes"></a>資料庫 ReadWriteMode
  通常在很多情況下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫管理員 (dba) 會想要將讀取/寫入資料庫變更為唯讀資料庫，反之亦然。 這些情況通常是由商務需求所驅使，例如在許多伺服器之間共用相同的資料庫資料夾，以便向外延展方案並改善效能。 這些情況下，`ReadWriteMode`資料庫屬性可讓[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]dba 輕易地變更資料庫作業模式。  
  
## <a name="readwritemode-database-property"></a>ReadWriteMode 資料庫屬性  
 `ReadWriteMode` 資料庫屬性會指定資料庫處於讀取/寫入模式或唯讀模式。 此屬性只有這兩種可能的值。 當資料庫處於唯讀模式時，您就無法將任何變更或更新套用至該資料庫。 不過，當資料庫處於讀取/寫入模式時，您就可以進行變更和更新。 `ReadWriteMode`資料庫屬性定義為唯讀屬性，則它只能透過設定`Attach`命令。  
  
 當資料庫處於唯讀模式時，就會產生特定限制，因而影響一般允許對資料庫進行的作業集合。 請參閱下表以便了解這些限制的作業。  
  
|ReadOnly 模式|限制的作業|  
|-------------------|---------------------------|  
|XML/A 命令<br /><br /> <br /><br /> 注意：當您執行其中一個命令時，就會引發錯誤。|`Create`<br /><br /> `Alter`<br /><br /> `Delete`<br /><br /> `Process`<br /><br /> `MergePartitions`<br /><br /> `DesignAggregations`<br /><br /> `CommitTransaction`<br /><br /> `Restore`<br /><br /> `Synchronize`<br /><br /> `Insert`<br /><br /> `Update`<br /><br /> `Drop`<br /><br /> <br /><br /> 注意：允許在設定為唯讀的資料庫中進行資料格回寫作業，但是無法認可變更。|  
|MDX 陳述式<br /><br /> <br /><br /> 注意：當您執行其中一個陳述式時，就會引發錯誤。|`COMMIT TRAN`<br /><br /> `CREATE SESSION CUBE`<br /><br /> `ALTER CUBE`<br /><br /> `ALTER DIMENSION`<br /><br /> `CREATE DIMENSION MEMBER`<br /><br /> `DROP DIMENSION MEMBER`<br /><br /> `ALTER DIMENSION`<br /><br /> <br /><br /> 注意： 由於該功能在內部實作使用 Excel 使用者無法使用群組功能，在樞紐分析表`CREATE SESSION CUBE`命令。|  
|DMX 陳述式<br /><br /> <br /><br /> 注意：當您執行其中一個陳述式時，就會引發錯誤。|`CREATE [SESSION] MINING STRUCTURE`<br /><br /> `ALTER MINING STRUCTURE`<br /><br /> `DROP MINING STRUCTURE`<br /><br /> `CREATE [SESSION] MINING MODEL`<br /><br /> `DROP MINING MODEL`<br /><br /> `IMPORT`<br /><br /> `SELECT INTO`<br /><br /> `INSERT`<br /><br /> `UPDATE`<br /><br /> `DELETE`|  
|背景作業|任何修改資料庫的背景作業都會被停用。 這包括延遲處理以及主動式快取。|  
  
## <a name="readwritemode-usage"></a>ReadWriteMode 使用方式  
 `ReadWriteMode` 資料庫屬性是要當做 `Attach` 資料庫命令的一部分使用。 `Attach`命令允許此資料庫屬性設定為 `ReadWrite`或`ReadOnly`。 您無法直接更新 `ReadWriteMode` 資料庫屬性值，因為此屬性定義為唯讀。 建立資料庫時，其 `ReadWriteMode` 屬性會設定為 `ReadWrite`。 您無法在唯讀模式下建立資料庫。  
  
 若要切換`ReadWriteMode`資料庫之間的屬性`ReadWrite`和`ReadOnly`，您必須發出一連串`Detach/Attach`命令。  
  
 所有資料庫作業，但`Attach`，保留`ReadWriteMode`資料庫處於目前狀態的屬性。 例如，`Alter`、`Backup`、`Restore` 和 `Synchronize` 等作業會保留 `ReadWriteMode` 值。  
  
> [!NOTE]  
>  您可以從唯讀資料庫建立本機 Cube。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [附加和卸離 Analysis Services 資料庫](attach-and-detach-analysis-services-databases.md)   
 [移動 Analysis Services 資料庫](move-an-analysis-services-database.md)   
 [Detach 元素](../xmla/xml-elements-commands/detach-element.md)   
 [Attach 元素](../xmla/xml-elements-commands/attach-element.md)  
  
  