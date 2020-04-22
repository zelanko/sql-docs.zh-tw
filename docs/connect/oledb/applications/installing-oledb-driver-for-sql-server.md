---
title: 安裝 OLE DB Driver for SQL Server | Microsoft Docs
description: 安裝和解除安裝 OLE DB Driver for SQL Server。 若要安裝 OLE DB Driver for SQL Server，您需要 msoledbsql.msi 安裝程式
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
ms.openlocfilehash: b971b7e537cecc7e94c87e2692707594fda9aebc
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528382"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>安裝 OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

若要安裝 OLE DB Driver for SQL Server，您需要 msoledbsql.msi 安裝程式。
執行安裝程式，並進行您慣用的選擇。 OLE DB Driver for SQL Server 可以與舊版 Microsoft OLE DB 提供者並存安裝。

OLE DB Driver for SQL Server 檔案 (msoledbsql.dll、msoledbsqlr.rll) 會安裝在 `%SYSTEMROOT%\system32\` 中。 此外，x64 msoledbsql.msi 會在 `%SYSTEMROOT%\SysWOW64\` 中安裝 32 位元的二進位檔。

> [!NOTE]  
> 所有適當的 OLE DB Driver for SQL Server 登錄設定都會在安裝程序時進行。  

OLE DB Driver for SQL Server 標頭和程式庫檔案 (msoledbsql.h 和 msoledbsql.lib) 會安裝在 `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK` 中。 此外，x64 msoledbsql.msi 會在 `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK` 中安裝相同的檔案。  

您可以透過 msoledbsql.msi 散發 OLE DB Driver for SQL Server。 當您部署應用程式時，可能必須安裝 OLE DB Driver for SQL Server。 使用 Chainer 和 Bootstrapper 技術是安裝多個封裝 (但對使用者卻好像是單一安裝) 的一種方法。 如需詳細資訊，請參閱[撰寫適用於 Visual Studio 2005 的自訂啟動載入器套件](https://go.microsoft.com/fwlink/?LinkId=115667)和[新增自訂的必要條件](https://go.microsoft.com/fwlink/?LinkId=115668)。  
  
x64 msoledbsql.msi 也會安裝 32 位元版本的 OLE DB Driver for SQL Server。 如果應用程式的目標使用平台與當初開發時的平台不同，您可以下載 x64 和 x86 版本的 msoledbsql.msi。

當您叫用 msoledbsql.msi 時，預設只會安裝用戶端元件。 用戶端元件是支援應用程式執行的檔案，應用程式則是使用 OLE DB Driver for SQL Server 所開發。 如果也要安裝 SDK 元件，請在命令列上指定 `ADDLOCAL=All`。 例如：  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>無訊息安裝  
 如果您搭配 msiexec 使用 /passive、/qn、/qb 或 /qr 選項，則也必須指定 IACCEPTMSOLEDBSQLLICENSETERMS=YES，以明確指出您接受使用者授權條款。 此選項必須以全部大寫的字母指定。  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>將 OLE DB Driver for SQL Server 安裝為相依性  
在解除安裝所有相依的應用程式之前，請務必不要解除安裝 OLE DB Driver for SQL Server。 若要為使用者提供指出應用程式相依於 OLE DB Driver for SQL Server 的警告，請使用 MSI 中的 APPGUID 安裝選項，如下所示：  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

傳遞給 APPGUID 的值是您特定的產品代碼。 使用 Microsoft Installer 來封裝應用程式安裝程式時，必須建立產品代碼。
APPGUID 選項需要從提高權限的命令提示字元執行安裝程式。

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
