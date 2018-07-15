---
title: 執行帳戶 （SSRS 原生模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.executionaccount.F1
ms.assetid: 440b5a09-5fd4-4c3a-b510-f3c33cbf1c82
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e18c8c37eba48fa2732a07f4906137cdd299fdd3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312808"
---
# <a name="execution-account-ssrs-native-mode"></a>執行帳戶 (SSRS 原生模式)
  使用此頁面，即可設定自動處理所使用的帳戶。 當其他認證來源無法使用的特殊情況下，請使用此帳戶：  
  
-   當報表伺服器連接到不需要認證的資料來源時。 可能不需要認證的資料來源範例包括 XML 文件和某些用戶端資料庫應用程式。  
  
-   當報表伺服器連接到另一個伺服器，以擷取報表中所參考的外部影像檔或其他資源時。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 原生模式。  
  
 設定這個帳戶是選擇性的，但若未設定此帳戶，當您使用外部影像及連接某些資料來源時，將會受到限制。 擷取外部影像檔時，報表伺服器會檢查是否可以建立匿名連接。 如果連接有密碼保護，報表伺服器便會使用自動報表處理帳戶連接到遠端伺服器。 擷取報表的資料時，報表伺服器會模擬目前使用者、提示使用者提供認證、使用預存認證，或如果資料來源連接指定認證類型為 **[無]** 時，則會使用自動處理帳戶。 報表伺服器不允許系統在連接到其他電腦時，委派或模擬其服務帳戶認證，因此如果沒有其他認證可以使用，報表伺服器就必須使用自動處理帳戶。  
  
 您所指定的帳戶應該與用於執行服務帳戶的帳戶不同。 如果您設定此帳戶，則會以加密值儲存於 RSReportServer.config 檔案中。 如果您在向外延展部署中執行報表伺服器，您必須在每一部報表伺服器上使用相同的方式設定此帳戶。  
  
 您可以使用任何 Windows 使用者帳戶。 為求最佳效果，請選擇擁有讀取權限及網路登入權限的帳戶，以連接到其他電腦。 此帳戶必須擁有您想在報表中使用之任何外部影像或資料檔案的讀取權限。 除非所有的報表資料來源和外部影像全都儲存在報表伺服器電腦上，否則請勿指定本機帳戶。 這種帳戶只適用於自動報表處理。  
  
> [!NOTE]  
>  如果您正在使用 [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] with Advanced Services，當您在報表中參考外部影像，而需要有存取該影像檔的權限時，您就只需要設定此帳戶。 SQL Server Express 不支援遠端伺服器的資料來源連接。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2012 版本支援的功能](http://go.microsoft.com/fwlink/?linkid=232473)。  
  
 若要開啟此頁面，請啟動[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]組態管理員，並選取**執行帳戶**瀏覽窗格中。 如需詳細資訊，請參閱 [Reporting Services 組態管理員 &#40;原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>選項。  
 **指定執行帳戶**  
 選取此項目來指定帳戶。  
  
 **帳戶**  
 輸入 Windows 網域使用者帳戶。 請使用此格式：\<網域\\<使用者帳戶\>。  
  
 **密碼**  
 輸入密碼。  
  
 **確認密碼**  
 重新輸入密碼。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態管理員 F1 說明主題&#40;SSRS 原生模式&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [儲存加密的報表伺服器資料 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
  
  
