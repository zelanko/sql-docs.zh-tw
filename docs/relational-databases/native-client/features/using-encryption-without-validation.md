---
title: 使用加密而不需驗證 | Microsoft Docs
description: 瞭解 SQL Server Native Client OLE DB 提供者和 ODBC 驅動程式如何支援不進行驗證的加密，以及使用時機的建議。
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 09cccfb889bb2eae2b80c2c466eaed1a96520be8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461999"
---
# <a name="using-encryption-without-validation-in-sql-server-native-client"></a>在 SQL Server Native Client 中使用加密而不需驗證
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一律會加密與登入有關的網路封包。 如果當它啟動時未在伺服器上提供任何憑證，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會產生自行簽署的憑證，該憑證會用來加密登入封包。  

自我簽署憑證不保證安全性。 加密的交握會以 NT LAN Manager (NTLM) 為基礎。 強烈建議您在 SQL Server 上佈建可驗證的憑證，以提供安全連線能力。 傳輸層安全性 (TLS) 只能透過憑證驗證來保護。

應用程式也可要求加密所有網路流量，其方式是使用連接字串關鍵字或連接屬性。 當您搭配 **IDbInitialize：： Initialize** 使用提供者字串時，關鍵字為 "Encrypt" for ODBC 和 OLE DB，或在搭配 **IDataInitialize** 使用初始化字串時，將 "Use Encryption FOR Data" 用於 ADO 和 OLE DB。 這也可以透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager 使用 [強制通訊協定加密] 選項來設定，以及藉由將用戶端設定為要求加密連線來設定。 根據預設，加密連接的所有網路流量會要求在伺服器上提供憑證。 藉由將您的用戶端設定為信任伺服器上的憑證，您可能很容易受到中間人攻擊。 如果您在伺服器上部署可驗證的憑證，請務必將有關信任憑證的用戶端設定變更為 FALSE。

如需連接字串關鍵字的詳細資訊，請參閱搭配 [SQL Server Native Client 使用連接字串關鍵字](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 若要在伺服器上尚未佈建憑證時使用加密，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員可用來設定 [強制通訊協定加密] 和 [信任伺服器憑證] 選項。 在此情況下，如果伺服器上未提供任何可驗證的憑證，加密將會使用自行簽署的伺服器憑證，而不需驗證。  
  
 應用程式可能也會使用 "TrustServerCertificate" 關鍵字或它的關聯連接屬性，以便保證加密將會發生。 應用程式設定絕對不會減少 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端組態管理員所設定的安全性層級，但是可能會強化它。 例如，如果未針對用戶端設定 [強制通訊協定加密]，應用程式可能會自行要求加密。 如果要保證加密，甚至是在尚未提供伺服器憑證時，應用程式可能會要求加密和 "TrustServerCertificate"。 但是，如果用戶端組態中未啟用 "TrustServerCertificate"，仍然需要提供的伺服器憑證。 下表描述所有的案例：  
  
|強制通訊協定加密用戶端設定|信任伺服器憑證用戶端設定|資料的連接字串/連接屬性加密/使用加密|連接字串/連接屬性信任伺服器憑證|結果|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|否|N/A|無 (預設值)|忽略|不發生任何加密。|  
|否|N/A|是|無 (預設值)|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|否|N/A|是|是|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
|是|否|忽略|忽略|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|是|是|無 (預設值)|忽略|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
|是|是|是|無 (預設值)|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|是|是|是|是|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
||||||

> [!CAUTION]
> 上表僅提供有關在不同設定下系統行為的指南。 針對安全連線能力，確定用戶端與伺服器都需要加密。 此外，也要確定伺服器具有可驗證的憑證，且用戶端上的 **TrustServerCertificate** 設定會設定為 FALSE。

## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者透過新增 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 資料來源初始化屬性（在 DBPROPSET_SQLSERVERDBINIT 屬性集內執行），支援加密而不需驗證。 此外，也已經加入新的連接字串關鍵字 "TrustServerCertificate"。 它可接受 yes 或 no 值；預設值是 no。 當使用服務元件時，它可接受 true 或 false 值；false 是預設值。  
  
 如需對 DBPROPSET_SQLSERVERDBINIT 屬性集所做之增強功能的詳細資訊，請參閱[初始化和授權屬性](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驅動程式  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native CLIENT ODBC 驅動程式支援透過[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)和[SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)函式的新增功能進行加密，而不需要驗證。 已經加入 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE 來接受 SQL_TRUST_SERVER_CERTIFICATE_YES 或 SQL_TRUST_SERVER_CERTIFICATE_NO，預設值為 SQL_TRUST_SERVER_CERTIFICATE_NO。 此外，也已經加入新的連接字串關鍵字 "TrustServerCertificate"。 它可接受 yes 或 no 值；預設值是 "no"。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
