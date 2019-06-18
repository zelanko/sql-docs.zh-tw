---
title: DacFx 和 SqlPackage 版本資訊 | Microsoft Docs
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
ms.openlocfilehash: 411a2cf4c9a3170e9fb3a3dc7709d8b3882f066b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183698"
---
# <a name="release-notes-for-sqlpackageexe"></a>SqlPackage.exe 的版本資訊

**[下載最新版本](sqlpackage-download.md)**

本文會列出 SqlPackage.exe 發行版本所提供的功能與修正。

<!--
TODO:
The Introduction text needs to add clarity regarding the relationship between
'SqlPackage.exe' and 'DacFx' (the Microsoft 'Data-Tier Application Framework').
One added sentence would be sufficient.

Or, if there is no relationship, remove 'DacFx' from the metadata 'title:'.

I discussed this with SStein (SteveStein).
Thanks.  GeneMi (MightyPen in GitHub).  2019-03-27
-->

## <a name="182-sqlpackage"></a>18.2 sqlpackage

發行日期：&nbsp;2019 年 4 月 15 日  
組建：&nbsp; 15.0.4384.2 

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 針對邊緣條件約束與邊緣條件約束子句新增圖形資料表支援。 | &nbsp; |
| 已啟用模型驗證規則，以針對 SQL Server 2016 和更新版本支援 32 個索引鍵資料行。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 修正因為使用了不支援的查詢提示，而對 SQL Server 2016 RTM 資料庫進行反向工程。 | &nbsp; |
| 修正在建立檔案群組陳述式前發生之自動關閉 alter 陳述式的部署順序。 | &nbsp; |
| 修正 ScriptDom 剖析迴歸，其中會將 'URL' 字串解譯為最上層權杖。 | &nbsp; |
| 修正在剖析 alter 資料表新增 index 陳述式時的 Null 參考例外狀況。 | &nbsp; |
| 已針對一律顯示為不同且可為 Null 之保存的計算資料行修正結構描述比較。| &nbsp; |
| &nbsp; | &nbsp; |

## <a name="181-sqlpackage"></a>18.1 sqlpackage

發行日期：&nbsp;2019 年 2 月 1 日  
組建：&nbsp;15.0.4316.1  
預覽版本。

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已新增 UTF8 定序的支援。 | &nbsp; |
| 已在索引檢視表上啟用非叢集資料行存放區索引。 | &nbsp; |
| 移到 .NET Core 2.2。 | &nbsp; |
| 在 .NET Core 上使用記憶體支援的儲存體來進行結構描述比較。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 使用舊版基數估計工具進行反向工程查詢的效能修正。 | &nbsp; |
| 已修正在產生指令碼時所發生的重大結構描述比較效能問題。 | &nbsp; |
| 已修正結構描述漂移偵測邏輯，以忽略特定的擴充事件 (xevent) 工作階段。 | &nbsp; |
| 已修正圖形資料表的匯入順序。 | &nbsp; |
| 已修正搭配物件權限匯出外部資料表。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題

此版本包含目標為 .NET Core 2.2 之 sqlpackage 的跨平台預覽組建。 Sqlpackage 可以在 macOS 和 Linux 上執行。

| 已知問題 | 詳細資料 |
| :---------- | :------ |
| 不支援建置和部署參與者。 | &nbsp; |
| 不支援使用 JSON 資料序列化的舊版 .dacpac 和 .bacpac 檔案。 | &nbsp; |
| 由於發生區分大小寫的檔案系統問題，因此可能無法解析參考的 .dacpacs (例如 master.dacpac)。 | 因應措施是將參考檔案的名稱改為大寫 (例如 MASTER.BACPAC)。 |
| &nbsp; | &nbsp; |

## <a name="180-sqlpackage"></a>18.0 sqlpackage

發行日期：&nbsp;2018 年 10 月 24 日  
組建：&nbsp; 15.0.4200.1

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已新增資料庫相容性層級 150 的支援。 | &nbsp; |
| 已新增受控執行個體的支援。 | &nbsp; |
| 已新增 MaxParallelism 命令列參數，可指定資料庫作業的平行處理原則程度。 | &nbsp; |
| 已新增 AccessToken 命令列參數，可指定連線至 SQL Server 時的驗證權杖。 | &nbsp; |
| 已新增支援串流處理 BLOB/CLOB 資料類型以用於匯入。 | &nbsp; |
| 已新增純量 UDF 'INLINE' 選項的支援。 | &nbsp; |
| 已新增圖形資料表 'MERGE' 語法的支援。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 已針對圖形資料表修正無法解析的虛擬資料行。 | &nbsp; |
| 已修正在使用記憶體最佳化的資料表時，透過記憶體最佳化的檔案群組來建立資料庫。 | &nbsp; |
| 已修正在外部資料表上包含擴充屬性。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="178-sqlpackage"></a>17.8 sqlpackage

發行日期：&nbsp;2018 年 6 月 22 日  
組建：&nbsp;14.0.4079.2

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已改進連線失敗的錯誤訊息，包括 SqlClient 例外狀況訊息。 | &nbsp; |
| 在單一分割區索引上支援索引壓縮以用於匯入/匯出。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 已修正使用 SQL 2017 和更新版本的 XML 資料行集的反向工程問題。 | &nbsp; |
| 已針對 Azure SQL Database 修正對資料庫相容性層級 140 進行指令碼處理會遭到忽略的問題。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1741-sqlpackage"></a>17.4.1 sqlpackage

發行日期：&nbsp;2018 年 1 月 25 日  
組建：&nbsp;14.0.3917.1

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已新增 ThreadMaxStackSize 命令列參數，可使用大量巢狀陳述式來剖析 Transact-SQL。 | &nbsp; |
| 資料庫目錄定序支援。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 將 Azure SQL Database .bacpac 匯入至內部部署執行個體時，已修正因為「此版本的 SQL Server 不支援沒有密碼的資料庫主要金鑰」  而引發的錯誤。 | &nbsp; |
| 已針對圖形資料表修正無法解析的虛擬資料行錯誤。 | &nbsp; |
| 已修正使用 SchemaCompareDataModel 搭配 SQL 驗證來比較結構描述。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="1740-sqlpackage"></a>17.4.0 sqlpackage

發行日期：&nbsp;2017 年 12 月 27 日  
組建：&nbsp;14.0.3881.1

### <a name="features"></a>功能

| 功能 | 詳細資料 |
| :------ | :------ |
| 已在 SQL 2017+ 和 Azure SQL Database 上新增「時態性保留原則」  的支援。 | &nbsp; |
| 已新增 /DiagnosticsFile:"C:\Temp\sqlpackage.log" 命令列參數，可指定要儲存診斷資訊的檔案路徑。 | &nbsp; |
| 已新增 /Diagnostics 命令列參數，可將診斷資訊記錄至主控台。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixes"></a>修正

| Fix | 詳細資料 |
| :-- | :------ |
| 在遇到不了解的資料庫相容性層級時不要封鎖。 | 相反地，將假設為最新的 Azure SQL Database 或內部部署平台。 |
| &nbsp; | &nbsp; |
