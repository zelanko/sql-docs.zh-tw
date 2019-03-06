---
title: OLE DB Driver for SQL Server 中的 UTF-8 支援| Microsoft Docs
description: OLE DB Driver for SQL Server 中的 UTF-8 支援
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: f410ddf4e3843936da6f93f488f379feea863e59
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744798"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 中的 UTF-8 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB Driver for SQL Server （版本 18.2.1） 新增支援 utf-8 伺服器版本編碼方式。 如需 SQL Server utf-8 支援資訊，請參閱：
- [定序與 Unicode 支援](../../../relational-databases/collations/collation-and-unicode-support.md)
- [UTF-8 支援 (CTP 2.2)](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-22)

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>資料插入 utf-8 編碼的 CHAR 或 VARCHAR 資料行
在建立時插入一個輸入的參數的緩衝區，所使用的陣列描述緩衝區[DBBINDING 結構](https://go.microsoft.com/fwlink/?linkid=2071182)。 每個 DBBINDING 結構使取用者緩衝區的單一參數，且包含資料值的類型與長度等資訊。 針對輸入的參數的型別 CHAR、 緩衝區*wType*的 DBBINDING 結構應該設定為 DBTYPE_STR。 針對輸入的參數緩衝區的型別 WCHAR *wType*的 DBBINDING 結構應該設定為 DBTYPE_WSTR。

當執行含有參數的命令，此驅動程式會建構參數資料類型資訊。 如果輸入的緩衝區型別和參數資料類型比對，驅動程式中不進行任何轉換。 否則驅動程式會將輸入的參數緩衝區轉換成參數資料類型。 參數資料類型可以明確設定使用者藉由呼叫[icommandwithparameters:: Setparameterinfo](https://go.microsoft.com/fwlink/?linkid=2071577)。 如果未提供的資訊，此驅動程式會衍生參數資料類型資訊 （a） 資料行中繼資料從伺服器擷取時準備的陳述式，或 （b） 嘗試從輸入的參數資料類型的預設轉換。

輸入的參數緩衝區可能會轉換成伺服器的資料行定序，驅動程式，或根據輸入的緩衝區的資料型別和參數資料類型的伺服器。 在轉換期間，如果用戶端字碼頁或資料庫的定序字碼頁無法表示在輸入緩衝區中的所有字元，可能會發生資料遺失。 下表描述轉換程序，將資料插入至 utf-8 啟用資料行：

|緩衝區的資料類型|參數資料類型|轉換|使用者的預防措施|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|用戶端字碼頁的伺服器轉換成資料庫定序字碼頁;資料庫定序字碼頁從伺服器轉換到資料行定序字碼頁。|請確定用戶端字碼頁和資料庫定序字碼頁，則可以代表輸入資料中的所有字元。 比方說，來插入波蘭文字元，可以設定用戶端字碼頁 1250 （ANSI 中歐），來和資料庫定序無法波蘭文做為定序指示項 (例如 Polish_100_CI_AS_SC)，或為 utf-8 啟用。|
|DBTYPE_STR|DBTYPE_WSTR|用戶端字碼頁的驅動程式轉換成 utf-16 編碼;從 utf-16 編碼方式為資料行定序字碼頁的伺服器轉換。|請確定用戶端字碼頁可代表輸入資料中的所有字元。 比方說，若要插入波蘭文的字元，用戶端字碼頁無法設定為 1250 （ANSI 中歐）。|
|DBTYPE_WSTR|DBTYPE_STR|從資料庫定序字碼頁; 的 utf-16 編碼的驅動程式轉換資料庫定序字碼頁從伺服器轉換到資料行定序字碼頁。|請確定資料庫定序字碼頁可代表輸入資料中的所有字元。 比方說，若要插入波蘭文的字元，資料庫的定序字碼頁無法波蘭文做為定序指示項 (例如 Polish_100_CI_AS_SC)，或為 utf-8 啟用。|
|DBTYPE_WSTR|DBTYPE_WSTR|從 utf-16 伺服器轉換到資料行定序字碼頁。|無。|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>資料擷取從 utf-8 編碼的 CHAR 或 VARCHAR 資料行
在建立時擷取資料的緩衝區，所使用的陣列描述緩衝區[DBBINDING 結構](https://go.microsoft.com/fwlink/?linkid=2071182)。 每個 DBBINDING 結構會將擷取的資料列中的單一資料行產生關聯。 若要擷取成 CHAR 資料行的資料，請設定*wType* DBTYPE_STR DBBINDING 結構。 若要擷取成 WCHAR 資料行的資料，請設定*wType* DBTYPE_WSTR DBBINDING 結構。

結果的緩衝區型別指示器 DBTYPE_STR，驅動程式會將 utf-8 編碼資料轉換成編碼的用戶端。 使用者應該確定用戶端的編碼方式來表示該資料從 utf-8 資料行，否則可能會發生資料遺失。

結果的緩衝區型別指示器 DBTYPE_WSTR，驅動程式會將 utf-8 編碼資料轉換成 utf-16 編碼。
  
## <a name="see-also"></a>另請參閱  
[OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[OLE DB Driver for SQL Server 中支援 UTF-16](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
