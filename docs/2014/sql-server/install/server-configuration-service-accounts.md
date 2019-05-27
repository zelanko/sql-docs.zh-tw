---
title: 伺服器組態-服務帳戶 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- service account configuration, SQL Server
ms.assetid: c283702d-ab20-4bfa-9272-f0c53c31cb9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8435b0c677f80bf4f26acd4411d90ab63c7473d1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092264"
---
# <a name="server-configuration---service-accounts"></a>伺服器組態 - 服務帳戶
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈的 [伺服器組態] 頁面，即可為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務指派登入帳戶。 設定在這個頁面上的實際服務隨著您選取要安裝的功能而不同。  
  
 用來啟動並執行的啟動帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以是超連結"ms help://SQL11_I1033/s11sq_GetStart_I/html/309b9dac-0b3a-4617-85ef-c4519ce9d014.htm"\l"Domain_User 「 網域使用者帳戶、 本機使用者帳戶、 受管理的服務帳戶虛擬帳戶或內建系統帳戶。  
  
## <a name="options"></a>選項  
 您可以將相同登入帳戶指派給所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務，或個別設定每一個服務帳戶。 此外，您也可以指定要自動啟動服務、手動啟動服務或停用服務。 大部分安裝都建議使用預設帳戶。  
  
 在 Windows 7 和 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 上，大部分帳戶都預設為虛擬帳戶。  
  
 如果您將服務設定為使用網域帳戶，[!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您個別設定服務帳戶，以便為每一個服務提供最低權限，其中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務會被授與完成其工作所需的最低權限。 如需詳細資訊，包括帳戶類型的說明，請參閱 [設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
 **設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]個別服務帳戶 （建議選項）**  
 使用此方格來為每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務提供登入使用者名稱和密碼，並為該服務設定啟動類型。 您可以將內建系統帳戶、本機帳戶、本機群組、網域群組或是網域使用者帳戶用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
 選取下列任何一項服務來自訂其設定。  
  
|選取這項服務|設定驗證設定|  
|-------------------------|----------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|執行作業、監視、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]及允許自動化管理工作的服務。<br /><br /> 此服務沒有預設登入帳戶。<br /><br /> 預設啟動類型為 [手動]。|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|預設啟動類型為 [自動]。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|預設啟動類型為 [自動]。<br /><br /> 若為 SharePoint 整合模式，您必須指定 Windows 網域使用者帳戶。 您所指定的帳戶會用於 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務。 您針對目前執行個體所指定的帳戶也必須用於之後加入至相同伺服陣列的任何其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|服務帳戶是用來設定報表伺服器資料庫連接。 如果您想要使用預設驗證設定，請選擇內建的網路服務。 如果您指定網域使用者帳戶，並且正在報表伺服器上使用 Windows 驗證，請務必註冊此帳戶的服務主要名稱 (SPN)。 如需詳細資訊，請參閱 [設定報表伺服器上的 Windows 驗證](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)。<br /><br /> 預設啟動類型為 [自動]。|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 是一組圖形化工具和可程式化物件，用來移動、複製和轉換資料。<br /><br /> 預設啟動類型為 [自動]。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|用於 Distributed Replay Client 服務的服務帳戶。<br /><br /> 提供用以執行 Distributed Replay Client 服務的帳戶。 這個帳戶應該與您用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶不同。<br /><br /> 預設啟動類型為 [手動]。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|用於 Distributed Replay Controller 服務的服務帳戶。<br /><br /> 提供用以執行 Distributed Replay Controller 服務的帳戶。 這個帳戶應該與您用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶不同。<br /><br /> 預設啟動類型為 [手動]。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文檢索篩選背景程式啟動器|建立 fdhost.exe 處理序的服務。 這是主控處理全文檢索索引之文字資料的斷詞工具與篩選的必要項目。<br /><br /> 如果您提供了用以執行 FDHOST 啟動器服務的網域帳戶，我們強烈建議您使用低權限帳戶。 這個帳戶應該與您用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶不同。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 是提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接資訊給用戶端電腦的名稱解析服務。 這項服務會在多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行個體之間共用。 預設登入帳戶為 NT Authority\Local service，而且無法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間加以變更。 您可以在安裝完成之後變更此帳戶。 如果沒有在安裝期間指定啟動類型，系統就會依照下列方式決定啟動類型：<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 設定為 [自動] 並在下列所述的安裝狀況中執行：<br />-<br />                            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體<br />-<br />                            啟用 TCP 或 NP 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具名執行個體<br />-<br />                            Analysis Server 的具名執行個體而且未建立叢集<br /><br /> 如果上述狀況都不適用，而且已經安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser，就會維持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 的目前狀態。<br /><br /> 啟動類型設定為 [停用]，而且如果在安裝之前，沒有舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體存在，就會停止。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 安裝的安全性考量](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
