---
title: "FTP 連接管理員 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 04cc47e64fbbaec3f1e1df9216ead850efa75b90
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="ftp-connection-manager"></a>FTP 連接管理員
  FTP 連接管理員可讓封裝連接到「檔案傳輸通訊協定 (FTP)」伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含的 FTP 工作使用此連線管理員。  
  
 當您將 FTP 連線管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段可解析為 FTP 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上的 **Connections** 集合。  
  
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
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的資訊，請參閱 [FTP 連線管理員編輯器](../../integration-services/connection-manager/ftp-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連線](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [FTP 工作](../../integration-services/control-flow/ftp-task.md)   
 [Integration Services &#40;SSIS &#41;連線](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
