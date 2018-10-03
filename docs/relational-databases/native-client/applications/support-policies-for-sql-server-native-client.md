---
title: SQL Server Native Client 的支援原則 |Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 09c80cf4-23e6-4027-a24f-cdb9c87af811
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2e6a0a8f0a7a5f39e024aeb6e04b09d830ff100d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621886"
---
# <a name="support-policies-for-sql-server-native-client"></a>SQL Server Native Client 的支援原則
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主題討論如何搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用各種不同的資料存取元件。  
  
## <a name="server-support"></a>伺服器支援  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 支援與 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]、[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]的連接。  
  
## <a name="supported-operating-system-versions"></a>支援的作業系統版本  
 下表將列出哪些作業系統支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
|SQL Server Native Client 版本|支援的作業系統|  
|--------------------------------------|---------------------------------|  
|SQL Server Native Client (SQL Server 2005)|Microsoft Windows 2000 Service Pack 4 或更新版本<br /><br /> Microsoft Windows Server 2003 或更新版本<br /><br /> Microsoft Windows XP Service Pack 1 或更新版本<br /><br /> Microsoft Windows Vista (需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Service Pack 2 或更新版本)<br /><br /> Microsoft Windows Server 2008 R2 (需要[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Service Pack 2 或更新版本)|  
|SQL Server Native Client 10.0 ([!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)])|Microsoft Windows Server 2003 Service Pack 2 或更新版本<br /><br /> Microsoft Windows XP Service Pack 2 或更新版本<br /><br /> Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2|  
|SQL Server Native Client 10.5 ([!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)])|Microsoft Windows Server 2003 Service Pack 2 或更新版本<br /><br /> Microsoft Windows XP Service Pack 2 或更新版本<br /><br /> Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2<br /><br /> Microsoft Windows 7|  
|SQL Server Native Client 11.0 ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])|Microsoft Windows Vista<br /><br /> Microsoft Windows Server 2008 R2<br /><br /> Microsoft Windows 7<br /><br /> Microsoft Windows 8<br /><br /> Microsoft Windows Server 2012|  
  
## <a name="ado-support-policies"></a>ADO 支援原則  
 如果 ADO 應用程式不需要 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的任何功能，就可以使用 Windows 隨附的 SQLOLEDB OLE DB 提供者。  
  
 ADO 應用程式可以使用新版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端包含在[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 ADO 應用程式也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 (隨附於 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)])，但是如果它們這樣做，就必須在連接字串中指定 `DataTypeCompatibility=80`。 當連接字串中存在 `DataTypeCompatibility=80` 時，只能使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的功能。  
  
## <a name="bcp-support-policies"></a>BCP 支援原則  
 從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始，bcp.exe 便支援不超過提供 bcp.exe 之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本前三個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本的資料檔案。  
  
## <a name="odbc-support-policies"></a>ODBC 支援原則  
 應用程式應該使用 Windows 作業系統隨附的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC 驅動程式。 如果應用程式經認證可搭配特定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 版本使用，您就可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式。  
  
## <a name="ole-db-support-policies"></a>OLE DB 支援原則  
 應用程式應該使用 Windows 作業系統隨附的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 提供者。 如果應用程式經認證可搭配特定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 版本使用，您就可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者。  
  
 如果未經認證可搭配 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 使用的 OLE DB 應用程式在其連接字串中指定了 `DataTypeCompatibility=80`，它們就可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。  
  
 如果使用 OLE DB 服務元件的 OLE DB 應用程式在其連接字串中指定了 `DataTypeCompatibility=80`，它們就只能使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 不過之後, 加入任何功能[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]會在此情況下提供。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建置應用程式](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
