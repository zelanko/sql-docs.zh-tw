---
title: SAP BW 來源編輯器 (連線管理員頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2a6dc531-85ca-43c5-a65f-3ad3f7d537c4
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c5993cfd66502310035a16325eb2e56bb0c698c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146987"
---
# <a name="sap-bw-source-editor-connection-manager-page"></a>SAP BW 來源編輯器 (連接管理員頁面)
  使用 **[SAP BW 來源編輯器]** 的 **[連接管理員]** 頁面可以選取 SAP BW 來源的 SAP BW 連接管理員。 在這個頁面上，您也可以選取執行模式以及從 SAP Netweaver BW 系統中擷取資料所用的參數。  
  
 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的 SAP BW 來源元件，請參閱 [SAP BW 來源](sap-bw-source.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
> [!IMPORTANT]  
>  擷取 SAP Netweaver BW 中的資料需要額外的 SAP 授權。 請洽詢 SAP 以確認這些需求。  
  
 **開啟連接管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 來源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤上，按兩下 SAP BW 來源。  
  
3.  在 **[SAP BW 來源編輯器]** 中，按一下 **[連接管理員]** 開啟編輯器的 **[連接管理員]** 頁面。  
  
## <a name="static-options"></a>靜態選項  
  
> [!NOTE]  
>  如果您不知道設定來源的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 **SAP BW 連接管理員**  
 從清單中選取現有的連線管理員，或按一下 [新增] 來建立新的連線。  
  
 **新增**  
 使用 [SAP BW 連線管理員] 對話方塊來建立新的連線管理員。  
  
 如需有關此對話方塊的詳細資訊，請參閱＜ [SAP BW Connection Manager Editor](../sap-bw-connection-manager-editor.md)＞。  
  
 **OHS 目的地**  
 選取要從來源中擷取資料所用的開放式中心服務 (Open Hub Service，OHS) 目的地。  
  
 **執行模式**  
 指定從來源中擷取資料的方法。  
  
|選項|描述|  
|------------|-----------------|  
|**P - 觸發處理鏈結**|觸發處理序鏈結。 在此情況下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝會啟動擷取處理序。|  
|**W - 等候通知**|等候來自 SAP Netweaver BW 系統的通知，以便開始擷取資料。 在此情況下，SAP Netweaver BW 系統會啟動擷取處理序。|  
|**E - 僅限擷取**|擷取與特定要求識別碼相關聯的資料。 在此情況下，SAP Netweaver BW 系統已經將資料擷取到內部資料表中，而且 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝剛剛讀取資料。|  
  
 **預覽**  
 開啟 [預覽] 對話方塊，以便預覽結果。 如需詳細資訊，請參閱 [Preview](preview.md)。  
  
> [!IMPORTANT]  
>  [SAP BW 來源編輯器] 之 **[連接管理員]** 頁面上提供的 **[預覽]** 選項會實際擷取資料。 如果您已將 SAP Netweaver BW 設定為僅擷取自從上次擷取以來已變更的資料，則選取 **[預覽]** 將會從下次擷取中排除已預覽的資料。  
  
 當您按一下 **[預覽]** 時，也會開啟 **[要求記錄檔]** 對話方塊。 您可以使用此對話方塊來檢視對 SAP Netweaver BW 系統提出資料取樣要求期間記錄的事件。 如需詳細資訊，請參閱 [Request Log](request-log.md)。  
  
## <a name="execution-mode-dynamic-options"></a>執行模式動態選項  
  
> [!NOTE]  
>  如果您不知道設定來源的所有必要值，可能必須詢問 SAP 系統管理員。  
  
### <a name="execution-mode--p---trigger-process-chain"></a>執行模式 = P - 觸發處理鏈結  
  
#### <a name="rfc-destination-options"></a>RFC 目的地選項  
 您不需要事先了解並輸入這些值。 使用 **[查閱]** 按鈕，即可尋找並選取適當的 RFC 目的地。 在您選取 RFC 目的地之後，此元件就會針對這些選項輸入適當的值。  
  
 **閘道器主機**  
 輸入閘道器主機的伺服器名稱或 IP 位址。 此名稱或 IP 位址通常與 SAP 應用程式伺服器相同。  
  
 **閘道器服務**  
 輸入閘道服務的名稱格式`sapgwNN`，其中`NN`是系統編號。  
  
 **程式識別碼**  
 輸入與 RFC 目的地相關聯的程式識別碼。  
  
 **查閱**  
 使用 [查閱 RFC 目的地] 對話方塊來查閱 RFC 目的地。 如需有關此對話方塊的詳細資訊，請參閱＜ [Look Up RFC Destination](look-up-rfc-destination.md)＞。  
  
#### <a name="process-chain-options"></a>處理序鏈結選項  
 您不需要事先了解並輸入這些值。 使用 **[查閱]** 按鈕，即可尋找並選取適當的處理序鏈結。 在您選取處理序鏈結之後，此元件就會針對選項輸入適當的值。  
  
 **處理序鏈結**  
 輸入要由來源觸發之處理序鏈結的名稱。  
  
 **查閱**  
 使用 [查閱 ProcessChain] 對話方塊來查閱處理序鏈結。 如需有關此對話方塊的詳細資訊，請參閱＜ [Look Up Process Chain](look-up-process-chain.md)＞。  
  
### <a name="execution-mode--w---wait-for-notify"></a>執行模式 = W - 等候通知  
  
#### <a name="rfc-destination-options"></a>RFC 目的地選項  
 您不需要事先了解並輸入這些值。 使用 **[查閱]** 按鈕，即可尋找並選取適當的 RFC 目的地。 在您選取 RFC 目的地之後，此元件就會針對這些選項輸入適當的值。  
  
 **閘道器主機**  
 輸入閘道器主機的伺服器名稱或 IP 位址。 此名稱或 IP 位址通常與 SAP 應用程式伺服器相同。  
  
 **閘道器服務**  
 輸入閘道服務的名稱格式`sapgwNN`，其中`NN`是系統編號。  
  
 **程式識別碼**  
 輸入與 RFC 目的地相關聯的程式識別碼。  
  
 **查閱**  
 使用 [查閱 RFC 目的地] 對話方塊來查閱 RFC 目的地。 如需有關此對話方塊的詳細資訊，請參閱＜ [Look Up RFC Destination](look-up-rfc-destination.md)＞。  
  
### <a name="execution-mode--e---extract-only"></a>執行模式 = E - 僅限擷取  
 **要求識別碼**  
 輸入與擷取相關聯的要求識別碼。  
  
## <a name="see-also"></a>另請參閱  
 [SAP BW 來源編輯器&#40;資料行頁面&#41;](sap-bw-source-editor-columns-page.md)   
 [SAP BW 來源編輯器 &#40;錯誤輸出頁面&#41;](sap-bw-source-editor-error-output-page.md)   
 [SAP BW 來源編輯器 &#40;進階頁面&#41;](sap-bw-source-editor-advanced-page.md)   
 [Microsoft Connector 1.1 for SAP BW F1 說明](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  