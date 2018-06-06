---
title: 保護 SQL Server 的安全 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- database objects [SQL Server], security
- SQL Server, security
- operating systems [SQL Server], security
- security [SQL Server], planning
- applications [SQL Server], security
ms.assetid: 4d93489e-e9bb-45b3-8354-21f58209965d
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 404258cb75327f04cbda7df0831ead8130ff8364
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="securing-sql-server"></a>保護 SQL Server 的安全
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  維護 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安全可視為一系列的步驟，與下列四個方面有關：平台、驗證、物件 (包括資料) 和存取系統的應用程式。 下列主題將會引導您逐步建立及實施有效的安全性計畫。  
  
 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Server [網站上找到有關](http://go.microsoft.com/fwlink/?LinkID=31629) 安全性的詳細資訊。 這包括最佳作法指南和安全性檢查清單。 該網站也提供了最新的 Service Pack 資訊和下載檔。  
  
## <a name="platform-and-network-security"></a>平台與網路安全性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的平台包括了將用戶端連接到資料庫伺服器的實體硬體和網路系統，以及用於處理資料庫要求的二進位檔案。  
  
### <a name="physical-security"></a>實體安全性  
 實體安全性的最佳作法應嚴格限制對於實體伺服器和硬體元件的存取。 例如，請將資料庫伺服器硬體和網路裝置放在上鎖限制存取的機房內。 此外，備份媒體應儲存在安全的異地位置以限制存取。  
  
 實施實體網路安全性的第一步，是禁止未經授權的使用者接近網路。 下表包含網路安全性資訊的進一步相關資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] 以及從網路存取其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|《 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 線上叢書》中的＜設定與保護伺服器環境安全＞|  
  
