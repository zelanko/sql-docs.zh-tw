---
title: SAP BW 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b780558fc41394d0da8949d33896e5409fbec5b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112238"
---
# <a name="sap-bw-connection-manager"></a>SAP BW 連接管理員
  SAP BW 連接管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的連接管理員元件。 因此，SAP BW 連接管理員會提供 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 來源和目的地元件所需之 SAP Netweaver BW 版本 7 系統的連接 (使用 SAP BW 連線管理員的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 元件只有屬於 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Connector 1.1 for SAP BW 封裝一部分的 SAP BW 來源和目的地)。  
  
> [!IMPORTANT]  
>  Microsoft Connector 1.1 for SAP BW 的文件集是假設使用者已熟悉 SAP Netweaver BW 環境。 如需有關 SAP Netweaver BW 的詳細資訊，或有關如何設定 SAP Netweaver BW 物件與處理序的詳細資訊，請參閱 SAP 文件集。  
  
 當您將 SAP BW 連接管理員加入封裝時，`ConnectionManagerType`連接管理員屬性設定為`SAPBI`。  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>設定 SAP BW 連接管理員  
 您可以利用下列方式設定 SAP BW 連接管理員：  
  
-   提供連接的用戶端、使用者名稱、密碼和語言。  
  
-   選擇要連接到單一應用程式伺服器，還是負載平衡的伺服器群組。  
  
-   提供單一應用程式伺服器的主機和系統編號，或提供負載平衡伺服器群組的訊息伺服器、群組和 SID。  
  
-   針對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 的元件啟用 RFC 函數呼叫的自訂記錄 (這項記錄與您針對 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝啟用的選擇性記錄是分開的)。若要啟用 RFC 函數呼叫的記錄，您必須指定一個目錄，用以儲存每個 RFC 函數呼叫前後建立的記錄檔  (這項記錄功能會使用 XML 格式來建立許多記錄檔。 因為這些記錄檔也包含所有傳輸的資料列，所以這些記錄檔可能會耗用大量磁碟空間)。如果您沒有選取記錄目錄，就不會啟用記錄功能。  
  
    > [!IMPORTANT]  
    >  如果傳輸的資料包含機密資訊，這些記錄檔也會包含該項機密資訊。  
  
-   使用您已輸入的值來測試連接。  
  
 如果您不知道設定連接管理員的所有必要值，可能必須詢問 SAP 系統管理員。  
  
 如需示範如何設定及使用 SAP BW 連接管理員、來源和目的地的逐步解說，請參閱＜ [搭配 SAP BI 7.0 使用 SQL Server 2008 Integration Services](http://go.microsoft.com/fwlink/?LinkID=137090)＞技術白皮書。 這份技術白皮書也會示範如何設定 SAP BW 中的必要物件。  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>使用 SSIS 設計師設定來源  
 如需有關可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之 SAP BW 連接管理員屬性的詳細資訊，請按下列主題：  
  
-   [SAP BW 連線管理員編輯器](../sap-bw-connection-manager-editor.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft Connector 1.1 for SAP BW 元件](../microsoft-connector-for-sap-bw-components.md)  
  
  
