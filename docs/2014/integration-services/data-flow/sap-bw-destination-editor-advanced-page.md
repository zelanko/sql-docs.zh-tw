---
title: SAP BW 目的地編輯器 (進階頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 862957db-bbc6-4dda-bc0e-591457f1baa7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 404fdbe10430e09ad2be96ec31b45c4bbf563260
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159608"
---
# <a name="sap-bw-destination-editor-advanced-page"></a>SAP BW 目的地編輯器 (進階頁面)
  使用 SAP BW 目的地編輯器的 [進階] 頁面可以設定進階設定，例如封裝大小和逾時資訊。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 目的地，請參閱 [SAP BW 目的地](sap-bw-destination.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟進階頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 目的地的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。  
  
2.  在 [資料流程] 索引標籤中，按兩下 SAP BW 目的地。  
  
3.  在 SAP BW 目的地編輯器中，按一下 [進階] 開啟編輯器的 [進階] 頁面。  
  
## <a name="options"></a>選項。  
  
> [!NOTE]  
>  如果您不知道設定目的地的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 **封裝大小**  
 指定一次會傳輸多少個資料列。 這個參數的最佳值取決於 SAP Netweaver BW 系統以及可能進行的其他資料處理。 一般而言，介於 2000 到 20000 之間的值可提供最佳效能。  
  
 **觸發處理序鏈結**  
 (選擇性) 指定要在資料載入完成後觸發之處理序鏈結的名稱。  
  
 **等候 InfoPackage 的逾時**  
 指定目的地應該等候 InfoPackage 完成的秒數上限。  
  
 **等候資料傳送結束**  
 指定目的地是否應該等候直到 SAP Netweaver BW 系統完成資料載入為止。  
  
 **不要啟動 InfoPackage (僅等候)**  
 指定目的地不會觸發 InfoPackage，而是只會等候 SAP Netweaver BW 系統已開始載入資料的通知。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 目的地編輯器&#40;連線管理員頁面&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [SAP BW 目的地編輯器&#40;對應頁面&#41;](sap-bw-destination-editor-mappings-page.md)   
 [SAP BW 目的地編輯器 &#40;錯誤輸出頁面&#41;](sap-bw-destination-editor-error-output-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 說明](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