### <a name="operating-system-security"></a>作業系統安全性  
 作業系統的 Service Pack 和升級包含重要的安全性增強功能。 任何更新和升級在經過資料庫應用程式的測試後，請立即套用至作業系統。  
  
 防火牆也提供了有效實施安全性的方法。 在邏輯上，防火牆具有隔離與限制網路流量的功能，可供您的組織進行設定以強制實施資料安全性原則。 如果您使用防火牆，可對有安全顧慮的重點區域提供阻卻作用，以提高作業系統層級安全性。 下表包含有關如何搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用防火牆的詳細資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|設定要搭配使用的防火牆 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[設定用於 Database Engine 存取的 Windows 防火牆](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|  
|設定要搭配使用的防火牆 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[Integration Services 服務 &#40;SSIS 服務&#41;](../../integration-services/service/integration-services-service-ssis-service.md)|  
|設定要搭配使用的防火牆 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|  
|開啟防火牆的特定通訊埠以啟用存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|使用通道繫結與服務繫結，設定驗證擴充保護的支援|[使用擴充保護連接至 Database Engine](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)|  
  
 介面區縮小是一種停止或停用未使用元件的安全性措施。 介面區縮小可透過提供較少的系統潛在攻擊途徑，以協助提高安全性。 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的介面區設限，重點事項包括僅授與服務和使用者適當權限，以賦予「最少權限」執行必要的服務。 下表包含服務及系統存取的詳細資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|所需的服務 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[設定 Windows 服務帳戶與權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)|  
  
 如果您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統使用 Internet Information Services (IIS)，則需要設定其他步驟以保護平台介面的安全。 下表包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Internet Information Services 的相關資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|IIS 安全性 [!INCLUDE[ssEW](../../includes/ssew-md.md)]|《 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 線上叢書》中的＜IIS 安全性＞|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 驗證|[Reporting Services 中的驗證](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] 與 IIS 存取|《 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 線上叢書》中的＜Internet Information Services 安全性流程圖＞|  
  
### <a name="sql-server-operating-system-files-security"></a>SQL Server 作業系統檔案安全性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用作業系統檔案執行作業及儲存資料。 檔案安全性的最佳作法要求針對這些檔案設定存取限制。 下表包含這些檔案的詳細資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式檔案|[SQL Server 的預設和具名執行個體的檔案位置](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Pack 和升級提供增強的安全性。 如需得知 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是否已有最新的 Service Pack 可供使用，請瀏覽 [SQL Server](http://go.microsoft.com/fwlink/?LinkID=31629) 網站。  
  
 您可以利用下列指令碼判斷系統上安裝的 Service Pack 版本。  
  
```  
SELECT CONVERT(char(20), SERVERPROPERTY('productlevel'));  
GO  
```  
  
## <a name="principals-and-database-object-security"></a>主體與資料庫物件安全性  
 主體是指已獲授權存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的個人、群組和處理序。 「安全性實體」則是指伺服器、資料庫及資料庫所包含的物件。 這些實體均可各自設定一組權限，以減少 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 介面區。 下表包含主體和安全性實體的相關資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|伺服器與資料庫使用者、角色和處理序|[主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)|  
|伺服器與資料庫物件安全性|[安全性實體](../../relational-databases/security/securables.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性階層架構|[權限階層 &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)|  
  
### <a name="encryption-and-certificates"></a>加密和憑證  
 加密並不能解決存取控制問題。 但是，若發生存取控制失靈的罕見情形，加密則可限縮資料遺失的風險以增強安全性。 例如，只要資料已加密，即使資料庫主機電腦設定不當而遭惡意使用者取得敏感性資料 (如信用卡號)，失竊的資訊就可能毫無用處。 下表包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中加密的詳細資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|加密階層 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)|  
|實作安全連接|[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)|  
|加密函數|[密碼編譯函數 &#40;Transact-SQL&#41;](../../t-sql/functions/cryptographic-functions-transact-sql.md)|  
  
 憑證是兩部伺服器之間共用的軟體「金鑰」，可透過強化驗證的方式提供安全通訊。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立與使用憑證，進而增強物件及連接安全性。 下表包含有關如何搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用憑證的詳細資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|建立使用的憑證 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)|  
|搭配資料庫鏡像使用憑證|[使用資料庫鏡像端點憑證 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
  
## <a name="application-security"></a>應用程式安全性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性最佳做法包括撰寫安全的用戶端應用程式。  
  
 如需如何在網路層維護用戶端應用程式安全的詳細資訊，請參閱 [用戶端網路組態](../../database-engine/configure-windows/client-network-configuration.md)。  
  
## <a name="sql-server-security-tools-utilities-views-and-functions"></a>SQL Server 安全性工具、公用程式、檢視和函數  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供可用於設定與管理安全性的工具、公用程式、檢視和函數。  
  
### <a name="sql-server-security-tools-and-utilities"></a>SQL Server 安全性工具和公用程式  
 下表包含可用於設定及管理安全性之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工具和公用程式的相關資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|連接、設定與控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[使用 SQL Server Management Studio](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)|  
|從命令提示字元連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並執行查詢|[sqlcmd 公用程式](../../tools/sqlcmd-utility.md)|  
|網路組態和控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)|  
|使用以原則為基礎的管理來啟用及停用功能|[使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)|  
|管理報表伺服器的對稱金鑰|[rskeymgmt 公用程式 &#40;SSRS&#41;](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)|  
  
### <a name="sql-server-security-catalog-views-and-functions"></a>SQL Server 安全性目錄檢視和函數  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在已針對效能與實用性最佳化的數種檢視和函數中公開安全性資訊。 下表包含安全性檢視和函數的相關資訊。  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性目錄檢視，傳回資料庫層級與伺服器層級的權限、主體、角色等等的相關資訊。 此外，另有若干目錄檢視提供了加密金鑰、憑證與認證的相關資訊。|[安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性函數，可傳回目前使用者、權限和結構描述的相關資訊。|[安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性動態管理檢視。|[安全性相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)|  
  
## <a name="related-content"></a>相關內容  
 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[SQL Server 2012 安全性最佳做法 - 作業和系統管理工作](http://download.microsoft.com/download/8/F/A/8FABACD7-803E-40FC-ADF8-355E7D218F4C/SQL_Server_2012_Security_Best_Practice_Whitepaper_Apr2012.docx)   
[SQL Server 安全性部落格](https://blogs.msdn.microsoft.com/sqlsecurity/)  
[安全性最佳做法和標籤安全性白皮書](https://blogs.msdn.microsoft.com/sqlsecurity/2012/03/06/security-best-practice-and-label-security-whitepapers/)  
[資料列層級安全性](../../relational-databases/security/row-level-security.md)   
[保護 SQL Server 智慧財產權](../../relational-databases/security/protecting-your-sql-server-intellectual-property.md)   
  
