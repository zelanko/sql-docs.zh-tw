---
title: 安裝 OLE DB Driver for SQL Server | Microsoft Docs
description: 安裝和卸載 SQL Server 的 OLE DB 驅動程式
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, uninstalling
- MSOLEDBSQL, installing
- MSOLEDBSQL, uninstalling
- Setup [OLE DB Driver for SQL Server]
- uninstalling OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server
- installing OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, installing
- data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server
- removing OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 08f33d84ee8c035e1e1d3818e2a036f96af2a280
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989316"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>安裝 OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

若要安裝 SQL Server 的 OLE DB 驅動程式, 您需要內含 msoledbsql.h 安裝程式。
執行安裝程式, 並進行您偏好的選擇。 SQL Server 的 OLE DB 驅動程式可以與舊版 Microsoft OLE DB 提供者並存安裝。

SQL Server 檔案的 OLE DB 驅動程式 (內含 msoledbsql.h, msoledbsqlr. semsfc.rll) 會安裝在中`%SYSTEMROOT%\system32\` 。 此外, x64 內含 msoledbsql.h 會在中`%SYSTEMROOT%\SysWOW64\`安裝32位的二進位檔。

> [!NOTE]  
> 所有適用于 SQL Server 的 OLE DB 驅動程式的登錄設定, 都是在安裝過程中進行。  

SQL Server 標頭和程式庫檔案 (內含 msoledbsql.h 和內含 msoledbsql.h) 的 OLE DB 驅動程式會安裝在中`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`。 此外, x64 內含 msoledbsql.h 也會在中`%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`安裝相同的檔案。  

您可以透過內含 msoledbsql.h 散發 SQL Server 的 OLE DB 驅動程式。 當您部署應用程式時, 您可能必須安裝 SQL Server 的 OLE DB 驅動程式。 使用 Chainer 和 Bootstrapper 技術是安裝多個封裝 (但對使用者卻好像是單一安裝) 的一種方法。 如需詳細資訊，請參閱[撰寫適用於 Visual Studio 2005 的自訂啟動載入器套件](https://go.microsoft.com/fwlink/?LinkId=115667)和[新增自訂的必要條件](https://go.microsoft.com/fwlink/?LinkId=115668)。  
  
X64 內含 msoledbsql.h 也會安裝32位版本的 OLE DB 驅動程式以進行 SQL Server。 如果您的應用程式是以開發所在的平臺為目標, 您可以下載適用于 x64 和 x86 的內含 msoledbsql.h 版本。

當您叫用 msoledbsql.msi 時，預設只會安裝用戶端元件。 用戶端元件是支援應用程式執行的檔案，應用程式則是使用 OLE DB Driver for SQL Server 所開發。 如果也要安裝 SDK 元件，請在命令列上指定 `ADDLOCAL=All`。 例如：  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>自動安裝  
 如果您搭配 msiexec 使用 /passive、/qn、/qb 或 /qr 選項，則也必須指定 IACCEPTMSOLEDBSQLLICENSETERMS=YES，以明確指出您接受使用者授權條款。 此選項必須以全部大寫的字母指定。  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>將 SQL Server 的 OLE DB 驅動程式安裝為相依性  
在卸載所有相依的應用程式之前, 請務必不要卸載 SQL Server 的 OLE DB 驅動程式。 若要為使用者提供一則警告, 指出您的應用程式相依于 SQL Server 的 OLE DB 驅動程式, 請使用 MSI 中的 APPGUID 安裝選項, 如下所示:  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

傳遞給 APPGUID 的值是您特定的產品代碼。 使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。
APPGUID 選項需要從提高許可權的命令提示字元執行安裝程式。

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
