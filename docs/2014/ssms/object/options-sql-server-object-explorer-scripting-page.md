---
title: 選項（SQL Server 物件總管-腳本頁面） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 81e4bafbd596894a8cecbeb707a5d8be698c1f3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63031932"
---
# <a name="options-sql-server-object-explorer-scripting-page"></a>選項（SQL Server 物件總管-腳本頁面）
  使用此頁面設定指定碼選項，以在**物件總管**之物件操作功能表的下列命令中使用：  
  
-   使用者資料表與檢視的 [編輯]  命令。  
  
-   **腳本\<物件> 做**為使用者建立之物件的命令。  
  
-   使用者建立之物件的 [修改]  命令。  
  
-   此頁面也可設定 [產生 SQL Server 指令碼精靈]  的編寫指令碼選項預設值。  
  
## <a name="remarks"></a>備註  
 [**編輯**] 和 [**修改**] 命令可能會產生與相同選項設定的 [ ** \<腳本物件>** ] 命令不同的結果。 [編輯]  與 [修改]  命令的設計讓您可以在查詢編輯器工作階段期間，修改目前資料庫中的物件。 **Script \<物件> as**命令的設計是用來產生腳本，以便稍後用來建立物件。  
  
## <a name="options"></a>選項。  
 在每個選項右方的清單中選取可用的設定，即可指定指令碼選項。  
  
