---
title: "附加和卸離 Analysis Services 資料庫 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssmsimbi.AttachDatabase.f1
- sql13.asvs.ssms.attachdatabase.f1
- sql13.asvs.ssmsimbi.DetachDatabase.f1
- sql13.asvs.ssms.detachdatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4abef02a67a334486b123a2ed29b8119e7a29f8b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="attach-and-detach-analysis-services-databases"></a>附加和卸離 Analysis Services 資料庫
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]通常很多情況下時[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料庫管理員 (dba) 想要讓資料庫保持離線一段時間中，在相同的伺服器執行個體，或另一部上，然後讓該資料庫恢復連線。 這些情況通常是由商務需求所驅使，例如將資料庫移至不同的磁碟以提升效能、取得讓資料庫成長的空間，或升級產品。 不論是哪一種情況， **Attach** 和 **Detach** 命令都可讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba 輕鬆地將資料庫保持離線並恢復連線狀態。  
  
## <a name="attach-and-detach-commands"></a>Attach 和 Detach 命令  
 **Attach** 命令可讓您將離線的資料庫恢復連線狀態。 您可以將資料庫附加至原始伺服器執行個體或其他執行個體。 當您附加資料庫時，使用者可以指定資料庫的 **[ReadWriteMode]** 設定。 **Detach** 命令可讓您中斷資料庫與伺服器的連線。  
  
## <a name="attach-and-detach-usage"></a>Attach 和 Detach 使用方式  
 **Attach** 命令是用來讓現有的資料庫結構恢復連線狀態。 如果資料庫是以 **ReadWrite** 模式附加，它就只能附加至伺服器執行個體一次。 不過，如果資料庫是以 **ReadOnly** 模式附加，它就可以附加至不同的伺服器執行個體許多次。 不過，相同的資料庫無法附加至相同的伺服器執行個體超過一次。 當您嘗試附加相同的資料庫超過一次時，即使資料已經複製到個別的資料夾，還是會引發錯誤。  
  
> [!IMPORTANT]  
>  如果需要使用密碼才能卸離資料庫，則附加資料庫時也會需要使用相同的密碼。  
  
 **Detach** 命令是用來讓現有的資料庫結構保持離線。 卸離資料庫時，您應該提供密碼來保護機密中繼資料。  
  
> [!IMPORTANT]  
>  為了保護資料檔案的內容，您應該針對資料夾、子資料夾和資料檔案使用存取控制清單。  
  
 當您卸離資料庫時，伺服器會遵循下列步驟進行。  
  
|卸離讀取/寫入資料庫|卸離唯讀資料庫|  
|--------------------------------------|-------------------------------------|  
|1) 伺服器發出在資料庫上執行 CommitExclusive 鎖定的要求<br /><br /> 2) 伺服器等候直到所有進行中的交易都已認可或回復為止<br /><br /> 3) 伺服器建立卸離資料庫所需的所有中繼資料<br /><br /> 4) 資料庫標示為已刪除<br /><br /> 5) 伺服器認可交易|1) 資料庫標示為已刪除<br /><br /> 2) 伺服器認可交易<br /><br /> 注意：您無法針對唯讀資料庫變更卸離密碼。 如果您針對已經包含密碼的卸離資料庫提供密碼參數，就會引發錯誤。|  
  
 **Attach** 和 **Detach** 命令必須當做單一作業執行。 它們無法在同一個交易中與其他作業結合。 此外， **Attach** 和 **Detach** 命令是不可部分完成的交易式命令。 這表示此作業不是成功，就是失敗。 沒有任何資料庫會處於未完成的狀態。  
  
> [!IMPORTANT]  
>  您必須擁有伺服器或資料庫管理員權限才能執行 **Detach** 命令。  
  
> [!IMPORTANT]  
>  您必須擁有伺服器管理員權限才能執行 **Attach** 命令。  
  
## <a name="see-also"></a>請參閱  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [移動 Analysis Services 資料庫](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [資料庫 Readwritemode](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [切換 ReadOnly 和 ReadWrite 模式之間的 Analysis Services 資料庫](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Detach 元素](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Attach 元素](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  
