---
title: 安裝 OLE DB Driver for SQL Server |Microsoft Docs
description: 安裝和解除安裝適用於 SQL Server 的 OLE DB 驅動程式
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 7e435aef0d4499f62ea8b6255ce25440436c3cbc
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106214"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>安裝 OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

若要安裝 OLE DB Driver for SQL Server 中，您需要 msoledbsql.msi 安裝程式。
執行安裝程式並進行您慣用的選項。 OLE DB Driver for SQL Server 可以是已安裝的並行和舊版的 Microsoft OLE DB 提供者。

OLE DB Driver for SQL Server 檔案 （msoledbsql.dll、 msoledbsqlr.rll） 會安裝在`%SYSTEMROOT%\system32\`。 此外，x64 msoledbsql.msi 會安裝在 32 位元二進位檔`%SYSTEMROOT%\SysWOW64\`。

> [!NOTE]  
> 所有適當的登錄設定 OLE DB driver for SQL Server 進行安裝程序的一部分。  

OLE DB Driver for SQL Server 標頭和程式庫檔案 （msoledbsql.h 和 msoledbsql.lib） 會安裝在`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\181\SDK`。 此外，x64 msoledbsql.msi 安裝中的相同檔案`%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\181\SDK`。  

您可以透過 msoledbsql.msi 來發佈適用於 SQL Server 的 OLE DB 驅動程式。 您可能必須安裝 OLE DB Driver for SQL Server，當您部署應用程式。 使用 Chainer 和 Bootstrapper 技術是安裝多個封裝 (但對使用者卻好像是單一安裝) 的一種方法。 如需詳細資訊，請參閱[撰寫適用於 Visual Studio 2005 的自訂啟動載入器套件](http://go.microsoft.com/fwlink/?LinkId=115667)和[新增自訂的必要條件](http://go.microsoft.com/fwlink/?LinkId=115668)。  
  
X64 msoledbsql.msi 也安裝 32 位元版本的 OLE DB Driver for SQL Server。 如果您的應用程式的目標平台上開發以外，您可以下載 msoledbsql.msi x64 和 x86 版本。

當您叫用 msoledbsql.msi 時，預設只會安裝用戶端元件。 用戶端元件是支援應用程式執行的檔案 (應用程式則是使用 OLE DB Driver for SQL Server 所開發)。 如果也要安裝 SDK 元件，請在命令列上指定 `ADDLOCAL=All`。 例如：  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>無訊息安裝  
 如果您搭配 msiexec 使用 /passive、/qn、/qb 或 /qr 選項，則也必須指定 IACCEPTMSOLEDBSQLLICENSETERMS=YES，以明確指出您接受使用者授權條款。 此選項必須以全部大寫的字母指定。  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>安裝 OLE DB Driver for SQL Server，做為相依性  
務必不解除安裝適用於 SQL Server OLE DB 驅動程式，直到所有相依的應用程式會解除安裝。 為使用者提供警告，應用程式相依於 OLE DB Driver for SQL Server 中，使用的 APPGUID 安裝選項在您的 MSI，如下所示：  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

傳遞給 APPGUID 的值是您特定的產品代碼。 使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。
APPGUID 選項需要從提升權限的命令提示字元執行安裝程式。

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
