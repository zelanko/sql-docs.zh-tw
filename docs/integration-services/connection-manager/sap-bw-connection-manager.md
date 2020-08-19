---
description: SAP BW 連接管理員
title: SAP BW 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
f1_keywords:
- sql13.dts.designer.sapbwconnectionmanager.f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6a67889df1635e2654adc80151e33a1c137985d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426000"
---
# <a name="sap-bw-connection-manager"></a>SAP BW 連接管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  SAP BW 連接管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的連接管理員元件。 因此，SAP BW 連接管理員會提供 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 來源和目的地元件所需之 SAP Netweaver BW 版本 7 系統的連接 (使用 SAP BW 連線管理員的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 元件只有屬於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Connector 1.1 for SAP BW 封裝一部分的 SAP BW 來源和目的地)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 當您將 SAP BW 連接管理員加入至封裝時，連接管理員的 **ConnectionManagerType** 屬性就會設定為 **SAPBI**。  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>設定 SAP BW 連接管理員  
 您可以利用下列方式設定 SAP BW 連接管理員：  
  
-   提供連接的用戶端、使用者名稱、密碼和語言。  
  
-   選擇要連接到單一應用程式伺服器，還是負載平衡的伺服器群組。  
  
-   提供單一應用程式伺服器的主機和系統編號，或提供負載平衡伺服器群組的訊息伺服器、群組和 SID。  
  
-   針對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的元件啟用 RFC 函數呼叫的自訂記錄 (這項記錄與您針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝啟用的選擇性記錄是分開的)。若要啟用 RFC 函數呼叫的記錄，您必須指定一個目錄，用以儲存每個 RFC 函數呼叫前後建立的記錄檔 (這項記錄功能會使用 XML 格式來建立許多記錄檔。 因為這些記錄檔也包含所有傳輸的資料列，所以這些記錄檔可能會耗用大量磁碟空間)。如果您沒有選取記錄目錄，就不會啟用記錄功能。  
  
    > [!IMPORTANT]  
    >  如果傳輸的資料包含機密資訊，這些記錄檔也會包含該項機密資訊。  
  
-   使用您已輸入的值來測試連接。  
  
 如果您不知道設定連接管理員的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 如需示範如何設定及使用 SAP BW 連接管理員、來源和目的地的逐步解說，請參閱＜ [搭配 SAP BI 7.0 使用 SQL Server 2008 Integration Services](https://go.microsoft.com/fwlink/?LinkID=137090)＞技術白皮書。 這份技術白皮書也會示範如何設定 SAP BW 中的必要物件。  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>使用 SSIS 設計師設定來源  
 如需有關可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之 SAP BW 連接管理員屬性的詳細資訊，請按下列主題：  
  
-   [SAP BW 連接管理員編輯器](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md)  
  
## <a name="sap-bw-connection-manager-editor"></a>SAP BW 連接管理員編輯器
  使用 [SAP BW 連線管理員編輯器]**** 可以指定要用來連接到 SAP Netweaver BW 版本 7 系統的屬性。  
  
 SAP BW 連接管理員會提供 SAP Netweaver BW 7 系統的連接，供 SAP BW 來源或目的地使用。 若要深入了解 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 之 SAP BW 連線管理員的詳細資訊，請參閱 [SAP BW 連線管理員](../../integration-services/connection-manager/sap-bw-connection-manager.md)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 **若要開啟 SAP BW 連接管理員編輯器**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含 SAP BW 連線管理員的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [控制流程]**** 索引標籤上的 [連線管理員] 區域中，執行下列其中一個步驟：  
  
    -   按兩下 SAP BW 連接管理員。  
  
         -或-  
  
    -   以滑鼠右鍵按一下 SAP BW 連線管理員，然後選取 [編輯]****。  
  
### <a name="options"></a>選項。  
  
> [!NOTE]  
>  如果您不知道設定連接管理員的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 **用戶端**  
 指定系統的用戶端編號。  
  
 **語言**  
 指定系統所使用的語言。 例如，指定 [EN]**** 代表英文。  
  
 **使用者名稱**  
 指定將用來連接到系統的使用者名稱。  
  
 **密碼**  
 指定將搭配使用者名稱使用的密碼。  
  
 **使用單一應用程式伺服器**  
 連接到單一應用程式伺服器。  
  
 若要連接到負載平衡的伺服器群組，請改用 [使用負載平衡]**** 選項。  
  
 **主控件**  
 如果要連接到單一應用程式伺服器，請指定主機名稱。  
  
> [!NOTE]  
>  只有當您已選取 [使用單一應用程式伺服器]**** 選項時，才能使用此選項。  
  
 **系統編號**  
 如果要連接到單一應用程式伺服器，請指定系統編號。  
  
> [!NOTE]  
>  只有當您已選取 [使用單一應用程式伺服器]**** 選項時，才能使用此選項。  
  
 **使用負載平衡**  
 連接到負載平衡的伺服器群組。  
  
 若要連接到單一應用程式伺服器，請改用 [使用單一應用程式伺服器]**** 選項。  
  
 **訊息伺服器**  
 如果要連接到負載平衡的伺服器群組，請指定訊息伺服器的名稱。  
  
> [!NOTE]  
>  只有當您已選取 [使用負載平衡]**** 選項時，才能使用此選項。  
  
 **群組**  
 如果要連接到負載平衡的伺服器群組，請指定伺服器群組的名稱。  
  
> [!NOTE]  
>  只有當您已選取 [使用負載平衡]**** 選項時，才能使用此選項。  
  
 **SID**  
 如果要連接到負載平衡的伺服器群組，請指定連接的系統識別碼。  
  
> [!NOTE]  
>  只有當您已選取 [使用負載平衡]**** 選項時，才能使用此選項。  
  
 **記錄目錄**  
 針對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的元件啟用記錄。  
  
 若要啟用記錄，請針對每個 RFC 函數呼叫前後建立的記錄檔指定目錄 (這項記錄功能會使用 XML 格式來建立許多記錄檔。 因為這些記錄檔也包含所有傳輸的資料列，所以這些記錄檔可能會耗用大量磁碟空間)。  
  
> [!IMPORTANT]  
>  如果傳輸的資料包含機密資訊，這些記錄檔也會包含該項機密資訊。  
  
 若要指定記錄目錄，您可以手動輸入目錄路徑，也可以按一下 [瀏覽]**** 並瀏覽到記錄目錄。  
  
 如果您沒有選取記錄目錄，就不會啟用記錄功能。  
  
 **瀏覽**  
 瀏覽並選取資料夾做為記錄目錄。  
  
 **測試連接**  
 使用您已提供的值來測試連接。 按一下 [測試連接]**** 之後，就會出現一個訊息方塊，指出連接成功或失敗。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft Connector for SAP BW 元件](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
  
