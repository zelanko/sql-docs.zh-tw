---
title: "SAP BW 來源 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 749afb64-3567-4dc9-8431-783d650c25db
caps.latest.revision: "10"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2e7a2f3ea58e0237ce5e037306223c6231fd12fd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sap-bw-source"></a>SAP BW 來源
  SAP BW 來源是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的來源元件。 因此，SAP BW 來源會從 SAP Netweaver BW 版本 7 系統中擷取資料，並將這項資料提供給 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中的資料流程。  
  
 此來源有一個輸出和一個錯誤輸出。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
> [!IMPORTANT]  
>  擷取 SAP Netweaver BW 中的資料需要額外的 SAP 授權。 請洽詢 SAP 以確認這些需求。  
  
 若要使用 SAP BW 來源，您必須執行下列工作：  
  
-   [準備 SAP Netweaver BW 物件](#bkmk_Prepare_Objects)  
  
-   [連接到 SAP Netweaver BW 系統](#bkmk_Connect_Database)  
  
-   [設定 SAP BW 來源](#bkmk_Configure_Source)  
  
##  <a name="bkmk_Prepare_Objects"></a> 準備來源所需的 SAP Netweaver BW 物件  
 SAP BW 來源要求特定物件必須存在 SAP Netweaver BW 系統中，然後來源才能運作。 如果這些物件原本不存在，您就必須遵循下列步驟，在 SAP Netweaver BW 系統中建立並設定這些物件。  
  
> [!NOTE]  
>  如需有關這些物件和這些組態設定步驟的其他詳細資料，請參閱 SAP Netweaver BW 文件集。  
  
1.  透過 SAP GUI 登入 SAP Netweaver BW、輸入交易代碼 SM59，並且建立 RFC 目的地：  
  
    1.  針對 [連接類型]，選取 [TCP/IP]。  
  
    2.  針對 **[啟動類型]**，選取 **[已註冊的伺服器程式]**。  
  
    3.  針對 [目標系統的通訊類型]，選取 [非 Unicode (非使用中 MDMP 設定)]。  
  
    4.  指派適當的程式識別碼。  
  
2.  建立開放式中心目的地 (Open Hub Destination)：  
  
    1.  移至 Administrator Workbench (交易代碼 RSA1)，並且在左窗格中，選取 [開放式中心目的地]。  
  
    2.  在中間窗格中，以滑鼠右鍵按一下 InfoArea，然後選取 [建立開放式中心目的地]。  
  
    3.  針對 **[目的地類型]**，選取 **[協力廠商工具]**，然後輸入先前建立的 RFC 目的地。  
  
    4.  儲存並啟用新的開放式中心目的地。  
  
3.  建立資料傳輸處理序 (DTP)：  
  
    1.  在 InfoArea 的中間窗格中，以滑鼠右鍵按一下先前建立的目的地，然後選取 [建立資料傳輸處理序]。  
  
    2.  設定、儲存並啟用 DTP。  
  
    3.  在功能表上，按一下 **[移至]**，然後按一下 **[批次管理員的設定]**。  
  
    4.  將 **[處理序數目]** 更新為 1，進行序列處理。  
  
4.  建立處理序鏈結：  
  
    1.  設定處理序鏈結時，請選取 **[使用中繼資料鏈結或 API 啟動]** 做為 **[啟動處理序]** 的 **[排程選項]**，然後加入先前建立的 DTP 做為後續節點。  
  
    2.  儲存並啟用處理序鏈結。  
  
     SAP BW 來源可以呼叫處理序鏈結以啟用資料傳輸處理序。  
  
##  <a name="bkmk_Connect_Database"></a> 連接到 SAP Netweaver BW 系統  
 為了連接到 SAP Netweaver BW 版本 7 系統，SAP BW 來源會使用屬於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 封裝一部分的 SAP BW 連接管理員。 SAP BW 連接管理員是 SAP BW 來源可以使用的唯一 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 連接管理員。  
  
 如需有關 SAP BW 連接管理員的詳細資訊，請參閱＜ [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md)＞。  
  
##  <a name="bkmk_Configure_Source"></a> 設定 SAP BW 來源  
 您可以利用下列方式設定 SAP BW 來源：  
  
-   查閱並選取要用來擷取資料的開放式中心服務 (Open Hub Service，OHS) 目的地。  
  
-   選取下列其中一種方法來擷取資料：  
  
    -   觸發處理序鏈結。 在此情況下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝會啟動擷取處理序。  
  
    -   等候來自 SAP Netweaver BW 系統的通知，以便開始擷取。 在此情況下，SAP Netweaver BW 系統會啟動擷取處理序。  
  
    -   擷取與特定要求識別碼相關聯的資料。 在此情況下，SAP Netweaver BW 系統已經將資料擷取到內部資料表，而且 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝剛剛讀取資料。  
  
-   根據選取的資料擷取方法，提供下列其他資訊：  
  
    -   針對 [P - 觸發處理鏈結] 選項，提供閘道器主機名稱、閘道器服務名稱、RFC 目的地的程式識別碼，以及處理序鏈結的名稱。  
  
    -   針對 [W - 等候通知] 選項，提供閘道器主機名稱、閘道器伺服器名稱，以及 RFC 目的地的程式識別碼。 您也可以指定逾時 (以秒為單位)。 逾時就是來源將等候收到通知的最大期限。  
  
    -   針對 [E - 僅限擷取] 選項，提供要求識別碼。  
  
-   指定字串轉換的規則 (例如，根據 SAP Netweaver BW 系統是否為 Unicode 而轉換所有字串，或將所有字串轉換為 **varchar** 或 **nvarchar**)。  
  
-   使用您已選取的選項來預覽要擷取的資料。  
  
 您也可以針對來源的 RFC 函數呼叫啟用記錄 (這項記錄與您針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝啟用的選擇性記錄是分開的)。您可以在設定來源將使用的 SAP BW 連接管理員時啟用 RFC 函數呼叫的記錄。 如需有關如何設定 SAP BW 連接管理員的詳細資訊，請參閱＜ [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md)＞。  
  
 如果您不知道設定來源的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 如需示範如何設定及使用 SAP BW 連接管理員、來源和目的地的逐步解說，請參閱＜ [搭配 SAP BI 7.0 使用 SQL Server 2008 Integration Services](http://go.microsoft.com/fwlink/?LinkID=137090)＞技術白皮書。 這份技術白皮書也會示範如何設定 SAP BW 中的必要物件。  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>使用 SSIS 設計師設定來源  
 如需有關可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之 SAP BW 來源屬性的詳細資訊，請按下列其中一個主題：  
  
-   [SAP BW 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)  
  
-   [SAP BW 來源編輯器 &#40;資料行頁面&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)  
  
-   [SAP BW 來源編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)  
  
-   [SAP BW 來源編輯器 &#40;進階頁面&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)  
  
 設定 SAP BW 來源時，您也可以使用各種對話方塊來查閱 SAP Netweaver BW 物件或預覽來源資料。 如需有關這些對話方塊的詳細資訊，請按下列其中一個主題：  
  
-   [查閱 RFC 目的地](../../integration-services/data-flow/look-up-rfc-destination.md)  
  
-   [查閱 ProcessChain](../../integration-services/data-flow/look-up-process-chain.md)  
  
-   [要求記錄檔](../../integration-services/data-flow/request-log.md)  
  
-   [預覽](../../integration-services/data-flow/preview.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft Connector for SAP BW 元件](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
