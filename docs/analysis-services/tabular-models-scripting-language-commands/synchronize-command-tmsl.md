---
title: Synchronize 命令 (TMSL) |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4265e6fa1e2214fae53cacdb084e152005eb3647
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033271"
---
# <a name="synchronize-command-tmsl"></a>Synchronize 命令 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  同步處理 Analysis Services 資料庫與另一個現有的資料庫。  
  
## <a name="request"></a>要求  
 接受的 JSON 屬性同步處理的命令如下所示。  
  
```  
{   
   "synchronize":{   
      "database":"AdventureWorksDW_Production",  
      "source":"Provider=MSOLAP.7;Data Source=localhost;Integrated Security=SSPI;Initial Catalog=AdventureWorksDW_Dev",  
      "synchronizeSecurity":"copyAll",  
      "applyCompression":true  
   }  
}  
```  
  
 接受的 JSON 屬性同步處理的命令如下所示。  
  
||||  
|-|-|-|  
|**屬性**|**預設值**|**說明**|  
|[資料庫]||同步處理資料庫物件的名稱。|  
|來源||要用來連線到來源伺服器的連接字串。|  
|synchronizeSecurity|skipMembership|列舉值，指定如何還原安全性定義，包括角色和權限。 有效值包括 skipMembership copyAll、 和 ignoreSecurity。|  
|applyCompression|True|布林值，若為 true，表示同步處理作業; 期間，將會套用壓縮否則為 false。|  
  
## <a name="response"></a>回應  
 命令成功時，會傳回空的結果。 否則，傳回 XMLA 例外狀況。  
  
## <a name="usage-endpoints"></a>使用方式 （端點）  
 陳述式中使用這個命令項目[Execute Method &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md)透過 XMLA 公開的端點，以下列方式呼叫：  
  
-   為 XMLA 視窗中 SQL Server Management Studio (SSMS)  
  
-   為輸入檔案**叫用 ascmd** PowerShell cmdlet  
  
-   做為 SSIS 工作或 SQL Server Agent 作業的輸入  
  
 您可以從 SSMS 產生現成的指令碼，此命令，依序按一下 [同步處理資料庫] 對話方塊中的 [指令碼] 按鈕。  
  
 [ \[MS-SSAS-T\]: SQL Server Analysis Services 表格式 （SQL Server 技術通訊協定）](http://go.microsoft.com/fwlink/p/?LinkId=784855)文件包含區段 3.1.5.2.2 描述 JSON 表格式中繼資料命令和物件的結構。 目前，該文件所涵蓋的命令和功能尚未實作用於 TMSL 指令碼。 請參閱主題[表格式模型指令碼語言&#40;TMSL&#41;參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)如需所支援的釐清  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
