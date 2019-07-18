---
title: 中斷連接的使用者和工作階段上 Analysis Services 伺服器 |Microsoft Docs
ms.date: 07/05/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 696c6548dadda2412566acf7fae1e2cff2b28095
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624385"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>中斷 Analysis Services 伺服器上的使用者和工作階段連接
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  身為管理員，您可能想要工作負載管理時結束使用者活動。 方法是您可以取消工作階段和連接來達成此目的。 工作階段可在查詢執行時自動形成 (隱含)，或在管理員建立時加以命名 (明確)。 連接就像開啟的導管，可在上面執行查詢。 使用中的工作階段和連接都可以結束。 例如，您可能要結束處理程序的時間太長，則有疑問並正在執行的命令是否撰寫正確處理工作階段。  
  
## <a name="ending-sessions-and-connections"></a>結束工作階段和連接  
 若要管理工作階段和連接，請使用動態管理檢視 (Dmv) 和 XMLA:  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到 Analysis Services 執行個體。  
  
2.  將下列任何一個 DMV 查詢貼入 MDX 查詢視窗中，以取得目前執行之所有工作階段、連接和命令的清單。  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  （此查詢不適用於 Azure Analysis Services）
  
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

取消 SPID/SessionID，將會取消任何作用中命令對應到 SPID/工作階段識別碼的工作階段上執行。 正在取消連接後，會識別與連線相關聯的工作階段，並取消任何作用中的命令，在該工作階段上執行。 在罕見的情況下，不會關閉連線如果引擎無法追蹤所有工作階段與連接相關聯的 Spid比方說，當多個工作階段會開啟一個 HTTP 狀況中。   
  
若要深入了解本主題中所參考之 XMLA，請參閱[Execute Method &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)並[Cancel 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)。  
  
## <a name="see-also"></a>另請參閱  
 [管理連接與工作階段 &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [BeginSession 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [EndSession 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Session 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  
