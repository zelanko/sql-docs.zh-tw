---
title: SQL Server Native Client 的系統需求 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [SQL Server Native Client]
- data access [SQL Server Native Client], system requirements
- SQL Server Native Client, system requirements
- SQLNCLI, system requirements
ms.assetid: 1c8e2f8a-a440-44da-8e3a-af632d34c52c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 147679798418dceb7de94ec8dbcc8489ad6fda3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026673"
---
# <a name="system-requirements-for-sql-server-native-client"></a>SQL Server Native Client 的系統需求
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  若要使用 MARS 這類 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料存取功能，您必須已經安裝下列軟體：  
  
-   在用戶端上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。  
  
-   在伺服器上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 需要 Windows Installer 3.0。 Windows Installer 3.0 已安裝在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 作業系統上。 如需任何其他平台，則您需要明確地加以安裝。 如需詳細資訊，請參閱 < [Windows Installer 3.0 可轉散發套件](https://go.microsoft.com/fwlink/?LinkId=46459)。  
  
> [!NOTE]  
>  在安裝此軟體之前，請確定已使用管理員權限登入。  
  
## <a name="operating-system-requirements"></a>作業系統需求  
 如需支援的作業系統[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端，請參閱[的 SQL Server Native Client 的支援原則](../../relational-databases/native-client/applications/support-policies-for-sql-server-native-client.md)。  
  
## <a name="sql-server-requirements"></a>SQL Server 需求  
 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料，您必須已經安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支援來自所有 MDAC 版本、Windows Data Access Components 及所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 版本的連接。 當舊版的用戶端版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接時，用戶端不知道的伺服器資料類型會對應至與用戶端版本相容的類型。 如需詳細資訊，請參閱本主題稍後的「用戶端版本的資料類型相容性」。  
  
## <a name="cross-language-requirements"></a>跨語言需求  
 所有受支援作業系統的當地語系化版本都支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的英文版。 與當地語系化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 版本相同語言的當地語系化作業系統都支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的當地語系化版本。 只要有安裝相符的語言設定，受支援作業系統的英文版就會支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的當地語系化版本。  
  
 在升級方面：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的英文版可以升級到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的任何當地語系化版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的當地語系化版本可以升級到相同語言之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的當地語系化版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的當地語系化版本可以升級到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的英文版。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的當地語系化版本無法升級到不同語言之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的當地語系化版本。  
  
## <a name="data-type-compatibility-for-client-versions"></a>用戶端版本的資料類型相容性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 會將新的資料類型對應到與下層用戶端相容的舊版資料類型，如下表所示。  
  
 OLE DB 和 ADO 的應用程式可以使用**DataTypeCompatibility**連接字串關鍵字搭配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端運作較舊的資料類型。 當 **DataTypeCompatibility=80** 時，OLE DB 用戶端會使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 表格式資料流 (TDS) 版本而非 TDS 版本進行連線。 這表示對 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和較新的資料類型來說，下層的轉換將由伺服器執行，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。 也表示連接可以使用的功能將限於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 功能集。 在 API 呼叫時，即可偵測出使用新資料類型或功能的嘗試，且錯誤會傳回給進行呼叫的應用程式，而不會嘗試將無效的要求傳遞給伺服器。  
  
 沒有任何**DataTypeCompatibility** ODBC 的控制項。  
  
 IDBInfo::GetKeywords 一律會傳回的關鍵字清單，對應到連接的伺服器版本，而且不會受到**DataTypeCompatibility**。  
  
|資料類型|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Windows Data Access Components、MDAC 和<br /><br /> DataTypeCompatibility=80 的 SQL Server Native Client OLE DB 應用程式|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8Kb)|udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|Image|  
|varchar(max)|varchar|varchar|Text|  
|nvarchar(max)|NVARCHAR|NVARCHAR|Ntext|  
|Xml|Xml|Xml|Ntext|  
|CLR UDT (> 8 Kb)|udt|varbinary|Image|  
|日期|日期|varchar|Varchar|  
|datetime2|datetime2|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|Varchar|  
|time|time|varchar|Varchar|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 程式設計](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [安裝 SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
