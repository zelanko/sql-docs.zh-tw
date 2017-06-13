---
title: "錯誤和事件參考 (Reporting Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- messages [Reporting Services]
- errors [Reporting Services]
- Reporting Services, errors and events
- troubleshooting [Reporting Services], errors
- events [Reporting Services]
ms.assetid: 818b4cc1-e65d-4f1a-bf7d-fe269e6dd739
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a0738c8ac950a86ef877c26fd8b6a0f6a6b075f2
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="errors-and-events-reference-reporting-services"></a>錯誤和事件參考 (Reporting Services)
  本主題提供有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]錯誤和事件的資訊。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 記錄檔也包含錯誤資訊。 如需有關可用記錄檔類型及如何檢視記錄的詳細資訊，請參閱 [Reporting Services 記錄檔和來源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Reporting Services 錯誤訊息的原因和解決方案  
 此處提供最常在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 網站上搜尋之錯誤的原因和解決方案資訊。 如需詳細資訊，請參閱 [Reporting Services 錯誤的原因和解決方案](../../reporting-services/troubleshooting/cause-and-resolution-of-reporting-services-errors.md)。  
  
## <a name="report-server-events"></a>報表伺服器事件  
 下列報表伺服器事件會記錄在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄中。  
  
|事件識別碼|型別|類別目錄|Source|說明|  
|--------------|----------|--------------|------------|-----------------|  
|106|錯誤|排程|報表伺服器|當您定義排程作業時 (例如，報表訂閱和傳遞)，必須執行 SQL Server Agent。|  
|[107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)|錯誤|啟動/關閉|報表伺服器<br /><br /> 排程與傳遞處理器|*\<來源 >*無法連接到報表伺服器資料庫。 如需詳細資訊，請參閱[報表伺服器 Windows 服務 &#40;MSSQLServer&#41; 107](../../reporting-services/troubleshooting/report-server-windows-service-mssqlserver-107.md)。|  
|108|錯誤|延伸模組|報表伺服器<br /><br /> 報表管理員|*\<來源 >*傳遞、 資料處理或轉譯延伸模組無法載入。<br /><br /> 最可能的情況是因為延伸模組的部署不完整或遭移除所造成的結果。 如需詳細資訊，請參閱 [部署資料處理延伸模組](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md) 和 [部署傳遞延伸模組](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)。|  
|109|資訊|管理|報表伺服器<br /><br /> 報表管理員|組態檔已經修改。 如需詳細資訊，請參閱 [Reporting Services 組態檔案](../../reporting-services/report-server/reporting-services-configuration-files.md)。|  
|110|警告|管理|報表伺服器<br /><br /> 報表管理員|組態檔其中之一的設定已經修改，因此不再有效。 會改用預設值。 如需詳細資訊，請參閱 [Reporting Services 組態檔案](../../reporting-services/report-server/reporting-services-configuration-files.md)。|  
|111|錯誤|記錄|報表伺服器<br /><br /> 報表管理員|*\<來源 >*無法建立追蹤記錄檔。 如需詳細資訊，請參閱 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。|  
|112|警告|Security|報表伺服器|報表伺服器偵測到可能的阻斷服務攻擊。 如需詳細資訊，請參閱 [Reporting Services 安全性與保護](../../reporting-services/security/reporting-services-security-and-protection.md)。|  
|113|錯誤|記錄|報表伺服器|報表伺服器無法建立效能計數器。|  
|114|錯誤|啟動/關閉|報表管理員|「報表管理員」無法連接到「報表伺服器」服務。|  
|115|警告|排程|排程與傳遞處理器|SQL Server Agent 佇列的排程工作已經修改或刪除。|  
|116|錯誤|內部|報表伺服器<br /><br /> 報表管理員<br /><br /> 排程與傳遞處理器|發生內部錯誤。|  
|117|錯誤|啟動/關閉|報表伺服器|報表伺服器資料庫是無效的版本。|  
|118|警告|記錄|報表伺服器<br /><br /> 報表管理員|追蹤記錄不在預期的目錄位置；將在預設目錄建立新的追蹤記錄。 如需詳細資訊，請參閱 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。|  
|119|錯誤|啟用|報表伺服器<br /><br /> 排程與傳遞處理器|*\<來源 >*未被授權存取報表伺服器資料庫的內容。|  
|120|錯誤|啟用|報表伺服器|對稱金鑰無法解密。 最可能的情況是因為，伺服器執行的帳戶已經變更。 如需詳細資訊，請參閱[設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
|121|錯誤|啟動/關閉|報表伺服器|遠端程序呼叫 (RPC) 服務啟動失敗。|  
|122|警告|傳遞|排程與傳遞處理器|「排程與傳遞處理器」無法連接到作為電子郵件傳遞的 SMTP 伺服器。 如需有關 SMTP 伺服器連接的詳細資訊，請參閱 [為電子郵件傳遞設定報表伺服器 (SSRS 組態管理員)](http://msdn.microsoft.com/en-us/b838f970-d11a-4239-b164-8d11f4581d83)。|  
|123|警告|記錄|報表伺服器<br /><br /> 報表管理員|報表伺服器寫入追蹤記錄失敗。 如需追蹤記錄的詳細資訊，請參閱 [報表伺服器服務追蹤記錄](../../reporting-services/report-server/report-server-service-trace-log.md)。|  
|124|資訊|啟用|報表伺服器|「報表伺服器」服務已經初始化。 如需詳細資訊，請參閱[初始化報表伺服器 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)。|  
|125|資訊|啟用|報表伺服器|用來加密資料的金鑰已經成功擷取。 如需金鑰的詳細資訊，請參閱[設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
|126|資訊|啟用|報表伺服器|用來加密資料的金鑰已經成功套用。 如需金鑰的詳細資訊，請參閱[設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
|127|資訊|啟用|報表伺服器|加密內容已經成功從報表伺服器資料庫移除。 如需刪除無法復原之加密資料的詳細資訊，請參閱[設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)。|  
|128|錯誤|啟用|報表伺服器|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不同版本的元件無法一起使用。|  
|129|錯誤|管理|報表伺服器<br /><br /> 排程與傳遞處理器|加密的組態檔設定無法解密。|  
|130|錯誤|管理|報表伺服器<br /><br /> 排程與傳遞處理器|*\<來源 >*找不到組態檔。 報表伺服器需要組態檔。|  
|131|錯誤|Security|報表伺服器<br /><br /> 排程與傳遞處理器|加密的使用者資料值無法解密。|  
|132|錯誤|Security|報表伺服器|加密使用者資料期間發生失敗。 無法儲存值。|  
|133|錯誤|管理|報表伺服器<br /><br /> 報表管理員<br /><br /> 排程與傳遞處理器|組態檔上傳失敗。 如果 XML 無效就可能會發生此錯誤。|  
|134|錯誤|管理|報表伺服器|報表伺服器加密組態檔設定的值失敗。|  
  
## <a name="see-also"></a>請參閱＜  
 [監視 Reporting Services 訂閱](../../reporting-services/subscriptions/monitor-reporting-services-subscriptions.md)   
 [Reporting Services 記錄檔和來源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

