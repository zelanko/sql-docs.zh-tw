---
title: "SAP BW 目的地編輯器 （對應頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwdestination.columns.f1
ms.assetid: dfa1f1d6-6b64-4331-bdc5-eaa8b7aa41a1
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 245ff83f84ff1a60a08f4a73d24ee76179b31e2b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-destination-editor-mappings-page"></a>SAP BW 目的地編輯器 (對應頁面)
  使用 [SAP BW 目的地編輯器] 的 [對應] 頁面可以將輸入資料行對應至目的地資料行。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目的地，請參閱 [SAP BW 目的地](../../integration-services/data-flow/sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **開啟對應頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程] 索引標籤中，按兩下 SAP BW 目的地。  
  
3.  在 [SAP BW 目的地編輯器] 中，按一下 [對應] 開啟編輯器的 [對應] 頁面。  
  
## <a name="options"></a>選項。  
  
> [!NOTE]  
>  如果您不知道設定目的地的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 [SAP BW 目的地編輯器] 的 [對應] 頁面包含兩個區段：  
  
-   上方區段會顯示可用的輸入和目的地資料行，並且讓您建立這兩種資料行類型之間的對應。  
  
-   下方區段是一份資料表，其中列出哪些輸入資料行已經對應至哪些輸出資料行。  
  
### <a name="upper-section-options"></a>上方區段選項  
 上方區段具有下列選項：  
  
 **可用的輸入資料行**  
 檢視可用的輸入資料行清單。  
  
 若要將輸入資料行對應至目的地資料行，請從 [可用的輸入資料行] 清單中拖曳資料行，並且將該資料行放入 [可用的目的地資料行] 清單中的資料行。  
  
 **可用的目的地資料行**  
 檢視可用的目的地資料行清單。  
  
 若要將輸入資料行對應至目的地資料行，請從 [可用的輸入資料行] 清單中拖曳資料行，並且將該資料行放入 [可用的目的地資料行] 清單中的資料行。  
  
 上方區段也具有操作功能表，而且您可以在背景上按一下滑鼠右鍵，即可開啟此功能表。 這個操作功能表包含下列選項：  
  
-   **選取全部對應**  
  
-   **刪除選取的對應**  
  
-   **藉由比對名稱來對應項目**  
  
### <a name="lower-section-columns"></a>下方區段資料行  
 下方區段是對應的資料表，而且具有下列資料行：  
  
 **輸入資料行**  
 檢視您已選取的輸入資料行。  
  
 若要將不同的輸入資料行對應至相同的目的地資料行，請在清單中選取不同的輸入資料行。 若要移除對應，請選取**\<忽略 >**從輸出排除輸入資料行。  
  
 **目的地資料行**  
 檢視每個可用的目的地資料行，不論該資料行是否已經對應。  
  
## <a name="see-also"></a>請參閱＜  
 [SAP BW 目的地編輯器 &#40;連接管理員頁面 &#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 目的地編輯器 &#40;錯誤輸出頁面 &#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [SAP BW 目的地編輯器 &#40;進階的頁面 &#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
