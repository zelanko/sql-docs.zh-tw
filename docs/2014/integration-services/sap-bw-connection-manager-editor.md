---
title: SAP BW 連接管理員編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ec970319-e749-4753-8675-9cf76ed99669
caps.latest.revision: 9
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dbfeaf04ca7eb8a07637c295a5aa80cc02bedd58
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231455"
---
# <a name="sap-bw-connection-manager-editor"></a>SAP BW 連接管理員編輯器
  使用 [SAP BW 連線管理員編輯器] 可以指定要用來連接到 SAP Netweaver BW 版本 7 系統的屬性。  
  
 SAP BW 連接管理員會提供 SAP Netweaver BW 7 系統的連接，供 SAP BW 來源或目的地使用。 若要深入了解 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW 之 SAP BW 連線管理員的詳細資訊，請參閱 [SAP BW 連線管理員](connection-manager/sap-bw-connection-manager.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟 SAP BW 連接管理員編輯器**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，開啟包含 SAP BW 連線管理員的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [控制流程] 索引標籤上的 [連線管理員] 區域中，執行下列其中一個步驟：  
  
    -   按兩下 SAP BW 連接管理員。  
  
         – 或 –  
  
    -   以滑鼠右鍵按一下 SAP BW 連線管理員，然後選取 [編輯]。  
  
## <a name="options"></a>選項。  
  
> [!NOTE]  
>  如果您不知道設定連接管理員的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 **用戶端**  
 指定系統的用戶端編號。  
  
 **語言**  
 指定系統所使用的語言。 例如，指定 [EN] 代表英文。  
  
 **使用者名稱**  
 指定將用來連接到系統的使用者名稱。  
  
 **密碼**  
 指定將搭配使用者名稱使用的密碼。  
  
 **使用單一應用程式伺服器**  
 連接到單一應用程式伺服器。  
  
 若要連接到負載平衡的伺服器群組，請改用 [使用負載平衡] 選項。  
  
 **主控件**  
 如果要連接到單一應用程式伺服器，請指定主機名稱。  
  
> [!NOTE]  
>  只有當您已選取 [使用單一應用程式伺服器] 選項時，才能使用此選項。  
  
 **系統編號**  
 如果要連接到單一應用程式伺服器，請指定系統編號。  
  
> [!NOTE]  
>  只有當您已選取 [使用單一應用程式伺服器] 選項時，才能使用此選項。  
  
 **使用負載平衡**  
 連接到負載平衡的伺服器群組。  
  
 若要連接到單一應用程式伺服器，請改用 [使用單一應用程式伺服器] 選項。  
  
 **訊息伺服器**  
 如果要連接到負載平衡的伺服器群組，請指定訊息伺服器的名稱。  
  
> [!NOTE]  
>  只有當您已選取 [使用負載平衡] 選項時，才能使用此選項。  
  
 **群組**  
 如果要連接到負載平衡的伺服器群組，請指定伺服器群組的名稱。  
  
> [!NOTE]  
>  只有當您已選取 [使用負載平衡] 選項時，才能使用此選項。  
  
 **SID**  
 如果要連接到負載平衡的伺服器群組，請指定連接的系統識別碼。  
  
> [!NOTE]  
>  只有當您已選取 [使用負載平衡] 選項時，才能使用此選項。  
  
 **記錄目錄**  
 針對 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW 的元件啟用記錄。  
  
 若要啟用記錄，請針對每個 RFC 函數呼叫前後建立的記錄檔指定目錄 (這項記錄功能會使用 XML 格式來建立許多記錄檔。 因為這些記錄檔也包含所有傳輸的資料列，所以這些記錄檔可能會耗用大量磁碟空間)。  
  
> [!IMPORTANT]  
>  如果傳輸的資料包含機密資訊，這些記錄檔也會包含該項機密資訊。  
  
 若要指定記錄目錄，您可以手動輸入目錄路徑，也可以按一下 [瀏覽] 並瀏覽到記錄目錄。  
  
 如果您沒有選取記錄目錄，就不會啟用記錄功能。  
  
 **瀏覽**  
 瀏覽並選取資料夾做為記錄目錄。  
  
 **測試連接**  
 使用您已提供的值來測試連接。 按一下 [測試連接] 之後，就會出現一個訊息方塊，指出連接成功或失敗。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft Connector 1.1 for SAP BW F1 說明](microsoft-connector-for-sap-bw-f1-help.md)  
  
  
