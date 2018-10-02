---
title: 選項 (SQL Server 物件總管 - 指令碼頁面) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a78a5b477fd92610ba4685cac96cb398d590634d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662496"
---
# <a name="options-sql-server-object-explorer---scripting-page"></a>選項 (SQL Server 物件總管 - 指令碼頁面)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
使用此頁面設定指定碼選項，以在**物件總管**之物件操作功能表的下列命令中使用：  
  
-   使用者資料表與檢視的 [編輯] 命令。  
  
-   使用者建立之物件的 編寫 <object> 。  
  
-   使用者建立之物件的 [修改] 命令。  
  
-   此頁面也可設定 [產生 SQL Server 指令碼精靈] 的編寫指令碼選項預設值。  
  
## <a name="remarks"></a>Remarks  
即使選項設定相同，編輯 與 修改 命令所產生的結果，可能會與 編寫 <object>命令所產生的結果不同。 [編輯] 與 [修改] 命令的設計讓您可以在查詢編輯器工作階段期間，修改目前資料庫中的物件。 [編寫 <object> 指令碼為] 命令的設計則在讓您產生指令碼，供日後建立物件之用。  
  
## <a name="options"></a>選項。  
在每個選項右方的清單中選取可用的設定，即可指定指令碼選項。  
  
### <a name="general-scripting-options"></a>一般指令碼選項  
**分隔個別陳述式**  
使用批次分隔符號來分隔個別 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 若要變更**查詢編輯器**的預設批次分隔符號，請選取 工具/選項/查詢執行/SQL Server/一般/批次分隔符號。 預設值是 False。 如需詳細資訊，請參閱 [GO (TRANSACT-SQL)](https://msdn.microsoft.com/b2ca6791-3a07-4209-ba8e-2248a92dd738)。  
  
**包含描述性標頭**  
透過將每個物件的指令碼分隔成區段，在指令碼中加入描述性註解。 預設值是 True。 如需詳細資訊，請參閱 [/*...*/ (Comment) (Transact-SQL)](https://msdn.microsoft.com/4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c)。  
  
**包含啟用 vardecimal 壓縮**  
加入 Vardecimal 儲存選項。 預設值是 False。 如需詳細資訊，請參閱 [sp_db_vardecimal_storage_format (Transact-SQL)](https://msdn.microsoft.com/9920b2f7-b802-4003-913c-978c17ae4542)。  
  
**編寫變更追蹤的指令碼**  
在指令碼中包含變更追蹤資訊。  
  
**編寫全文檢索目錄的指令碼**  
加入全文檢索目錄的指令碼。 預設值是 False。 如需詳細資訊，請參閱 [CREATE FULLTEXT CATALOG (TRANSACT-SQL)](https://msdn.microsoft.com/d7a8bd93-e2d7-4a40-82ef-39069e65523b)。  
  
**指令碼 USE <database>**  
將 USE DATABASE 陳述式新增到指令碼中，可在目前的 **物件總管** 資料庫內容中建立資料庫物件。 如果預期指令碼會用於不同的資料庫，請選取 False 省略。 預設值是 True。 如需詳細資訊，請參閱 [USE (TRANSACT-SQL)](https://msdn.microsoft.com/c05acac8-c063-4770-8e36-d7f71d500b10)。  
  
### <a name="object-scripting-options"></a>物件指令碼選項  

：在卸除或改變前檢查給定名稱的物件是否存在，或在建立前檢查給定名稱的物件是否不存在。 如需詳細資訊，請參閱 [IF...ELSE (Transact-SQL)](https://msdn.microsoft.com/676c881f-dee1-417a-bc51-55da62398e81) and [EXISTS (Transact-SQL)](https://msdn.microsoft.com/b6510a65-ac38-4296-a3d5-640db0c27631)。

**產生相依物件的指令碼**  
針對執行選取物件之指令碼時所需的其他物件，產生指令碼。 預設值是 False。  
  
**結構描述會限定物件名稱**  
使用物件結構描述來限定物件名稱。 預設值是 False。 如需詳細資訊，請參閱 [建立資料庫結構描述](../../relational-databases/security/authentication-access/create-a-database-schema.md)。  

**編寫資料壓縮選項的指令碼**：在指令碼中包含資料壓縮選項。 預設值是 False。

**編寫擴充屬性的指令碼**  
當物件具有擴充屬性時，在指令碼中包含擴充屬性。 預設值是 False。 如需詳細資訊，請參閱 [sp_addextendedproperty (TRANSACT-SQL)](https://msdn.microsoft.com/565483ea-875b-4133-b327-d0006d2d7b4c)。  
  
**編寫擁有者的指令碼**  
將擁有者包括在產生的指令碼中。 預設值是 False。  
  
**編寫權限的指令碼**  
在指令碼中加入資料庫物件的權限。 預設值是 True。 如需詳細資訊，請參閱 [權限](../../relational-databases/security/permissions-database-engine.md)。  
  
### <a name="tableview-options"></a>資料表/檢視選項  
下列選項只適用於資料表或檢視的指令碼。  
  
**將使用者自訂資料類型轉換成基底類型**  
將使用者自訂資料類型轉換成用以建立這些資料類型的基底類型。 當來源資料庫使用者自訂資料類型不存在於執行指令碼的資料庫時，請使用 True。 請使用 False 來保留使用者自訂資料類型。 預設值是 False。 如需詳細資訊，請參閱 [CREATE TYPE (TRANSACT-SQL)](https://msdn.microsoft.com/2202236b-e09f-40a1-bbc7-b8cff7488905)。  
  
**產生 SET ANSI PADDING 命令**  
在每個 CREATE TABLE 陳述式前後加入 SET ANSI_PADDING 陳述式。 預設值是 True。 如需詳細資訊，請參閱 [SET ANSI_PADDING (TRANSACT-SQL)](https://msdn.microsoft.com/92bd29a3-9beb-410e-b7e0-7bc1dc1ae6d0)。  
  
**包含定序**  
在資料行定義中加入定序。 預設值是 True。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
**包含 IDENTITY 屬性**  
加入 IDENTITY 種子和 IDENTITY 遞增的定義。 預設值是 True。 如需詳細資訊，請參閱 [IDENTITY (屬性) (TRANSACT-SQL)](https://msdn.microsoft.com/8429134f-c821-4033-a07c-f782a48d501c)。  
  
**結構描述會限定外部索引鍵參考**  
在 FOREIGN KEY 條件約束的資料表參考中加入結構描述名稱。 預設值是 True。  
  
**編寫繫結預設值和規則的指令碼**  
加入 **sp_bindefault** 及 **sp_bindrule** 繫結預存程序呼叫。 預設值是 True。 如需詳細資訊，請參閱 [sp_bindefault (TRANSACT-SQL)](https://msdn.microsoft.com/3da70c10-68d0-4c16-94a5-9e84c4a520f6) 及 [sp_bindrule (TRANSACT-SQL)](https://msdn.microsoft.com/2606073e-c52f-498d-a923-5026b9d97e67)。  
  
**編寫 CHECK 條件約束的指令碼**  
將 [CHECK 條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 指令碼。 預設值是 True。  
  
**編寫預設值的指令碼**  
在指令碼中加入資料行預設值。 預設值是 False。 如需詳細資訊，請參閱 [CREATE DEFAULT (TRANSACT-SQL)](https://msdn.microsoft.com/08475db4-7d90-486a-814c-01a99d783d41)。  
  
**編寫檔案群組的指令碼**  
在資料表定義的 ON 子句中指定檔案群組。 預設值是 False。 如需詳細資訊，請參閱 [CREATE TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/1e068443-b9ea-486a-804f-ce7b6e048e8b)。  
  
**編寫外部索引鍵的指令碼**  
將 [FOREIGN KEY 條件約束](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 加入指令碼。 預設值是 False。  
  
**編寫全文檢索索引的指令碼**  
在指令碼中加入全文檢索索引。 預設值是 False。 如需詳細資訊，請參閱 [CREATE FULLTEXT CATALOG (TRANSACT-SQL)](https://msdn.microsoft.com/8b80390f-5f8b-4e66-9bcc-cabd653c19fd)。  
  
**編寫索引的指令碼**  
在指令碼中加入叢集、非叢集和 XML 索引。 預設值是 True。 如需詳細資訊，請參閱 [CREATE FULLTEXT CATALOG (TRANSACT-SQL)](https://msdn.microsoft.com/d2297805-412b-47b5-aeeb-53388349a5b9)。  
  
**編寫分割區結構描述的指令碼**  
在指令碼中加入資料表分割區結構描述。 預設值是 False。 如需詳細資訊，請參閱 [CREATE PARTITION SCHEME (TRANSACT-SQL)](https://msdn.microsoft.com/5b21c53a-b4f4-4988-89a2-801f512126e4)。  
  
**編寫主索引鍵的指令碼**  
將 [主要及外部索引鍵條件約束](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 加入指令碼。 預設值是 True。  
  
**編寫統計資料的指令碼**  
在指令碼中加入使用者自訂統計資料。 預設值是 False。 如需詳細資訊，請參閱 [CREATE STATISTICS (TRANSACT-SQL)](https://msdn.microsoft.com/b23e2f6b-076c-4e6d-9281-764bdb616ad2)。  
  
**編寫觸發程序的指令碼**  
在指令碼中加入觸發程序。 預設值是 False。 如需詳細資訊，請參閱 [CREATE TRIGGER (TRANSACT-SQL)](https://msdn.microsoft.com/edeced03-decd-44c3-8c74-2c02f801d3e7)。  
  
**編寫唯一索引鍵的指令碼**  
將 [Unique 條件約束及 Check 條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 加入指令碼。 預設值是 False。  
  
**編寫檢視資料行的指令碼**  
在檢視標頭中宣告檢視資料行。 預設值是 False。 如需詳細資訊，請參閱 [CREATE VIEW (TRANSACT-SQL)](https://msdn.microsoft.com/aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9)。  
  
**包含 dri 系統名稱**  
加入系統產生的條件約束名稱，以便強制執行宣告式參考完整性。 預設值是 False。 如需詳細資訊，請參閱 [REFERENTIAL_CONSTRAINTS (TRANSACT-SQL)](https://msdn.microsoft.com/5d358f18-0a85-4b55-af4b-98d5f4cd1020)。  
  
### <a name="version-options"></a>版本選項

**使指令碼設定與來源相符**：如果已啟用目標版本，所產生指令碼的引擎版本和引擎類型將會設定為編寫物件指令碼之伺服器的值。 這會停用 (並忽略) 其他版本選項。 

**資料庫引擎版本的指令碼**：所指定的[引擎版本](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.edition.aspx)將會以所產生的指令碼為目標。

**資料庫引擎類型的指令碼**：所指定的[資料庫引擎類型](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.databaseenginetype.aspx)將會以所產生的指令碼為目標。

**針對伺服器版本編寫指令碼**  
所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本將會以所產生的指令碼為目標。 無法針對較舊的版本編寫 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 新增功能的指令碼。 有一些為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 所建立的指令碼，無法在執行舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的伺服器上執行，也無法在 [資料庫相容性層級設定](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)資料庫上執行。  

## <a name="see-also"></a>另請參閱  
[產生指令碼 (SQL Server Management Studio)](https://msdn.microsoft.com/9711c617-3c68-4e5a-aea3-befc64d51524)  
  
