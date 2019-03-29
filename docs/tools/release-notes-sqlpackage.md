---
title: DacFx 和 SqlPackage 版本資訊 |Microsoft Docs
description: Microsoft sqlpackage 的版本資訊。
ms.custom: tools|sos
ms.date: 02/02/2019
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: kenvh
ms.openlocfilehash: de45add2b02686f990d68f7c1c23eec385848751
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538774"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe 的版本資訊

**[下載最新版本](sqlpackage-download.md)**

本文列出的功能和 SqlPackage.exe 發行版本所提供的修正。

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="181-sqlpackage"></a>18.1 sqlpackage

發行日期：&nbsp;2019 年 2 月 1 日  
組建：&nbsp;15.0.4316.1  
預覽版本。

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已新增的支援 UTF8 定序。 | &nbsp; |
| 啟用索引檢視表上的非叢集資料行存放區索引。 | &nbsp; |
| 移到.NET Core 2.2。 | &nbsp; |
| 使用.NET Core 上的結構描述比較支援的記憶體儲存體。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 若要使用的舊版基數估計工具進行反向工程查詢修正效能。 | &nbsp; |
| 產生指令碼時，請修正重大結構描述比較效能問題。 | &nbsp; |
| 修正結構描述漂移偵測邏輯，忽略特定的擴充的事件 (xevent) 工作階段。 | &nbsp; |
| 固定的匯入圖形資料表的排序。 | &nbsp; |
| 已修正匯出搭配物件權限的外部資料表。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題

此版本包含 sqlpackage 的目標.NET Core 2.2 的跨平台預覽組建。 Sqlpackage 可以在 macOS 和 Linux 上執行。

| 已知問題 | 詳細資料 |
| :---------- | :------ |
| 不支援建置和部署參與者。 | &nbsp; |
| 不支援使用 json 資料序列化的舊版.dacpac 及.bacpac 檔案。 | &nbsp; |
| 由於與區分大小寫的檔案系統的問題，可能無法解析參考的.dacpacs (例如 master.dacpac)。 | 因應措施是改為大寫的參考檔案 (例如 MASTER。BACPAC)。 |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

發行日期： &nbsp; 2018 年 10 月 24 日  
組建：&nbsp; 15.0.4200.1

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已新增的支援資料庫相容性層級 150。 | &nbsp; |
| 新增受控執行個體的支援。 | &nbsp; |
| 已新增的 MaxParallelism 命令列參數來指定資料庫作業的平行處理原則程度。 | &nbsp; |
| 已新增的 AccessToken 命令列參數來指定驗證權杖時連接到 SQL Server。 | &nbsp; |
| 已新增的支援匯入的資料流 BLOB/CLOB 資料型別。 | &nbsp; |
| 已新增支援純量 UDF 'INLINE' 選項。 | &nbsp; |
| 新增的圖形資料表 'MERGE' 語法的支援。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 已修正無法解析虛擬資料行圖形資料表。 | &nbsp; |
| 已修正使用記憶體最佳化檔案群組時的記憶體最佳化資料表用來建立資料庫。 | &nbsp; |
| 已修正，包括外部資料表上的擴充的屬性。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

發行日期：&nbsp;2018 年 6 月 22 日  
組建：&nbsp;14.0.4079.2

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 改善的連線失敗，包括 SqlClient 例外狀況訊息的錯誤訊息。 | &nbsp; |
| 匯入/匯出的單一分割區索引支援索引的壓縮。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 已修正 SQL 2017 和更新版本的 XML 資料行集的反向工程問題。 | &nbsp; |
| 已修正的問題，Azure SQL Database 指令碼的資料庫相容性層級 140 忽略。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

發行日期： &nbsp; 2018 年 1 月 25 日  
組建：&nbsp;14.0.3917.1

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已新增的 ThreadMaxStackSize 命令列參數，以剖析使用大量的巢狀陳述式的 TRANSACT-SQL。 | &nbsp; |
| 資料庫目錄定序支援。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 當內部部署執行個體，匯入 Azure SQL Database.bacpac，修復了錯誤，因為_在這個版本的 SQL Server 不支援沒有密碼的資料庫主要金鑰_。 | &nbsp; |
| 已修正無法解析的虛擬資料行錯誤圖形資料表。 | &nbsp; |
| 已修正使用 SchemaCompareDataModel 使用 SQL 驗證，來比較結構描述。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

發行日期：&nbsp;2017 年 12 月 27 日  
組建：&nbsp;14.0.3881.1

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已新增支援_時態保留原則_SQL 2017 + 和 Azure SQL Database。 | &nbsp; |
| 新增 /DiagnosticsFile:"C:\Temp\sqlpackage.log 」 命令列參數來指定要儲存診斷資訊的檔案路徑。 | &nbsp; |
| 已新增的 /Diagnostics 命令列參數，以記錄至主控台的診斷資訊。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 不會封鎖時遇到不了解資料庫相容性層級。 | 相反地，將假設為最新的 Azure SQL Database 或內部部署平台。 |
| &nbsp; | &nbsp; |
