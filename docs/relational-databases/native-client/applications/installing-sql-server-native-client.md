---
title: "安裝 SQL Server Native Client |Microsoft 文件"
ms.custom: 
ms.date: 07/15/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
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
caps.latest.revision: "44"
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 96dba471bb1b3de2b04561392b29eaa173bed6a0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="installing-sql-server-native-client"></a>安裝 SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 > 如需舊版的 SQL Server 相關的內容，請參閱[安裝 SQL Server Native Client](https://msdn.microsoft.com/en-US/library/ms131321(SQL.120).aspx)。

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Microsoft[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安裝時，會安裝 Native Client 11.0 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]。 
 
 沒有任何 SQL Server 2016 Native Client。 如需詳細資訊，請參閱[SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client.md)。 
 
您也可以從 SQL Server 2012 功能套件網頁取得 sqlncli.msi。 若要下載最新版本的 SQL Server Native Client，請移至[Microsoft® SQL Server® 2012 Feature Pack](http://www.microsoft.com/en-us/download/confirmation.aspx?id=29065)。 如果舊版[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]早於 SQL Server 2012 也會安裝在電腦上，原生用戶端[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 11.0 會由-並行安裝較舊的版本。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 檔案 (sqlncli11.dll、sqlnclir11.rll 和 s11ch_sqlncli.chm) 會安裝到下列位置：  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式的所有適當的登錄設定，都會在安裝程序時進行。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 標頭和程式庫檔 (sqlncli.h 和 sqlncli11.lib) 會安裝到下列位置：  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 除了安裝[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端當成部分[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安裝，也是可轉散發安裝程式，名為 sqlncli.msi，可以找到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安裝磁碟，在下列位置：`%CD%\Setup\`.  
  
 您可以透過 sqlncli.msi 散佈 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 當您部署應用程式時，可能必須安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 使用 Chainer 和 Bootstrapper 技術是安裝多個封裝 (但對使用者卻好像是單一安裝) 的一種方法。 如需詳細資訊，請參閱[撰寫的自訂啟動載入器封裝適用於 Visual Studio 2005](http://go.microsoft.com/fwlink/?LinkId=115667)和[加入自訂的必要條件](http://go.microsoft.com/fwlink/?LinkId=115668)。  
  
 x64 和 Itanium 版本的 sqlncli.msi 會安裝 32 位元版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client。 如果應用程式的目標使用平台與當初開發時的平台不同，您可以從 Microsoft 下載中心下載 x64、Itanium 和 x86 版本的 sqlncli.msi。  
  
 當您叫用 sqlncli.msi 時，依預設會安裝用戶端元件。 用戶端元件是支援應用程式執行的檔案 (應用程式則是利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 所開發)。 如果也要安裝 SDK 元件，請在命令列上指定 `ADDLOCAL=All`。 例如：  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>無訊息安裝  
 如果您搭配 msiexec 使用 /passive、/qn、/qb 或 /qr 選項，則也必須指定 IACCEPTSQLNCLILICENSETERMS=YES，以明確指出您接受使用者授權條款。 此選項必須以全部大寫的字母指定。  
  
## <a name="uninstalling-sql-server-native-client"></a>解除安裝 SQL Server Native Client  
 因為應用程式，例如[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]伺服器和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]工具取決於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，請務必不解除安裝[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，直到所有相依的應用程式會解除安裝。 若要為使用者提供警告指出應用程式相依於[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端，使用 APPGUID 安裝選項中程式 MSI，如下所示：  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 傳遞給 APPGUID 的值是您特定的產品代碼。 使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。  
  
## <a name="see-also"></a>請參閱＜  
 [使用 SQL Server Native Client 建立應用程式](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)   
 [安裝的使用說明主題](http://msdn.microsoft.com/library/59de41e7-557f-462a-8914-53ec35496baa)  
  
  
