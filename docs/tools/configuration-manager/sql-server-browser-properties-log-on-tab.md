---
title: SQL Server Browser 屬性 (登入索引標籤)
description: 了解 [SQL Server 瀏覽器屬性] 對話方塊的 [登入] 索引標籤。 了解如何使用此索引標籤來指定帳戶，以及啟動或停止服務。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c77871ec-c2f4-4e4a-9a10-5aeb4ae70507
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 13c448b6f856b8c7027bcf044bc9fd8688533948
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897809"
---
# <a name="sql-server-browser-properties-log-on-tab"></a>SQL Server Browser 屬性 (登入索引標籤)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 程式會以伺服器服務的方式執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 會接聽 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源的內送要求，並提供有關電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資訊。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器會接聽 UDP 通訊埠，並接受使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) 的未驗證要求。  
  
 帳戶密碼的變更會立即生效，不需要重新啟動服務。  
  
## <a name="options"></a>選項。  
 **本機系統帳戶**  
 在本機系統帳戶的安全性內容執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。 如果可能的話，請另外使用權限較低的帳戶來執行。  
  
 **這個帳戶**  
 指定使用 Windows 驗證的本機或網域使用者帳戶。 建議您使用具有最少服務權限的網域使用者帳戶。 如需有關選取帳戶的資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜設定 Windows 服務帳戶＞。  
  
 **瀏覽**  
 瀏覽使用者或內建的安全性主體。  
  
> [!IMPORTANT]  
>  請使用低權限的帳戶。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務所需權限的資訊，請參閱 [SQL Server Browser 服務](../../tools/configuration-manager/sql-server-browser-service.md)的＜安全性＞一節。  
  
 **密碼**  
 輸入安全性主體的密碼。  
  
 **確認密碼**  
 確認安全性主體的密碼。  
  
 **服務狀態**  
 表示這項服務為執行中、已停止或已停用。 " **...** " 表示狀態變更已暫止。  
  
 **啟動**  
 啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器服務。  
  
 **停止**  
 停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
 **暫停**  
 暫停 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務。  
  
 **繼續**  
 繼續已暫停的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器服務。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Browser 服務](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
