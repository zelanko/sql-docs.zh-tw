---
title: 用戶端連接 (OLE DB) 中的服務主體名稱 (Spn) |Microsoft 文件
description: 用戶端連接 (OLE DB) 中的服務主體名稱 (Spn)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 64ef857df576d9c7fae75be3136e0792b60b8e3f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>用戶端連接中的服務主要名稱 (SPN) (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


  本主題描述可在用戶端應用程式內支援服務主要名稱 (SPN) 的 OLE DB 屬性和成員函數。 如需有關 Spn 的用戶端應用程式，請參閱[服務主體名稱&#40;SPN&#41;支援用戶端連接中的](../../oledb/features/service-principal-name-spn-support-in-client-connections.md)。 如需範例，請參閱[整合式 Kerberos 驗證&#40;OLE DB&#41;](../../oledb/ole-db-how-to/integrated-kerberos-authentication-ole-db.md)。  
  
## <a name="provider-initialization-string-keywords"></a>提供者初始化字串關鍵字  
 下列提供者初始化字串關鍵字可支援 OLE DB 應用程式內的 SPN。 下表中，關鍵字欄中的值會用於 idbinitialize:: Initialize 的提供者字串。 使用 ADO 或 idatainitialize:: Getdatasource 連接時，描述資料行的值可用在初始化字串中。  
  
|關鍵字|Description|Value|  
|-------------|-----------------|-----------|  
|ServerSPN|伺服器 SPN|伺服器的 SPN。 預設值是空字串，這會導致 OLE DB 驅動程式使用預設的 SQL Server，提供者產生 SPN。|  
|FailoverPartnerSPN|容錯移轉夥伴 SPN|容錯移轉夥伴的 SPN。 預設值是空字串，這會導致 OLE DB 驅動程式使用預設的 SQL Server，提供者產生 SPN。|  
  
## <a name="data-source-initialization-properties"></a>資料來源初始化屬性  
 中的下列屬性**DBPROPSET_SQLSERVERDBINIT**屬性集讓應用程式指定 Spn。  
  
|名稱|型別|使用方式|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR，讀取/寫入|指定伺服器的 SPN。 預設值是空字串，這會導致 OLE DB 驅動程式使用預設的 SQL Server，提供者產生 SPN。|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR，讀取/寫入|指定容錯移轉夥伴的 SPN。 預設值是空字串，這會導致 OLE DB 驅動程式使用預設的 SQL Server，提供者產生 SPN。|  
  
## <a name="data-source-properties"></a>資料來源屬性  
 中的下列屬性**DBPROPSET_SQLSERVERDATASOURCEINFO**屬性集讓應用程式探索驗證方法。  
  
|名稱|型別|使用方式|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR，唯讀|傳回連接所使用的驗證方法。 傳回至應用程式的值是 Windows 回到 SQL Server 的 OLE DB 驅動程式的值。 以下是可能的值： <br />"NTLM"，當使用 NTLM 驗證開啟連接時所傳回。<br />"Kerberos"，當使用 Kerberos 驗證開啟連接時所傳回。<br /><br /> 如果連接已經開啟，而且無法判定驗證方法，就會傳回 VT_EMPTY。<br /><br /> 只有當已經初始化資料來源時，才可讀取這個屬性。 如果您嘗試在初始化資料來源以前讀取屬性，IDBProperties::GetProperies 會適當地傳回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，而且將在 DBPROPSET_PROPERTIESINERROR 中設定 DBPROPSTATUS_NOTSUPPORTED這個屬性。 這個行為會根據 OLE DB 核心規格。|  
|SSPROP_MUTUALLYAUTHENICATED|VT_BOOL，唯讀|如果連接中的伺服器已互相驗證過，則會傳回 VARIANT_TRUE，否則會傳回 VARIANT_FALSE。<br /><br /> 只有當已經初始化資料來源時，才可讀取這個屬性。 如果沒有嘗試在初始化資料來源以前讀取屬性，IDBProperties::GetProperies 會適當地傳回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，而且將 DBPROPSET_ 中設定 DBPROPSTATUS_NOTSUPPORTED這個屬性的 PROPERTIESINERROR。 這個行為會根據 OLE DB 核心規格。<br /><br /> 如果針對未使用 Windows 驗證的連接來查詢這個屬性，就會傳回 VARIANT_FALSE。|  
  
## <a name="ole-db-api-support-for-spns"></a>OLE DB API 對 SPN 的支援  
 下表描述在用戶端連接中支援 SPN 的 OLE DB 成員函數：  
  
|成員函數|Description|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString*可以包含新的關鍵字**ServerSPN**和**FailoverPartnerSPN**。|  
|IDataInitialize::GetInitializationString|如果 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 有非預設值，它們會包含在初始化字串透過*ppwszInitString*關鍵字的值為**ServerSPN**和**FailoverPartnerSPN**。 否則，這些關鍵字將不會包含在初始化字串中。|  
|IDBInitialize::Initialize|如果在資料來源初始化屬性內設定 DBPROP_INIT_PROMPT 來啟用提示，將會顯示 [OLE DB 登入] 對話方塊。 如此可允許同時針對主體伺服器和它的容錯移轉夥伴來輸入 SPN。<br /><br /> 提供者字串中 DPPROP_INIT_PROVIDERSTRING，如果有設定，將會辨識新的關鍵字**ServerSPN**和**FailoverPartnerSPN**並使用其值，如果有的話，以初始化 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN。<br /><br /> Idbproperties:: Setproperties 可以 idbinitialize:: Initialize 呼叫之前設定 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN 屬性被呼叫。 這是使用提供者字串的替代方式。<br /><br /> 如果在一個以上的地方設定屬性，以程式設計方式設定的值會優先於提供者字串中設定的值。 在初始化字串中設定的值會優先於登入對話方塊內設定的值。<br /><br /> 如果相同的關鍵字在提供者字串內出現一次以上，第一次出現的值會優先於其他的值。|  
|IDBProperties::GetProperties|IDBProperties::GetProperties 可以呼叫以取得新資料來源初始化屬性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 以及新的資料來源屬性 SSPROP_AUTHENTICATIONMETHOD 和 SSPROP_ 的值MUTUALLYAUTHENTICATED。|  
|IDBProperties::GetPropertyInfo|Idbproperties:: Getpropertyinfo 將包含新資料來源初始化屬性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 或是新的資料來源屬性 SSPROP_AUTHENTICATION_METHOD 和 SSPROP_MUTUALLYAUTHENTICATED。|  
|IDBProperties::SetProperties|Idbproperties:: Setproperties 可以呼叫以初始化屬性 SSPROP_INITSERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 設定新的資料來源的值。<br /><br /> 這些屬性可以在任何時間設定，但是如果資料來源已經開啟，將會傳回下列錯誤：DB_E_ERRORSOCCURRED --「多重步驟的 OLE DB 作業已產生錯誤。 請檢查每個 OLE DB 狀態值 (如果有的話)。 未完成任何工作」。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
