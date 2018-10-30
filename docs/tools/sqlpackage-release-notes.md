---
title: Microsoft DacFx & sqlpackage 版本資訊 |Microsoft Docs
description: Microsoft sqlpackage 版本資訊
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: c146426a9c325eec721e3289d711d0a00a632e2c
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050850"
---
# <a name="sqlpackage-release-notes"></a>sqlpackage 版本資訊

**[下載最新版本](sqlpackage-download.md)**

## <a name="sqlpackage-180"></a>sqlpackage 18.0

發行日期： 2018 年 10 月 24 日  
建置： 15.0.4200.1 

版本包含下列功能和修正程式：

- 已新增的支援資料庫相容性層級 150。
- 新增受控執行個體的支援。
- 已新增的 MaxParallelism 命令列參數來指定資料庫作業的平行處理原則程度。
- 新增 AccessToken 的命令列參數，來連接到 SQL Server 時，指定驗證權杖。
- 已新增的支援匯入的資料流 BLOB/CLOB 資料型別。
- 已新增支援純量 UDF 'INLINE' 選項。
- 新增的圖形資料表 'MERGE' 語法的支援。
- 已修正無法解析虛擬資料行圖形資料表。
- 已修正使用記憶體最佳化檔案群組時的記憶體最佳化資料表用來建立資料庫。
- 已修正，包括外部資料表上的擴充的屬性。

## <a name="sqlpackage-178"></a>sqlpackage 17.8

發行日期：2018 年 6 月 22 日  
組建：14.0.4079.2  

版本包含下列修正：

- 改善的連線失敗，包括 SqlClient 例外狀況訊息的錯誤訊息。
- 匯入/匯出的單一分割區索引支援索引的壓縮。
- 已修正 SQL 2017 和更新版本的 XML 資料行集的反向工程問題。
- 已修正的問題，Azure SQL Database 指令碼的資料庫相容性層級 140 忽略。

## <a name="sqlpackage-1741"></a>sqlpackage 17.4.1

發行日期： 2018 年 1 月 25 日  
組建：14.0.3917.1

版本包含下列修正：

- 當正在 Azure SQL Database.bacpac 匯入至內部部署執行個體，已修正錯誤，因為 '沒有密碼的資料庫主要金鑰不支援在這個版本的 SQL Server'。
- 資料庫目錄定序支援。
- 已修正無法解析的虛擬資料行錯誤圖形資料表。
- 已新增的 ThreadMaxStackSize 命令列參數，以剖析 TSQL 且含有大量巢狀陳述式。
- 已修正使用 SchemaCompareDataModel 使用 SQL 驗證，來比較結構描述。

## <a name="sqlpackage-1740"></a>sqlpackage 17.4.0

發行日期：2017 年 12 月 12 日  
組建：14.0.3881.1

版本包含下列修正：

- 不會封鎖時遇到資料庫相容性層級不了解。 相反地，將假設的最新的 Azure SQL Database 或內部部署平台。
- SQL2017 + 和 Azure SQL Database 上的 「 時態保留原則 」 所新增的支援。
- 新增 /DiagnosticsFile:"C:\Temp\sqlpackage.log 」 命令列參數來指定要儲存診斷資訊的檔案路徑。
- 已新增的 /Diagnostics 命令列參數，以記錄至主控台的診斷資訊。

## <a name="sqlpackage-on-macos-and-linux-001-preview"></a>在 macOS 和 Linux 0.0.1 （預覽） 上的 sqlpackage

發行日期：2018 年 5 月 9 日  
組建：15.0.4057.1

此版本包含.NET Core 2.0 為目標的 sqlpackage 的跨平台預覽組建，並可在 macOS 和 Linux 上執行。 

此版本是早期預覽，具有下列已知問題：

- /P:CommandTimeout 參數是硬式編碼為 120。
- 不支援建置和部署參與者。
  - 移至.NET Core 2.1 受到 System.ComponentModel.Composition.dll 之後，將會修正。
  - 需要處理區分大小寫的路徑。
- 不支援 SQL CLR UDT 類型，包括 SQL Server CLR UDT 類型： SqlGeography，SqlGeometry，& SqlHierarchyId。
- 不支援使用 json 資料序列化的舊版.dacpac 及.bacpac 檔案。
- 由於與區分大小寫的檔案系統的問題，可能無法解析參考的.dacpacs (例如 master.dacpac)。
  - 因應措施是改為大寫的參考檔案 (例如 MASTER。BACPAC)。
