---
description: FTP 連接管理員
title: FTP 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 854f975c64f5622c53d04c51651929d83745864a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91728039"
---
# <a name="ftp-connection-manager"></a>FTP 連接管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  FTP 連接管理員可讓封裝連接到「檔案傳輸通訊協定 (FTP)」伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 FTP 工作會使用此連線管理員。  
  
 當您將 FTP 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段可解析為 FTP 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上的 **Connections** 集合。  
  
 連線管理員的 **ConnectionManagerType** 屬性會設為 [FTP]。  
  
 您可以利用下列方式設定 FTP 連接管理員：  
  
-   指定伺服器名稱和伺服器通訊埠。  
  
-   指定匿名存取，或提供基本驗證的使用者名稱和密碼。  
  
    > [!IMPORTANT]  
    >  FTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
-   設定逾時、重試次數，以及一次複製的資料數量。  
  
-   指示 FTP 連接管理員使用被動還是主動模式。  
  
 依據 FTP 連接管理員連接之 FTP 站台的組態而定，您可能必須變更連接管理員的下列預設值：  
  
-   伺服器通訊埠設定為 21。 您應該指定 FTP 站台接聽的通訊埠。  
  
-   使用者名稱設定為 "anonymous"。 您應該提供 FTP 站台需要的認證。  
  
## <a name="activepassive-modes"></a>主動/被動模式  
 FTP 連接管理員可使用主動模式或使用被動模式來傳送和接收檔案。 在主動模式中，伺服器會起始資料連接，而在被動模式中，用戶端會起始資料連接。  
  
## <a name="configuration-of-the-ftp-connection-manager"></a>設定 FTP 連接管理員  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的資訊，請參閱 [FTP 連線管理員編輯器]()。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="ftp-connection-manager-editor"></a>FTP 連接管理員編輯器
  使用 [FTP 連線管理員編輯器] 對話方塊來指定連接到 FTP 伺服器的屬性。  
  
> [!IMPORTANT]  
>  FTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 若要深入了解 FTP 連線管理員，請參閱 [FTP 連線管理員](../../integration-services/connection-manager/ftp-connection-manager.md)。  
  
### <a name="options"></a>選項。  
 **伺服器名稱**  
 提供 FTP 伺服器的名稱。  
  
 **伺服器通訊埠**  
 指定 FTP 伺服器上用來連接的通訊埠編號。 這個屬性的預設值為 **21**。  
  
 **使用者名稱**  
 提供存取 FTP 伺服器的使用者名稱。 這個屬性的預設值為 **匿名**。  
  
 **密碼**  
 提供存取 FTP 伺服器的密碼。  
  
 **逾時 (以秒為單位)**  
 指定工作在逾時之前所花的秒數。值為 **0** 指出無限的時間量。 這個屬性的預設值為 **60**。  
  
 **使用被動模式**  
 指定伺服器或用戶端是否起始連接。 伺服器會以主動模式起始連接，而用戶端則會以被動模式啟動連接。 此屬性的預設值為 **主動模式**。  
  
 **重試**  
 指定工作嘗試連接的次數。 值為 **0** 指出不限制嘗試次數。  
  
 **區塊大小 (以 KB 為單位)**  
 提供以 KB 為單位的傳輸資料區塊大小。  
  
 **測試連接**  
 設定 FTP 連線管理員之後，請按一下 [測試連接] 以確認連接是可行的。  
  
## <a name="see-also"></a>另請參閱  
 [FTP 工作](../../integration-services/control-flow/ftp-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
