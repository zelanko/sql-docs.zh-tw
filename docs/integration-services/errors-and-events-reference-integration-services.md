---
title: 錯誤和事件參考 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- events [Integration Services]
- errors [Integration Services]
- Integration Services, errors
ms.assetid: cf4f0f14-8087-42d7-9b67-e4929228abd6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 64e805e5dd9b334afe252e2c1d43685e9c92b95f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "71290615"
---
# <a name="errors-and-events-reference-integration-services"></a>錯誤和事件參考 (Integration Services)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  文件集中的這一節包含一些與 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]相關之錯誤和事件的資訊， 包含錯誤訊息的原因和解決方案資訊。  
  
 如需 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤訊息的詳細資訊，包括大部分 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 錯誤及其描述的清單，請參閱 [Integration Services 錯誤和訊息參考](../integration-services/integration-services-error-and-message-reference.md)。 不過，此清單目前並不包含疑難排解的資訊。  
  
> [!IMPORTANT]  
>  在使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 時所看到的許多錯誤訊息都是來自其他元件。 這可能包括 OLE DB 提供者、其他的資料庫元件 (例如 [!INCLUDE[ssDE](../includes/ssde-md.md)] 和 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ) 或其他的服務或元件 (例如檔案系統、SMTP 伺服器或 Microsoft Message Queueing)。 若要尋找有關這些外部錯誤訊息的資訊，請參閱該元件的特定文件集。  
  
## <a name="error-messages"></a>錯誤訊息  
  
|錯誤的符號名稱|描述|  
|----------------------------|-----------------|  
|DTS_E_CACHELOADEDFROMFILE|指出封裝無法執行，因為某個「快取轉換」轉換正嘗試將資料寫入記憶體中的快取。 不過，快取連線管理員已經將快取檔案載入記憶體中的快取。|  
|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|指出封裝無法執行，因為指定的連接已失敗。|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|指出資料流程元件正在嘗試將 Unicode 字串資料傳遞給另一個預期在對應資料行中收到非 Unicode 字串資料的元件 (或者相反情況)。|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|指出資料流程元件正在嘗試將 Unicode 字串資料傳遞給另一個預期在對應資料行中收到非 Unicode 字串資料的元件 (或者相反情況)。|  
|DTS_E_CANTINSERTCOLUMNTYPE|指出資料行無法加入至資料庫資料表，因為不支援 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 資料行資料類型與資料庫資料行資料類型之間的轉換。|  
|DTS_E_CONNECTIONNOTFOUND|指出封裝無法執行，因為找不到指定的連線管理員。|  
|DTS_E_CONNECTIONREQUIREDFORMETADATA|指出 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師必須連接到資料來源，才能擷取來源或目的地的新增或更新中繼資料，並指出該設計師無法與資料來源連接。|  
|DTS_E_MULTIPLECACHEWRITES|指出封裝無法執行，因為某個「快取轉換」轉換正嘗試將資料寫入記憶體中的快取。 不過，另一個「快取轉換」已經寫入記憶體中的快取。|  
|DTS_E_PRODUCTLEVELTOLOW|指出套件無法執行，因為尚未安裝正確的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 版本。|  
|DTS_E_READNOTFILLEDCACHE|指出「查閱」轉換正嘗試從記憶體中的快取讀取資料，同時「快取轉換」轉換正將資料寫入快取。|  
|DTS_E_UNPROTECTXMLFAILED|指出系統並未將保護的 XML 節點解密。|  
|DTS_E_WRITEWHILECACHEINUSE|指出「快取轉換」轉換正嘗試將資料寫入記憶體中的快取，同時「查閱」轉換正從記憶體中的快取讀取資料。|  
|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|指出資料來源中的資料行中繼資料與連接至資料來源之來源或目的地元件的資料行中繼資料不相符。|  
  
## <a name="events-sqlispackage"></a>事件 (SQLISPackage)  
 如需詳細資訊，請參閱 [Integration Services 封裝所記錄的事件](../integration-services/performance/events-logged-by-an-integration-services-package.md)。  
  
|事件|描述|  
|-----------|-----------------|  
|SQLISPackage_12288|指出封裝已經啟動。|  
|SQLISPackage_12289|指出封裝已順利地完成執行。|  
|SQLISPACKAGE_12291|指出封裝無法完成執行而且已經停止。|  
|SQLISPackage_12546|指出封裝中的工作或其他可執行檔已經完成其工作。|  
|SQLISPackage_12549|指出在封裝中引發了警告訊息。|  
|SQLISPackage_12550|指出在封裝中引發了錯誤訊息。|  
|SQLISPackage_12551|指出封裝沒有完成其工作而且已停止。|  
|SQLISPackage_12557|指出封裝已完成執行。|  
  
## <a name="events-sqlisservice"></a>事件 (SQLISService)  
 如需詳細資訊，請參閱 [Integration Services 服務所記錄的事件](../integration-services/service/events-logged-by-the-integration-services-service.md)。  
  
|事件|描述|  
|-----------|-----------------|  
|SQLISService_256|指出服務即將啟動。|  
|SQLISService_257|指出服務已經啟動。|  
|SQLISService_258|指出服務即將停止。|  
|SQLISService_259|指出服務已經停止。|  
|SQLISService_260|指出服務嘗試啟動，但是無法啟動。|  
|SQLISService_272|指出組態檔不存在指定的位置中。|  
|SQLISService_273|指出組態檔無法讀取或無效。|  
|SQLISService_274|指出包含組態檔位置的登錄項目不存在或是空的。|  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../integration-services/integration-services-error-and-message-reference.md)  
  
  
