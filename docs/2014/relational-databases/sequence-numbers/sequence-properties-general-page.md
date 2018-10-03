---
title: 順序屬性 (一般頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sequence.general.f1
ms.assetid: 0187f413-cdf0-48a2-b2e6-9b3578cd5811
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54a6d265c6ad8f7c585a629c2adc997b808d636b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063240"
---
# <a name="sequence-properties-general-page"></a>順序屬性 (一般頁面)
  建立順序物件，並指定其屬性。 序列是使用者定義之結構描述繫結的物件，該物件會根據建立序列所使用的規格產生一連串的數值。 數值序列會在定義的間隔依照遞增或遞減順序來產生，而且在用完時可設定為重新啟動 (循環)。 順序不會與特定資料表產生關聯，與識別欄位不同。 應用程式會參考順序物件，以擷取它的下一個值。 順序與資料表之間的關聯性是由應用程式所控制。 使用者的應用程式可以參考序列物件，並協調跨越多個資料列和資料表的值。  
  
 不同於插入時產生的識別資料行值，應用程式可以藉由呼叫 [NEXT VALUE FOR 函數](/sql/t-sql/functions/next-value-for-transact-sql)取得下一個序數，而不需要插入資料列。 您可以使用 [sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql) 一次取得多個序號。  
  
 如需使用 **CREATE SEQUENCE** 和 **NEXT VALUE FOR** 函數的相關資訊和案例，請參閱[序號](sequence-numbers.md)。  
  
 此頁面可經由兩種方式存取：以滑鼠右鍵按一下 [物件總管] 中的 [順序]，然後按一下 [新增順序]，或者以滑鼠右鍵按一下現有的順序，然後按一下 [屬性]。 以滑鼠右鍵按一下現有的順序，然後按一下 [屬性] 時，無法編輯選項。 若要變更順序選項，請使用 [ALTER SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-sequence-transact-sql) 陳述式或卸除然後重新建立順序物件。  
  
## <a name="options"></a>選項。  
 **順序名稱**  
 在此處輸入順序名稱。  
  
 **順序結構描述**  
 指定將擁有此順序的結構描述。  
  
 **資料類型**  
 順序可以定義為任何整數類型。 這包括：  
  
|資料類型|範圍|  
|---------------|-----------|  
|`tinyint`|0 至 255|  
|`smallint`|-32,768 至 32,767|  
|`int`|-2,147,483,648 至 2,147,483,647|  
|`bigint`|-9,223,372,036,854,775,808 至 9,223,372,036,854,775,807|  
  
-   `decimal` 或小數位數為 0 的 `numeric`。  
  
-   以這些類型之一為基礎的任何使用者定義的資料類型 (別名類型)。  
  
 **有效位數**  
 如果是 `decimal` 或 `numeric` 資料類型，請指定有效位數  (小數位數一定是 0)。  
  
 **開始值**  
 順序物件會傳回的第一個值。 **START** 值必須是小於或等於順序物件的最大值，而且大於或等於最小值。 新順序物件的預設開始值是遞增順序物件的最小值，是遞減順序物件的最大值。  
  
 **遞增量**  
 每次呼叫 **NEXT VALUE FOR** 函數時，用來遞增順序物件值的值 (如果是負數則遞減)。 如果增量是負值，則會遞減順序物件，否則會遞增。 增量不能為 0。  
  
 **最小值**  
 指定順序物件的界限。 新序列物件的預設最小值是序列物件之資料類型的最小值。 這是零`tinyint`資料型別和所有其他資料類型為負數。  
  
 **最大值**  
 指定順序物件的界限。 新序列物件的預設最大值是序列物件之資料類型的最大值。  
  
 **在達到限制時循環順序將會重新啟動**  
 選取以允許當超出其最小值或最大值時，順序物件從最小值 (或是遞減順序物件的最大值) 重新啟動。  
  
> [!NOTE]  
>  循環並不會從開始值重新啟動，而是從最小值/最大值重新啟動。  
  
 **快取選項**  
 建立順序值的快取，可藉由減少建立序號所需的磁碟 IO 數目，對使用順序物件的應用程式提升效能。  
  
-   預設快取大小 - [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會選取大小，但是使用者不應該依賴此選取來取得一致的結果。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 可能變更計算快取大小的方法，而不另行通知。  
  
-   無快取 - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會快取序號。  
  
-   快取與大小 - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會快取順序值。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會追蹤目前值，以及留在快取中的值數目。 因此，儲存快取所需的記憶體數量永遠是順序物件之資料類型的兩個執行個體。  
  
 以 CACHE 選項建立時，非預期關閉 (例如停電) 可能會失去快取中的序號。  
  
 如需有關建立順序選項的詳細資訊，請參閱 [CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql)。  
  
## <a name="permissions"></a>Permissions  
 需要 SCHEMA 的 **CREATE SEQUENCE**、 **ALTER**或 **CONTROL** 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.sequences &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sequences-transact-sql)  
  
  
