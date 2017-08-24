---
title: "SAP BW 來源編輯器 （資料行頁面） |Microsoft 文件"
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
- sql13.dts.designer.sapbwsource.columns.f1
ms.assetid: c2ec8bb7-be9b-4783-ad88-32512de784b0
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2047fddb6986bd3014015d742053bfb0dda42019
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-source-editor-columns-page"></a>SAP BW 來源編輯器 (資料行頁面)
  使用 [SAP BW 來源編輯器] 的 [資料行] 頁面可以將輸出資料行對應至每個外部 (來源) 資料行。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 來源元件，請參閱 [SAP BW 來源](../../integration-services/data-flow/sap-bw-source.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
> [!IMPORTANT]  
>  擷取 SAP Netweaver BW 中的資料需要額外的 SAP 授權。 請洽詢 SAP 以確認這些需求。  
  
 **開啟資料行頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 來源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 SAP BW 來源。  
  
3.  在 **[SAP BW 來源編輯器]**中，按一下 **[資料行]** 開啟編輯器的 **[資料行]** 頁面。  
  
## <a name="options"></a>選項。  
  
> [!NOTE]  
>  如果您不知道設定來源的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 **可用的外部資料行**  
 檢視資料來源中可用的外部資料行清單，然後選取要包含在資料流程中的資料行。  
  
 若要在資料流程中包含資料行，請選取對應至該資料行的核取方塊。 您選取核取方塊的順序會決定資料行的輸出順序。 也就是說，您所選取的第一個核取方塊就是第一個輸出資料行，第二個核取方塊就是第二個輸出資料行，依此類推。  
  
 **外部資料行**  
 檢視選取的外部 (來源) 資料行。 當您設定從這個來源取用資料的下游元件時，選取的資料行會按照其對應輸出資料行的顯示順序出現。  
  
 若要變更資料行的順序，請在 **[可用的外部資料行]** 清單中，清除所有資料行的核取方塊。 然後，按照您想要讓資料行出現的順序選取資料行。  
  
 **輸出資料行**  
 為每個輸出資料行提供唯一的名稱。 預設值是選取之外部 (來源) 資料行的名稱。 不過，您可以輸入任何唯一的描述性名稱。 [!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具將顯示**輸出資料行**設定從這個來源取用資料的下游元件時的資料行的名稱。  
  
## <a name="see-also"></a>請參閱＜  
 [SAP BW 來源編輯器 &#40;連接管理員頁面 &#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [SAP BW 來源編輯器 &#40;錯誤輸出頁面 &#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [SAP BW 來源編輯器 &#40;進階的頁面 &#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)   
 [Microsoft Connector for SAP BW F1 說明](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