### <a name="general-scripting-options"></a>一般指令碼選項  
 **分隔個別陳述式**  
 使用批次分隔符號來分隔個別 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 若要變更**查詢編輯器**的預設批次分隔符號，請選取 工具  /選項  /查詢執行  /SQL Server  /一般  /批次分隔符號  。 預設值是 False。 如需詳細資訊，請參閱[GO &#40;transact-sql&#41;](/sql/t-sql/language-elements/sql-server-utilities-statements-go)。  
  
 **包含描述性標頭**  
 透過將每個物件的指令碼分隔成區段，在指令碼中加入描述性註解。 預設值是 True。 如需詳細資訊，請參閱[Comment &#40;transact-sql&#41;](/sql/t-sql/language-elements/comment-transact-sql)。  
  
 **包含 vardecimal 選項**  
 加入 Vardecimal 儲存選項。 預設值是 False。 如需詳細資訊，請參閱和[sp_db_vardecimal_storage_format &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql)。  
  
 **編寫變更追蹤的指令碼**  
 在指令碼中包含變更追蹤資訊。  
  
 **針對伺服器版本編寫指令碼**  
 建立可以在選取的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]版本上執行的指令碼。 無法針對較舊的版本編寫 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 新增功能的指令碼。 有一些為 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 所建立的指令碼，無法在執行舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的伺服器上執行，也無法在 [資料庫相容性層級設定](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)資料庫上執行。  
  
 **編寫全文檢索目錄的指令碼**  
 加入全文檢索目錄的指令碼。 預設值是 False。 如需詳細資訊，請參閱[&#40;transact-sql&#41;建立全文檢索目錄](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)。  
  
 **腳本使用\<資料庫>**  
 將 USE DATABASE 陳述式新增到指令碼中，可在目前的 **物件總管** 資料庫內容中建立資料庫物件。 如果預期指令碼會用於不同的資料庫，請選取 False 省略。 預設值是 True。 如需詳細資訊，請參閱 [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)。  
  
### <a name="object-scripting-options"></a>物件指令碼選項  
 **產生相依物件的指令碼**  
 針對執行選取物件之指令碼時所需的其他物件，產生指令碼。 預設值是 False。  
  
 **包含 If NOT EXISTS 子句**  
 加入陳述式，以便檢查每個物件是否都不存在資料庫中，然後再嘗試建立物件。 預設值是 False。 如需詳細資訊，請參閱[IF .。。或者，&#40;Transact-sql&#41;](/sql/t-sql/language-elements/if-else-transact-sql)和[EXISTS &#40;transact-sql&#41;](/sql/t-sql/language-elements/exists-transact-sql)。  
  
 **結構描述會限定物件名稱**  
 使用物件結構描述來限定物件名稱。 預設值是 False。 如需詳細資訊，請參閱 [建立資料庫結構描述](../../relational-databases/security/authentication-access/create-a-database-schema.md)。  
  
 **編寫擴充屬性的指令碼**  
 當物件具有擴充屬性時，在指令碼中包含擴充屬性。 預設值是 False。 如需詳細資訊，請參閱 [sp_addextendedproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql)。  
  
 **編寫擁有者的指令碼**  
 將擁有者包括在產生的指令碼中。 預設值是 False。  
  
 **編寫權限的指令碼**  
 在指令碼中加入資料庫物件的權限。 預設值是 True。 如需詳細資訊，請參閱[許可權 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)。  
  
### <a name="tableview-options"></a>資料表/檢視選項  
 下列選項只適用於資料表或檢視的指令碼。  
  
 **將使用者自訂資料類型轉換成基底類型**  
 將使用者自訂資料類型轉換成用以建立這些資料類型的基底類型。 當來源資料庫使用者自訂資料類型不存在於執行指令碼的資料庫時，請使用 True。 請使用 False 來保留使用者自訂資料類型。 預設值是 False。 如需詳細資訊，請參閱[CREATE TYPE &#40;transact-sql&#41;](/sql/t-sql/statements/create-type-transact-sql)。  
  
 **產生 SET ANSI PADDING 命令**  
 在每個 CREATE TABLE 陳述式前後加入 SET ANSI_PADDING 陳述式。 預設值是 True。 如需詳細資訊，請參閱 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)。  
  
 **包含定序**  
 在資料行定義中加入定序。 預設值是 True。 如需詳細資訊，請參閱 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
 **包含 IDENTITY 屬性**  
 加入 IDENTITY 種子和 IDENTITY 遞增的定義。 預設值是 True。 如需詳細資訊，請參閱 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)。  
  
 **結構描述會限定外部索引鍵參考**  
 在 FOREIGN KEY 條件約束的資料表參考中加入結構描述名稱。 預設值是 True。  
  
 **編寫繫結預設值和規則的指令碼**  
 加入 **sp_bindefault** 及 **sp_bindrule** 繫結預存程序呼叫。 預設值是 True。 如需詳細資訊，請參閱[sp_bindefault &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-bindefault-transact-sql)和[sp_bindrule &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-bindrule-transact-sql)。  
  
 **編寫 CHECK 條件約束的指令碼**  
 將 [CHECK 條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 指令碼。 預設值是 True。  
  
 **編寫預設值的指令碼**  
 在指令碼中加入資料行預設值。 預設值是 False。 如需詳細資訊，請參閱 [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql)。  
  
 **編寫檔案群組的指令碼**  
 在資料表定義的 ON 子句中指定檔案群組。 預設值是 False。 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)。  
  
 **編寫外部索引鍵的指令碼**  
 將 [FOREIGN KEY 條件約束](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 加入指令碼。 預設值是 False。  
  
 **編寫全文檢索索引的指令碼**  
 在指令碼中加入全文檢索索引。 預設值是 False。 如需詳細資訊，請參閱[CREATE 全文檢索索引 &#40;transact-sql&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)。  
  
 **編寫索引的指令碼**  
 在指令碼中加入叢集、非叢集和 XML 索引。 預設值是 True。 如需詳細資訊，請參閱 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
 **編寫分割區結構描述的指令碼**  
 在指令碼中加入資料表分割區結構描述。 預設值是 False。 如需詳細資訊，請參閱[&#40;transact-sql&#41;建立分割區配置](/sql/t-sql/statements/create-partition-scheme-transact-sql)。  
  
 **編寫主索引鍵的指令碼**  
 將 [主要及外部索引鍵條件約束](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 加入指令碼。 預設值是 True。  
  
 **編寫統計資料的指令碼**  
 在指令碼中加入使用者自訂統計資料。 預設值是 False。 如需詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
 **編寫觸發程序的指令碼**  
 在指令碼中加入觸發程序。 預設值是 False。 如需詳細資訊，請參閱 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)。  
  
 **編寫唯一索引鍵的指令碼**  
 將 [Unique 條件約束及 Check 條件約束](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 加入指令碼。 預設值是 False。  
  
 **編寫檢視資料行的指令碼**  
 在檢視標頭中宣告檢視資料行。 預設值是 False。 如需詳細資訊，請參閱 [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)。  
  
 **ScriptDriIncludeSystemNames**  
 加入系統產生的條件約束名稱，以便強制執行宣告式參考完整性。 預設值是 False。 如需詳細資訊，請參閱[REFERENTIAL_CONSTRAINTS &#40;transact-sql&#41;](/sql/relational-databases/system-information-schema-views/referential-constraints-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [產生指令碼 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)  
  
  
