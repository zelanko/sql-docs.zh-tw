---
title: 安裝適用於 SQL Server 的 OLE DB 驅動程式 |Microsoft 文件
description: 安裝和解除安裝適用於 SQL Server 的 OLE DB 驅動程式
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
ms.openlocfilehash: 3cb05e6fbbc3507aec67f4faa61f621c4245e7c8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ole-db-driver-for-sql-server"></a>安裝 SQL Server 的 OLE DB 驅動程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

若要安裝 SQL Server 的 OLE DB 驅動程式中，您需要 msoledbsql.msi 安裝程式。
執行安裝程式以您慣用的選項。 SQL Server OLE DB 驅動程式可以由-並行安裝舊版的 Microsoft OLE DB 提供者。

SQL Server 檔案 （msoledbsql.dll、 msoledbsqlr.rll） OLE DB 驅動程式會安裝在`%SYSTEMROOT%\system32\`。 此外，x64 msoledbsql.msi 會安裝 32 位元二進位檔案中的`%SYSTEMROOT%\SysWOW64\`。

> [!NOTE]  
> 所有適當的登錄設定 OLE DB 驅動程式的 SQL Server 會安裝程序的一部分。  

SQL Server 標頭和程式庫檔案 （msoledbsql.h 和 msoledbsql.lib） OLE DB 驅動程式會安裝在`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`。 此外，x64 msoledbsql.msi 安裝中的相同檔案`%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`。  

您可以透過 msoledbsql.msi，適用於 SQL Server 散發 OLE DB 驅動程式。 您可能必須在部署應用程式時，適用於 SQL Server 安裝 OLE DB 驅動程式。 使用 Chainer 和 Bootstrapper 技術是安裝多個封裝 (但對使用者卻好像是單一安裝) 的一種方法。 如需詳細資訊，請參閱[撰寫的自訂啟動載入器封裝適用於 Visual Studio 2005](http://go.microsoft.com/fwlink/?LinkId=115667)和[加入自訂的必要條件](http://go.microsoft.com/fwlink/?LinkId=115668)。  
  
X64 msoledbsql.msi 也會安裝 32 位元版本的 OLE DB 驅動程式適用於 SQL Server。 如果您的應用程式的目標平台上開發以外，您可以下載 msoledbsql.msi x64 和 x86 版本。

當您叫用 msoledbsql.msi 時，預設會安裝用戶端元件。 用戶端元件是支援執行使用適用於 SQL Server 的 OLE DB 驅動程式所開發的應用程式的檔案。 如果也要安裝 SDK 元件，請在命令列上指定 `ADDLOCAL=All`。 例如：  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>無訊息安裝  
 如果您搭配 msiexec 使用 /passive、 /qn、 /qb 或 /qr 選項，您也必須指定 IACCEPTMSOLEDBSQLLICENSETERMS = YES，以明確地指出您接受使用者授權條款。 此選項必須以全部大寫的字母指定。  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>安裝適用於 SQL Server 的 OLE DB 驅動程式，做為相依性  
它是適用於 SQL Server 中解除安裝 OLE DB 驅動程式，直到所有相依的應用程式會解除安裝。 若要為使用者提供警告適用於 SQL Server 的應用程式相依於 OLE DB 驅動程式，使用 APPGUID 安裝選項 MSI 中,，如下所示：  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

傳遞給 APPGUID 的值是您特定的產品代碼。 使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。
APPGUID 選項需要提高權限的命令提示字元執行安裝程式。

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
