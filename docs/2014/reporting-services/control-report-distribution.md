---
title: 控制報表散發 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- subscriptions [Reporting Services], e-mail
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- subscriptions [Reporting Services], security
- mail [Reporting Services]
ms.assetid: 8f15e2c6-a647-4b05-a519-1743b5d8654c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a72f9d943a883a70c7dcf0476b92c6cb5b678f21
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946444"
---
# <a name="control-report-distribution"></a>控制報表散發
  您可以設定報表伺服器，以減少與電子郵件和檔案共用散發相關聯的安全性風險。  
  
## <a name="securing-reports"></a>保護報表的安全  
 控制報表散發的第一個步驟是保護報表的安全，以避免未授權的存取。 若要在訂閱中使用，報表對個別傳遞都必須使用相同的預存認證組。 可以存取報表伺服器上之報表的任何使用者，都可以執行報表，並可能散發報表。 若要避免發生此情況，您必須限制只有需要報表的使用者才可以存取報表。 如需詳細資訊，請參閱 <<c0> [ 保護報表和資源](security/secure-reports-and-resources.md)並[保護資料夾的](security/secure-folders.md)。  
  
 使用資料庫安全性以授權存取的高度機密報表，無法透過訂閱方式散發。  
  
> [!IMPORTANT]  
>  報表會當成檔案傳輸。 適用於檔案的風險和保護，同樣適用於儲存在磁碟或當做附加檔案傳送的報表。 任何對檔案有存取權的使用者都可以自由地散發或使用檔案。  
  
## <a name="controlling-e-mail-delivery"></a>控制電子郵件傳遞  
 您可以設定報表伺服器，來限制只能散發電子郵件至特定主機網域。 例如，您可以防止報表伺服器將報表傳遞至 RSReportServer 組態檔中所列網域以外的所有網域。  
  
 您也可以組態組態設定，以隱藏訂閱中的 [收件者] 欄位。 在此情況下，報表只會傳遞給定義訂閱的使用者。 然而，在報表傳送給使用者之後，您無法明確地防止其被轉送。  
  
 控制報表散發最有效的方式，是將報表伺服器設定為只傳送報表伺服器 URL。 報表伺服器使用 Windows 驗證和以角色為基礎的驗證模型，來控制對報表的存取。 如果使用者意外地透過電子郵件接收到未被授權檢視的報表，報表伺服器將不會顯示報表。  
  
## <a name="controlling-file-share-delivery"></a>控制檔案共用傳遞  
 檔案共用傳遞用於傳送報表到硬碟中的檔案。 檔案儲存至磁碟後，就不再受到報表伺服器用於控制使用者存取之以角色為基礎的安全性模型的規範。 若要保護已傳遞至磁碟的報表，您可以為檔案本身或包含檔案的資料夾加上存取控制清單 (ACL)。 視您的作業系統而定，可能有其他的安全性選項。  
  
## <a name="see-also"></a>另請參閱  
 [為電子郵件傳遞設定報表伺服器&#40;SSRS 組態管理員&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [建立及管理原生模式報表伺服器的訂閱](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)  
  
  
