---
title: 以程式設計方式變更密碼 |Microsoft 文件
description: 使用 SQL Server 的 OLE DB 驅動程式以程式設計方式變更密碼
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], password expiration
- OLE DB Driver for SQL Server, passwords
- passwords [SQL Server], expiration
- MSOLEDBSQL, password expiration
- expiration [OLE DB Driver for SQL Server]
- passwords [SQL Server], modifying
- expired passwords [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, password expiration
- modifying passwords
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8ac5c5c127b67fb872a6b10ffc7bd32ec7458092
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="changing-passwords-programmatically"></a>以程式設計方式變更密碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前，當使用者密碼到期時，只有系統管理員可以重設密碼。 開頭為[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，OLE DB 驅動程式處理密碼逾期透過 OLE DB 驅動程式，以程式設計方式，以及透過變更的 SQL Server 支援**SQL Server 登入**對話方塊。  
  
> [!NOTE]  
>  如果可能的話，請在執行階段提示使用者輸入其認證，並避免以保存的格式儲存其認證。 如果您必須保存其認證，您應該先加密它們使用[Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)。 如需有關使用的密碼，請參閱[強式密碼](../../../relational-databases/security/strong-passwords.md)。  
  
## <a name="sql-server-login-error-codes"></a>SQL Server 登入錯誤碼  
 當連接因為驗證問題而無法建立時，將會提供下列其中一個 SQL Server 錯誤碼給應用程式來協助診斷和復原。  
  
|SQL Server 錯誤碼|錯誤訊息|  
|---------------------------|-------------------|  
|15113|使用者 '%.*ls' 登入失敗。原因: 密碼驗證失敗。 帳戶已經鎖定。|  
|18463|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 密碼此時不適用。|  
|18464|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 因為密碼太短而不符合原則需求。|  
|18465|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 因為密碼太長而不符合原則需求。|  
|18466|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 因為密碼不夠複雜而不符合原則需求。|  
|18467|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 密碼不符合密碼篩選 DLL 的需求。|  
|18468|使用者 '%.*ls' 的登入失敗。 原因: 密碼變更失敗。 密碼驗證期間發生意外的錯誤。|  
|18487|使用者 '%.*ls' 的登入失敗。 原因: 帳戶的密碼已過期。|  
|18488|使用者 '%.*ls' 的登入失敗。 原因: 必須變更帳戶的密碼。|  
  
## <a name="ole-db-driver-for-sql-server"></a>SQL Server 的 OLE DB 驅動程式  
 SQL Server OLE DB 驅動程式支援密碼逾期，透過使用者介面，以程式設計的方式。  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB 使用者介面密碼逾期  
 SQL Server OLE DB 驅動程式支援透過所做的變更密碼逾期**SQL Server 登入**對話方塊。 如果 DBPROP_INIT_PROMPT 的值設定為 DBPROMPT_NOPROMPT，則密碼到期時，初始連接嘗試將會失敗。  
  
 如果 DBPROP_INIT_PROMPT 已設定為任何其他值，則使用者會看見**SQL Server 登入**對話方塊中，不論是否已過期的密碼。 使用者可以按一下**選項**按鈕，然後檢查**變更密碼**變更密碼。  
  
 如果使用者按一下 [確定]，而且密碼已過期，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]會提示使用者輸入並確認新密碼使用**變更 SQL Server 密碼**對話方塊。  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB 提示行為與鎖定帳戶  
 連接嘗試可能會因為帳戶遭到鎖定而失敗。 如果發生這個情況後的顯示**SQL Server 登入** 對話方塊中，伺服器會顯示錯誤訊息給使用者，並中止連接嘗試。 它也可能會發生下列顯示**變更 SQL Server 密碼**對話方塊如果使用者輸入舊密碼不正確的值。 在此情況下，會顯示相同的錯誤訊息，並中止連接嘗試。  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB 連接共用、密碼逾期與鎖定帳戶  
 當連接在連接共用中仍處於作用中狀態時，帳戶可能會遭到鎖定，或者其密碼可能會過期。 伺服器會在兩種時機下檢查過期的密碼與鎖定的帳戶。 第一個時機是首次建立連接時。 第二個時機則是在連接取自集區而重設連接時。  
  
 當重設嘗試失敗後，連接便會從集區移除並傳回錯誤。  
  
### <a name="ole-db-programmatic-password-expiration"></a>OLE DB 程式設計密碼逾期  
 SQL Server OLE DB 驅動程式支援透過加入已加入 DBPROPSET_SQLSERVERDBINIT 屬性集的 SSPROP_AUTH_OLD_PASSWORD (vt_bstr 類型) 屬性的密碼逾期。  
  
 現有的 "Password" 屬性會參考 DBPROP_AUTH_PASSWORD，並用於儲存新的密碼。  
  
> [!NOTE]  
>  在此連接字串中，"Old Password" 屬性會設定 SSPROP_AUTH_OLD_PASSWORD，這是無法透過提供者字串屬性取得的目前密碼 (可能已過期)。  
  
 提供者不會保存此屬性的值。 設定此屬性時，提供者不會將連接共用用於第一個連接，因為將會產生新的連接。 如果密碼變更成功，則無法重複使用目前的連接，因為該連接仍然包含舊密碼，而這個密碼將在密碼變更後變成無效。 同時，如果登入成功，提供者會清除這個屬性。 後續嘗試擷取舊密碼時，便會傳回 VT_EMPTY。  
  
> [!NOTE]  
>  系統絕不會保存 SSPROP_AUTH_OLD_PASSWORD，因為只有在密碼到期時才會使用它。  
  
 請注意，每當設定 "Old Password" 屬性時，除非同時指定優先順序永遠最高的 Windows 驗證，否則提供者會假設有嘗試變更密碼。  
  
 如果使用 Windows 驗證時，指定舊密碼會導致 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 取決於是否舊密碼指定為 REQUIRED 或 OPTIONAL 分別和 DBPROPSTATUS_ 的狀態值中會傳回 CONFLICTINGBADVALUE *dwStatus*。 偵測到這個時**idbinitialize:: Initialize**呼叫。  
  
 如果嘗試變更密碼時意外失敗，伺服器會傳回錯誤碼 18468。 標準 OLEDB 錯誤會從連線嘗試傳回。  
  
 如需有關 DBPROPSET_SQLSERVERDBINIT 屬性集的詳細資訊，請參閱[初始化和授權屬性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)。  

  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
