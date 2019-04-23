---
title: OLE DB Driver for SQL Server 中的 UTF-8 支援| Microsoft Docs
description: OLE DB Driver for SQL Server 中的 UTF-8 支援
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 4a30b233190817faee581106db5c8a18695a00d1
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583011"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 中的 UTF-8 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB Driver for SQL Server (18.2.1 版) 新增 UTF-8 伺服器編碼的支援。 如需有關 SQL Server UTF-8 支援的相關資訊，請參閱：
- [定序與 Unicode 支援](../../../relational-databases/collations/collation-and-unicode-support.md)
- [UTF-8 支援](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-23)

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
  
## <a name="see-also"></a>另請參閱  
[OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[OLE DB Driver for SQL Server 中支援 UTF-16](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
