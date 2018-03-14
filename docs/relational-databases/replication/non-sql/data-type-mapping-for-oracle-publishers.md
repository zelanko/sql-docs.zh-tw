---
title: "Oracle 發行者的資料類型對應 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: 6da0e4f4-f252-4b7e-ba60-d2e912aa278e
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 241e3a775bc00fbd1d8c9a773a75c9cf25138ae2
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="data-type-mapping-for-oracle-publishers"></a>Oracle 發行者的資料類型對應
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle 資料類型與 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料類型並非始終完全相符。 若有可能，將在發行 Oracle 資料表時自動選取相符的資料類型。 如果單一資料類型對應不清楚，將提供替代的資料類型對應。 如需有關如何選取替代對應的詳細資訊，請參閱本主題稍後的「指定替代資料類型對應」一節。  
  
 下表顯示了將資料從「Oracle 發行者」移至「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」時，資料類型在 Oracle 與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之間的預設對應方式。 「替代方案」一欄會指示替代對應是否可用。  
  
|Oracle 資料類型|SQL Server 資料類型|替代方案|  
|----------------------|--------------------------|------------------|  
|BFILE|VARBINARY(MAX)|是|  
|BLOB|VARBINARY(MAX)|是|  
|CHAR([1-2000])|CHAR([1-2000])|是|  
|CLOB|VARCHAR(MAX)|是|  
|DATE|DATETIME|是|  
|FLOAT|FLOAT|否|  
|FLOAT([1-53])|FLOAT([1-53])|否|  
|FLOAT([54-126])|FLOAT|否|  
|INT|NUMERIC(38)|是|  
|INTERVAL|DATETIME|是|  
|LONG|VARCHAR(MAX)|是|  
|LONG RAW|IMAGE|是|  
|NCHAR([1-1000])|NCHAR([1-1000])|否|  
|NCLOB|NVARCHAR(MAX)|是|  
|NUMBER|FLOAT|是|  
|NUMBER([1-38])|NUMERIC([1-38])|否|  
|NUMBER([0-38],[1-38])|NUMERIC([0-38],[1-38])|是|  
|NVARCHAR2([1-2000])|NVARCHAR([1-2000])|否|  
|RAW([1-2000])|VARBINARY([1-2000])|否|  
|real|FLOAT|否|  
|ROWID|CHAR(18)|否|  
|TIMESTAMP|DATETIME|是|  
|TIMESTAMP(0-7)|DATETIME|是|  
|TIMESTAMP(8-9)|DATETIME|是|  
|TIMESTAMP(0-7) WITH TIME ZONE|VARCHAR(37)|是|  
|TIMESTAMP(8-9) WITH TIME ZONE|VARCHAR(37)|否|  
|TIMESTAMP(0-7) WITH LOCAL TIME ZONE|VARCHAR(37)|是|  
|TIMESTAMP(8-9) WITH LOCAL TIME ZONE|VARCHAR(37)|否|  
|UROWID|CHAR(18)|否|  
|VARCHAR2([1-4000])|VARCHAR([1-4000])|是|  
  
## <a name="considerations-for-data-type-mapping"></a>資料類型對應的考量  
 從 Oracle 資料庫複寫資料時，注意下列資料類型問題。  
  
### <a name="unsupported-data-types"></a>不支援的資料類型  
 下列資料類型不受支援；無法複寫具有這些類型的資料行：  
  
-   物件類型  
  
-   XML 類型  
  
-   Varrays  
  
-   巢狀資料表  
  
-   使用 REF 的資料行  
  
### <a name="the-date-data-type"></a>DATE 資料類型  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的日期範圍是從 1753 A.D. 到 9999 A.D.，而 Oracle 的日期範圍則是從 4712 B.C. 到 4712 A.D. 如果 DATE 類型的資料行包含的值超出 SQL Server 的範圍，請為此資料行選取替代資料類型，也就是 VARCHAR(19)。  
  
### <a name="float-and-number-types"></a>FLOAT 和 NUMBER 類型  
 在對應 FLOAT 和 NUMBER 資料類型期間指定的小數位數與有效位數，取決於為使用 Oracle 資料庫中資料類型的資料行指定的小數位數與有效位數。 位數 (Precision) 是指數字中總共的位數。 小數位數 (Scale) 則是指數字中小數點右方的位數。 例如 123.45 的位數是 5，小數位數是 2。  
  
 Oracle 允許將數字定義為小數位數大於有效位數，例如 NUMBER(4,5)，但 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 需要有效位數等於或大於小數位數。 若要確定沒有資料截斷，如果「Oracle 發行者」端的小數位數大於有效位數，則在對應資料類型時要將有效位數設定為等於小數位數：NUMBER(4,5) 將對應為 NUMERIC(5,5)。  
  
> [!NOTE]  
>  如果您沒有為 NUMBER 指定小數位數和有效位數，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設為使用最大小數位數 (8) 和有效位數 (38)。 建議您在 Oracle 中設定特定的小數位數和有效位數，以便在複寫資料時獲得更好的儲存容量和效能。  
  
### <a name="large-object-types"></a>大型物件類型  
 Oracle 最多支援 4 GB，而 SQL Server 最多支援 2 GB。 超過 2 GB 的複寫資料將被截斷。  
  
 如果 Oracle 資料表包含 BFILE 資料行，該資料行的資料將儲存在檔案系統中。 複寫管理使用者帳戶必須被授與目錄存取權限。在該目錄中，資料使用下列語法儲存：  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 如需大型物件類型的詳細資訊，請參閱 [Oracle 發行者的設計考量與限制](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)中的＜大型物件的考量＞一節。  
  
## <a name="specifying-alternative-data-type-mappings"></a>指定替代資料類型對應  
 通常適合使用預設的資料類型對應，但對於許多 Oracle 資料類型，您可以從一組替代對應中選取資料類型對應，而不使用預設對應。 可透過兩種方式指定替代對應：  
  
-   使用預存程序或「新增發行集精靈」覆寫各發行項的預設值。  
  
-   使用預存程序對所有未來發行項的預設值進行全域變更 (不變更現有發行項的預設值)。  
  
 若要指定替代資料類型對應，請參閱＜ [Specify Data Type Mappings for an Oracle Publisher](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 發行者的設計考量與限制](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
