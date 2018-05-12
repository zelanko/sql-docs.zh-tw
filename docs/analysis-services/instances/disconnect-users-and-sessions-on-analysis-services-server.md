---
title: 中斷使用者的連線工作階段上 Analysis Services 伺服器和 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 99072a36fe65679dbf81aa0ba3f4efdb3b487533
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>中斷 Analysis Services 伺服器上的使用者和工作階段連接
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的管理員在執行工作負載管理時，可以選擇結束使用者活動。 方法是您可以取消工作階段和連接來達成此目的。 工作階段可在查詢執行時自動形成 (隱含)，或在管理員建立時加以命名 (明確)。 連接就像開啟的導管，可在上面執行查詢。 使用中的工作階段和連接都可以結束。 例如，處理時間如果太長，或對於執行的命令是否撰寫正確有疑問時，管理員可以結束工作階段的處理。  
  
## <a name="ending-sessions-and-connections"></a>結束工作階段和連接  
 若要管理工作階段和連接，您可以使用動態管理檢視 (DMV) 和 XMLA：  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 Analysis Services 執行個體。  
  
2.  將下列任何一個 DMV 查詢貼入 MDX 查詢視窗中，以取得目前執行之所有工作階段、連接和命令的清單。  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  
  
     `Select * from $System.Discover_Commands`  
  
3.  按 F5 執行查詢。  
  
     DMV 查詢會以易於閱讀和複製的表格形式，傳回工作階段與連接資訊的結果集。  
  
 讓查詢視窗保持開啟狀態。 在下一步中，您需要回到這個頁面，複製您要中斷連接之工作階段的 SPID。  
  
 若要結束工作階段，請開啟第二個 XMLA 查詢視窗。  
  
1.  將下列語法貼入 MDX 查詢視窗，並將 ConnectionID、SessionID 或 SPID 預留位置，以上一個步驟複製的有效值取代。  
  
    ```  
    <Cancel xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  
       <ConnectionID>111</ConnectionID>  
       <SessionID>222</SessionID>  
       <SPID>333</SPID>  
  
    <CancelAssociated>1</CancelAssociated>  
    </Cancel>  
  
    ```  
  
2.  按 F5 執行取消命令。  
  
 結束連接會取消所有工作階段與 SPID，並關閉主機工作階段。  
  
 結束工作階段會停止當做該工作階段一部分執行的所有命令 (SPID)。  
  
 結束 SPID 會取消一個特定命令。  
  
 在罕見的情況下，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 若無法追蹤與連接相關聯的所有工作階段和 SPID，則不會關閉連接 (例如，當某個 HTTP 案例中開啟了多個工作階段時)。  
  
 如需本主題中所參考之 XMLA 的詳細資訊，請參閱 [Execute 方法 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md) 和 [Cancel 元素 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理連接和工作階段 & #40;XMLA & #41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [BeginSession 元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)   
 [EndSession 元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)   
 [Session 元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)  
  
  
