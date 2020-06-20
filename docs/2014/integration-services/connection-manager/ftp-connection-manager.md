---
title: FTP 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- FTP connection manager
- connections [Integration Services], FTP
- connection managers [Integration Services], FTP
ms.assetid: c4f43455-29ca-44ba-ac7f-ea729b1daf93
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 02501b845254301a8370fcd208d849a6c6e3e3a9
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920809"
---
# <a name="ftp-connection-manager"></a>FTP 連接管理員
  FTP 連接管理員可讓封裝連接到「檔案傳輸通訊協定 (FTP)」伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 FTP 工作會使用此連線管理員。  
  
 當您將 FTP 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段可解析為 FTP 連接的連接管理員、設定連接管理員屬性，並將連接管理員加入封裝上的 `Connections` 集合。  
  
 連接管理員的 `ConnectionManagerType` 屬性會設為 `FTP`。  
  
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
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的資訊，請參閱 [FTP 連線管理員編輯器](../ftp-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [FTP 工作](../control-flow/ftp-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](integration-services-ssis-connections.md)  
  
  
