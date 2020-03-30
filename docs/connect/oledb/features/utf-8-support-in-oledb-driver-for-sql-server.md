---
title: OLE DB Driver for SQL Server 中的 UTF-8 支援| Microsoft Docs
description: OLE DB Driver for SQL Server 中的 UTF-8 支援
ms.custom: ''
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: reference
ms.reviewer: v-kaywon
ms.author: jroth
author: rothja
ms.openlocfilehash: 340c1bdd7ab3ff54ffab52aebe08eeab258c7b41
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75257689"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 中的 UTF-8 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB Driver for SQL Server (18.2.1 版) 新增 UTF-8 伺服器編碼的支援。 如需有關 SQL Server UTF-8 支援的相關資訊，請參閱：
- [定序與 Unicode 支援](../../../relational-databases/collations/collation-and-unicode-support.md)
- [UTF-8 支援](#ctp23)

> [!IMPORTANT]
> Microsoft OLE DB Driver for SQL Server 使用 [GetACP](https://docs.microsoft.com/windows/win32/api/winnls/nf-winnls-getacp) 函式來判斷 DBTYPE_STR 輸入緩衝區的編碼方式。 不支援 GetACP 傳回 UTF-8 編碼的情況。 如果緩衝區需要儲存 Unicode 資料，緩衝區資料類型應該設定為 DBTYPE_WSTR (UTF-16 編碼)。

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>將資料插入至 UTF-8 編碼的 CHAR 或 VARCHAR 資料行
建立輸入參數緩衝區以用於插入時，會使用 [DBBINDING 結構](https://go.microsoft.com/fwlink/?linkid=2071182) \(英文\) 的陣列來描述緩衝區。 每個 DBBINDING 結構都會將單一參數關聯至取用者的緩衝區，並包含資料值的類型與長度等資訊。 針對類型 CHAR 的輸入參數緩衝區，應該將 DBBINDING 結構的 *wType* 設定為 DBTYPE_STR。 針對類型 WCHAR 的輸入參數緩衝區，應該將 DBBINDING 結構的 *wType* 設定為 DBTYPE_WSTR。

搭配參數執行命令時，驅動程式會建構參數資料類型資訊。 如果輸入緩衝區類型和參數資料類型相符，就不會在驅動程式中進行任何轉換。 否則，驅動程式會將輸入參數緩衝區轉換為參數資料類型。 使用者可以藉由呼叫 [ICommandWithParameters::SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577) \(英文\)，明確地設定參數資料類型。 若未提供此資訊，驅動程式就會 (a) 在陳述式備妥時從伺服器中擷取資料行中繼資料，或 (b) 嘗試從輸入參數資料類型進行預設轉換，藉以衍生參數資料類型資訊。

根據輸入緩衝區資料類型和參數資料類型而定，可能會透過驅動程式或伺服器來將輸入參數緩衝區轉換為伺服器資料行定序。 轉換期間，如果用戶端字碼頁或資料庫定序字碼頁無法表示輸入緩衝區中的所有字元，則可能會發生資料遺失。 下表描述將資料插入至啟用 UTF-8 的資料行時的轉換流程：

|緩衝區資料類型|參數資料類型|轉換|使用者預防措施|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|從用戶端字碼頁到資料庫定序字碼頁的伺服器轉換；從資料庫定序字碼頁到資料行定序字碼頁的伺服器轉換。|確定用戶端字碼頁和資料庫定序字碼頁均可表示輸入資料中的所有字元。 例如，若要插入波蘭文字元，可以將用戶端字碼頁設定為 1250 (ANSI 中歐語系)，而資料庫定序可以使用波蘭文作為定序指示項 (例如 Polish_100_CI_AS_SC) 或啟用 UTF-8。|
|DBTYPE_STR|DBTYPE_WSTR|從用戶端字碼頁到 UTF-16 編碼的驅動程式轉換；從 UTF-16 編碼到資料行定序字碼頁的伺服器轉換。|確定用戶端字碼頁可以表示輸入資料中的所有字元。 例如，若要插入波蘭文字元，可以將用戶端字碼頁設定為 1250 (ANSI 中歐語系)。|
|DBTYPE_WSTR|DBTYPE_STR|從 UTF-16 編碼到資料庫定序字碼頁的驅動程式轉換；從資料庫定序字碼頁到資料行定序字碼頁的伺服器轉換。|確定資料庫定序字碼頁可以表示輸入資料中的所有字元。 例如，若要插入波蘭文字元，資料庫定序字碼頁可以使用波蘭文作為定序指示項 (例如 Polish_100_CI_AS_SC) 或啟用 UTF-8。|
|DBTYPE_WSTR|DBTYPE_WSTR|從 UTF-16 到資料行定序字碼頁的伺服器轉換。|無。|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>從 UTF-8 編碼的 CHAR 或 VARCHAR 資料行擷取資料
針對擷取的資料建立緩衝區時，會使用 [DBBINDING 結構](https://go.microsoft.com/fwlink/?linkid=2071182) \(英文\) 的陣列來描述緩衝區。 每個 DBBINDING 結構都會與所擷取資料列中的單一資料行產生關聯。 若要以 CHAR 格式擷取資料行資料，將 DBBINDING 結構的 *wType* 設定為 DBTYPE_STR。 若要以 WCHAR 格式擷取資料行資料，將 DBBINDING 結構的 *wType* 設定為 DBTYPE_WSTR。

針對結果緩衝區類型指示器 DBTYPE_STR，驅動程式會將啟用 UTF-8 編碼的資料轉換為用戶端編碼。 使用者應該確定用戶端編碼可以表示來自 UTF-8 資料行的資料，否則可能會發生資料遺失。

針對結果緩衝區類型指示器 DBTYPE_WSTR，驅動程式會將啟用 UTF-8 編碼的資料轉換為 UTF-16 編碼。

<a name="ctp23"></a>

### <a name="utf-8-support-sql-server-2019-ctp-23"></a>UTF-8 支援 (SQL Server 2019 CTP 2.3)

[!INCLUDE[ss2019](../../../includes/sssqlv15-md.md)] 開始完整支援廣泛使用 UTF-8 字元編碼作為匯入或匯出編碼，或作為文字資料的資料庫層級或資料行層級定序。 UTF-8 允許用於 `CHAR` 和 `VARCHAR` 資料類型，並且在建立物件定序或將其變更為具有 `UTF8` 尾碼的定序時啟用。

例如，`LATIN1_GENERAL_100_CI_AS_SC` 至 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`。 UTF-8 僅適用於支援增補字元的 Windows 定序，已於 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中推出。 `NCHAR` 和 `NVARCHAR` 只允許 UTF-16 編碼，並維持不變。

此功能可能會節省大量儲存空間 (視使用的字元集而定)。 例如，使用啟用 UTF-8 的定序，將具有 ASCII (拉丁文) 字串的現有資料行資料類型從 `NCHAR(10)` 變更為 `CHAR(10)`，會使儲存體需求減少 50%。 這項減少的原因是 `NCHAR(10)` 需要 20 個位元組作為儲存空間，而 `CHAR(10)` 針對相同的 Unicode 字串需要 10 個位元組。

如需詳細資訊，請參閱 [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md)。

**CTP 2.1** 新增在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 安裝期間選取 UTF-8 定序作為預設的支援。

**CTP 2.2** 新增在 SQL Server 複寫中使用 UTF-8 字元編碼的支援。

**CTP 2.3** 新增在 BIN2 定序 (UTF8_BIN2) 中使用 UTF-8 字元編碼的支援。

## <a name="see-also"></a>另請參閱  
[OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[OLE DB Driver for SQL Server 中支援 UTF-16](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
