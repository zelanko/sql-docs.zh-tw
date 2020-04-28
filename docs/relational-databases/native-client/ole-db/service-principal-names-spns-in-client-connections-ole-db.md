---
title: OLE DB 服務主體名稱連接
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e212010e-a5b6-4ad1-a3c0-575327d3ffd3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: de214361ce06c6f0ff103c4e591ff4e5e53d887c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295624"
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>用戶端連接中的服務主要名稱 (SPN) (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題描述可在用戶端應用程式內支援服務主要名稱 (SPN) 的 OLE DB 屬性和成員函數。 如需用戶端應用程式中 SPN 的詳細資訊，請參閱[用戶端連接中的服務主體名稱 &#40;SPN&#41; 支援](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)。 如需範例，請參閱[整合式 Kerberos 驗證 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/integrated-kerberos-authentication-ole-db.md)。  
  
## <a name="provider-initialization-string-keywords"></a>提供者初始化字串關鍵字  
 下列提供者初始化字串關鍵字可支援 OLE DB 應用程式內的 SPN。 在下表中，關鍵字欄中的值會用於 IDBInitialize::Initialize 的提供者字串。 當使用 ADO 或 IDataInitialize::GetDataSource 連接時，描述欄中的值會在初始化字串中使用。  
  
|關鍵字|描述|值|  
|-------------|-----------------|-----------|  
|ServerSPN|伺服器 SPN|伺服器的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
|FailoverPartnerSPN|容錯移轉夥伴 SPN|容錯移轉夥伴的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
  
## <a name="data-source-initialization-properties"></a>資料來源初始化屬性  
 **DBPROPSET_SQLSERVERDBINIT** 屬性集中的以下屬性可讓應用程式指定 SPN。  
  
|名稱|類型|使用量|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR，讀取/寫入|指定伺服器的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR，讀取/寫入|指定容錯移轉夥伴的 SPN。 預設值為空字串，它可讓 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用提供者產生的預設 SPN。|  
  
## <a name="data-source-properties"></a>資料來源屬性  
 **DBPROPSET_SQLSERVERDATASOURCEINFO** 屬性集中的以下屬性可讓應用程式探索驗證方法。  
  
|名稱|類型|使用量|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR，唯讀|傳回連接所使用的驗證方法。 傳給應用程式的值就是 Windows 傳給 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 的值。 以下是可能的值： <br />"NTLM"，當使用 NTLM 驗證開啟連接時所傳回。<br />"Kerberos"，當使用 Kerberos 驗證開啟連接時所傳回。<br /><br /> 如果連接已經開啟，而且無法判定驗證方法，就會傳回 VT_EMPTY。<br /><br /> 只有當已經初始化資料來源時，才可讀取這個屬性。 如果您嘗試在已初始化資料來源之前讀取這個屬性，IDataInitialize::GetDataSource 將會適當地傳回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，而且將會針對這個屬性在 DBPROPSET_PROPERTIESINERROR 中設定 DBPROPSTATUS_NOTSUPPORTED。 這個行為會根據 OLE DB 核心規格。|  
|SSPROP_MUTUALLYAUTHENICATED|VT_BOOL，唯讀|如果連接中的伺服器已互相驗證過，則會傳回 VARIANT_TRUE，否則會傳回 VARIANT_FALSE。<br /><br /> 只有當已經初始化資料來源時，才可讀取這個屬性。 如果嘗試在已初始化資料來源之前讀取這個屬性，IDataInitialize::GetDataSource 將會適當地傳回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED，而且將會針對這個屬性在 DBPROPSET_PROPERTIESINERROR 中設定 DBPROPSTATUS_NOTSUPPORTED。 這個行為會根據 OLE DB 核心規格。<br /><br /> 如果針對未使用 Windows 驗證的連接來查詢這個屬性，就會傳回 VARIANT_FALSE。|  
  
## <a name="ole-db-api-support-for-spns"></a>OLE DB API 對 SPN 的支援  
 下表描述在用戶端連接中支援 SPN 的 OLE DB 成員函數：  
  
|成員函數|描述|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString* 可以包含新的關鍵字 **ServerSPN** 和 **FailoverPartnerSPN**。|  
|IDataInitialize::GetInitializationString|如果 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 有非預設值，將會透過 *ppwszInitString* 將它們當做 **ServerSPN** 和 **FailoverPartnerSPN** 的關鍵字值包含在初始化字串中。 否則，這些關鍵字將不會包含在初始化字串中。|  
|IDBInitialize::Initialize|如果在資料來源初始化屬性內設定 DBPROP_INIT_PROMPT 來啟用提示，將會顯示 [OLE DB 登入] 對話方塊。 如此可允許同時針對主體伺服器和它的容錯移轉夥伴來輸入 SPN。<br /><br /> DPPROP_INIT_PROVIDERSTRING 中的提供者字串 (如果有設定的話) 將會辨識新的關鍵字 **ServerSPN** 和 **FailoverPartnerSPN**，並使用它們的值 (如果有的話) 來初始化 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN。<br /><br /> 呼叫 IDBInitialize::Initialize 之前，可以呼叫 IDBProperties::SetProperties 來設定 SSPROP_INIT_SERVER_SPN 和 SSPROP_INIT_FAILOVER_PARTNER_SPN 屬性。 這是使用提供者字串的替代方式。<br /><br /> 如果在一個以上的地方設定屬性，以程式設計方式設定的值會優先於提供者字串中設定的值。 在初始化字串中設定的值會優先於登入對話方塊內設定的值。<br /><br /> 如果相同的關鍵字在提供者字串內出現一次以上，第一次出現的值會優先於其他的值。|  
|IDBProperties::GetProperties|可以呼叫 IDBProperties::GetProperties 來取得新資料來源初始化屬性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 以及新資料來源屬性 SSPROP_AUTHENTICATIONMETHOD 和 SSPROP_MUTUALLYAUTHENTICATED 的值。|  
|IDBProperties::GetPropertyInfo|IdbProperties::GetPropertyInfo 將會包含新的資料來源初始化屬性 SSPROP_INIT_SERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 或是新的資料來源屬性 SSPROP_AUTHENTICATION_METHOD 和 SSPROP_MUTUALLYAUTHENTICATED。|  
|IDBProperties::SetProperties|可以呼叫 IDBProperties::SetProperties 來設定新資料來源初始化屬性 SSPROP_INITSERVERSPN 和 SSPROP_INIT_FAILOVERPARTNERSPN 的值。<br /><br /> 這些屬性可以在任何時間設定，但是如果資料來源已經開啟，將會傳回下列錯誤：DB_E_ERRORSOCCURRED --「多重步驟的 OLE DB 作業已產生錯誤。 請檢查每個 OLE DB 狀態值 (如果有的話)。 未完成任何工作」。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
