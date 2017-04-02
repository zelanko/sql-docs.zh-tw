---
title: "對封裝使用之檔案的存取權 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SSIS 封裝, 安全性"
  - "封裝 [Integration Services], 安全性"
  - "組態檔 [Integration Services]"
  - "檢查點檔案"
  - "Integration Services 封裝, 安全性"
  - "記錄 [Integration Services], 安全性"
  - "檔案 [Integration Services], 安全性"
  - "SQL Server Integration Services 封裝, 安全性"
ms.assetid: 2e3ddea9-5289-4289-a70e-11c018f34977
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# 對封裝使用之檔案的存取權
  封裝保護等級不會保護儲存於封裝之外的檔案。 這些檔案包括下列各項：  
  
-   組態檔  
  
-   檢查點檔案  
  
-   記錄檔  
  
 您必須分開保護這些檔案，尤其是當檔案中包含機密資訊時。  
  
## 組態檔  
 如果組態中含有機密資訊，例如登入和密碼資訊，則應考慮將組態儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，或使用存取控制清單 (ACL) 來限制對儲存檔案之位置或資料夾的存取權，且只允許特定帳戶擁有其存取權。 通常，您可以將存取權授與您允許執行封裝的帳戶，以及負責管理和疑難排解封裝的帳戶，其工作可能包括檢閱組態、檢查點和記錄檔的內容。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供更安全的儲存體，因為它可以提供伺服器和資料庫層級的保護。 若要將組態儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態類型。 若要儲存至檔案系統，則可以使用 XML 組態類型。  
  
 如需詳細資訊，請參閱[封裝組態](../../integration-services/packages/package-configurations.md)、[建立封裝組態](../../integration-services/packages/create-package-configurations.md)和 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)。  
  
## 檢查點檔案  
 同樣地，如果封裝使用的檢查點檔案包含機密資訊，應使用存取控制清單 (ACL) 來保護儲存檔案之位置或資料夾的安全。 檢查點檔案儲存有關封裝進度和目前變數值的目前狀態資訊。 例如，封裝可能包括含有電話號碼的自訂變數。 如需詳細資訊，請參閱 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)。  
  
## 記錄檔  
 寫入檔案系統的記錄項目也應使用存取控制清單 (ACL) 保護其安全。 記錄項目還可以儲存於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性進行保護。 記錄項目可能包含機密資訊，例如，如果封裝包含建構參考電話號碼之 SQL 陳述式的「執行 SQL」工作，SQL 陳述式的記錄項目便會包含電話號碼。 SQL 陳述式可能還顯示有關資料庫中資料表與資料行名稱的私用資訊。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
  