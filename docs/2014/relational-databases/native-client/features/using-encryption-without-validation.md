---
title: 使用加密而不需驗證 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: eda7a4e7ac9d6558301affc7d2b027c55bc1f7e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135792"
---
# <a name="using-encryption-without-validation"></a>使用加密而不需驗證
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一律會加密與登入有關的網路封包。 如果當它啟動時未在伺服器上提供任何憑證，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會產生自行簽署的憑證，該憑證會用來加密登入封包。  
  
 應用程式也可要求加密所有網路流量，其方式是使用連接字串關鍵字或連接屬性。 關鍵字使用的提供者字串時，即"Encrypt"適用於 ODBC 和 OLE DB **idbinitialize:: Initialize**，或"Use Encryption for Data"ADO 和 OLE DB 時使用與初始字串**IDataInitialize**. 這可能會設定由[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager 使用**強制通訊協定加密**選項。 根據預設，加密連接的所有網路流量會要求在伺服器上提供憑證。  
  
 如需連接字串關鍵字的詳細資訊，請參閱[Using Connection String Keywords with SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 若要啟用加密不在伺服器上，提供憑證時所要使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager 可以用來將兩個設定**強制通訊協定加密**和**信任伺服器憑證**選項。 在此情況下，如果伺服器上未提供任何可驗證的憑證，加密將會使用自行簽署的伺服器憑證，而不需驗證。  
  
 應用程式可能也會使用 "TrustServerCertificate" 關鍵字或它的關聯連接屬性，以便保證加密將會發生。 應用程式設定絕對不會減少 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端組態管理員所設定的安全性層級，但是可能會強化它。 例如，如果**強制通訊協定加密**未設定的用戶端應用程式可能會要求本身的加密。 如果要保證加密，甚至是在尚未提供伺服器憑證時，應用程式可能會要求加密和 "TrustServerCertificate"。 但是，如果用戶端組態中未啟用 "TrustServerCertificate"，仍然需要提供的伺服器憑證。 下表描述所有的案例：  
  
|強制通訊協定加密用戶端設定|信任伺服器憑證用戶端設定|資料的連接字串/連接屬性加密/使用加密|連接字串/連接屬性信任伺服器憑證|結果|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|否|不適用|無 (預設值)|忽略|不發生任何加密。|  
|否|不適用|是|無 (預設值)|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|否|不適用|是|是|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
|是|否|忽略|忽略|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|是|是|無 (預設值)|忽略|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
|是|是|是|無 (預設值)|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|是|是|是|是|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援加密，而不需透過實作中使用的 DBPROPSET_SQLSERVERDBINIT 屬性 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 資料來源初始化屬性加入驗證設定。 此外，也已經加入新的連接字串關鍵字 "TrustServerCertificate"。 它可接受 yes 或 no 值；預設值是 no。 當使用服務元件時，它可接受 true 或 false 值；false 是預設值。  
  
 如需有關對 DBPROPSET_SQLSERVERDBINIT 屬性集的增強功能的詳細資訊，請參閱[初始化和授權屬性](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驅動程式  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援加密，而不需驗證透過 新增項目[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)和[SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md)函式。 已經加入 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE 來接受 SQL_TRUST_SERVER_CERTIFICATE_YES 或 SQL_TRUST_SERVER_CERTIFICATE_NO，預設值為 SQL_TRUST_SERVER_CERTIFICATE_NO。 此外，也已經加入新的連接字串關鍵字 "TrustServerCertificate"。 它可接受 yes 或 no 值；預設值是 "no"。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  