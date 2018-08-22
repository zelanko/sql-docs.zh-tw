---
title: 安裝 SQL Server Native Client |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4023294d52724e5cd132ab4a47b8b8e7f910e3a
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393616"
---
# <a name="installing-sql-server-native-client"></a>安裝 SQL Server Native Client
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 會在安裝時安裝[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]。 沒有 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client。 如需詳細資訊，請參閱 < [What's New in SQL Server Native Client](../sql-server-native-client.md)。 您也可以從 SQL Server 2012 功能套件網頁取得 sqlncli.msi。 若要下載最新版本的 SQL Server Native Client，請前往[Microsoft® SQL Server® 2012 SP2 功能套件](http://www.microsoft.com/en-us/download/details.aspx?id=43339)。 如果舊版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]早於 SQL Server 2012 也會安裝在電腦上，原生用戶端[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 11.0 會安裝由並行與舊版本。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 檔案 (sqlncli11.dll、sqlnclir11.rll 和 s11ch_sqlncli.chm) 會安裝到下列位置：  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式的所有適當的登錄設定，都會在安裝程序時進行。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭和程式庫檔 (sqlncli.h 和 sqlncli11.lib) 會安裝到下列位置：  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 除了在安裝[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端的一部分[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安裝，另外還有名為 sqlncli.msi，可以找到的可轉散發套件的安裝程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安裝光碟，在下列位置：`%CD%\Setup\`.  
  
 您可以透過 sqlncli.msi 散佈 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 當您部署應用程式時，可能必須安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 使用 Chainer 和 Bootstrapper 技術是安裝多個封裝 (但對使用者卻好像是單一安裝) 的一種方法。 如需詳細資訊，請參閱[撰寫適用於 Visual Studio 2005 的自訂啟動載入器套件](http://go.microsoft.com/fwlink/?LinkId=115667)和[新增自訂的必要條件](http://go.microsoft.com/fwlink/?LinkId=115668)。  
  
 x64 和 Itanium 版本的 sqlncli.msi 會安裝 32 位元版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 如果應用程式的目標使用平台與當初開發時的平台不同，您可以從 Microsoft 下載中心下載 x64、Itanium 和 x86 版本的 sqlncli.msi。  
  
 當您叫用 sqlncli.msi 時，依預設會安裝用戶端元件。 用戶端元件是支援應用程式執行的檔案 (應用程式則是利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 所開發)。 如果也要安裝 SDK 元件，請在命令列上指定 `ADDLOCAL=All`。 例如：  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>無訊息安裝  
 如果您搭配 msiexec 使用 /passive、/qn、/qb 或 /qr 選項，則也必須指定 IACCEPTSQLNCLILICENSETERMS=YES，以明確指出您接受使用者授權條款。 此選項必須以全部大寫的字母指定。  
  
## <a name="uninstalling-sql-server-native-client"></a>解除安裝 SQL Server Native Client  
 因為這類的應用程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]伺服器和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]工具取決於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client，請務必不解除安裝[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，直到所有相依的應用程式會解除安裝。 若要為使用者提供警告指出您的應用程式相依於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，使用的 APPGUID 安裝選項在您的 MSI，如下所示：  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 傳遞給 APPGUID 的值是您特定的產品代碼。 使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server Native Client 建立應用程式](installing-sql-server-native-client.md)   
 [安裝的使用說明主題](../../../sql-server/install/installation-how-to-topics.md)  
  
  
