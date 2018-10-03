---
title: 使用加密而不需驗證 |Microsoft Docs
description: 使用加密而不需驗證
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 41aa355de39aabc266e798b6870a8f43ceca4110
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47814720"
---
# <a name="using-encryption-without-validation"></a>使用加密而不需驗證
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一律會加密與登入有關的網路封包。 如果當它啟動時未在伺服器上提供任何憑證，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會產生自行簽署的憑證，該憑證會用來加密登入封包。  

自我簽署的憑證不保證安全性。 加密信號交換以 NT LAN Manager (NTLM)。 強烈建議您佈建 SQL Server 上的安全連線可驗證的憑證。 傳輸安全性層 (TLS) 可安全只使用憑證驗證。

應用程式也可要求加密所有網路流量，其方式是使用連接字串關鍵字或連接屬性。 當搭配 **IDbInitialize::Initialize** 使用提供者字串時，關鍵字為 "Encrypt" (適用於 OLE DB)；當搭配 **IDataInitialize** 使用初始化字串時，關鍵字為 "Use Encryption for Data" (適用於 ADO 和 OLE DB)。 這也可以藉由設定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 Configuration Manager**強制通訊協定加密**選項，然後藉由設定 用戶端要求加密的連線。 根據預設，加密連接的所有網路流量會要求在伺服器上提供憑證。 藉由設定您的用戶端信任的伺服器上的憑證，您可能會很容易遭受攔截攻擊程式碼。 如果您部署在伺服器上可驗證的憑證，請確定您將信任的憑證相關的用戶端設定變更為 FALSE。

如需連接字串關鍵字的資訊，請參閱[搭配 OLE DB Driver for SQL Server 使用連接字串關鍵字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md )。  
  
 若要在伺服器上尚未佈建憑證時使用加密，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員可用來設定 [強制通訊協定加密] 和 [信任伺服器憑證] 選項。 在此情況下，如果伺服器上未提供任何可驗證的憑證，加密將會使用自行簽署的伺服器憑證，而不需驗證。  
  
 應用程式可能也會使用 "TrustServerCertificate" 關鍵字或它的關聯連接屬性，以便保證加密將會發生。 應用程式設定絕對不會減少 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用戶端組態管理員所設定的安全性層級，但是可能會強化它。 例如，如果未針對用戶端設定 [強制通訊協定加密]，應用程式可能會自行要求加密。 如果要保證加密，甚至是在尚未提供伺服器憑證時，應用程式可能會要求加密和 "TrustServerCertificate"。 但是，如果用戶端組態中未啟用 "TrustServerCertificate"，仍然需要提供的伺服器憑證。 下表描述所有的案例：  
  
|強制通訊協定加密用戶端設定|信任伺服器憑證用戶端設定|資料的連接字串/連接屬性加密/使用加密|連接字串/連接屬性信任伺服器憑證|結果|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|否|不適用|無 (預設值)|忽略|不發生任何加密。|  
|否|不適用|是|無 (預設值)|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|否|不適用|是|是|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
|是|否|忽略|忽略|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|是|是|無 (預設值)|忽略|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
|是|是|是|無 (預設值)|只有當有可驗證的伺服器憑證時才會發生加密，否則連接嘗試會失敗。|  
|是|是|是|是|加密一定會發生，但是可能會使用自行簽署的伺服器憑證。|  
||||||

> [!CAUTION]
> 上表只會提供不同設定下的系統行為的指南。 安全的連線，請確定用戶端和伺服器都需要加密。 也請確定伺服器具有可驗證的憑證，以及**TrustServerCertificate**用戶端上的設定設為 FALSE。

## <a name="ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 
 OLE DB Driver for SQL Server 可透過 SSPROP_INIT_TRUST_SERVER_CERTIFICATE 資料來源初始化屬性的加入來支援不需驗證的加密，該屬性是在 DBPROPSET_SQLSERVERDBINIT 屬性集中實作。 此外，也已經加入新的連接字串關鍵字 "TrustServerCertificate"。 它可接受 yes 或 no 值；預設值是 no。 當使用服務元件時，它可接受 true 或 false 值；false 是預設值。  
  
 如需有關對 DBPROPSET_SQLSERVERDBINIT 屬性集所做的增強功能的詳細資訊，請參閱 <<c0> [ 初始化和授權屬性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)。  

  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
