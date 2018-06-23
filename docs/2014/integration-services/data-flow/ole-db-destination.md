---
title: OLE DB 目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.oledbdest.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
caps.latest.revision: 77
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5ead833d28c31a1c34da1ce6e2182cbaa418f156
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031265"
---
# <a name="ole-db-destination"></a>OLE DB 目的地
  OLE DB 目的地會使用資料庫的資料表、檢視或 SQL 命令將資料載入各種符合 OLE DB 標準的資料庫。 例如，OLE DB 來源可以將資料載入至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料表中。  
  
> [!NOTE]  
>  如果資料來源為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，則資料來源需要舊版 Excel 以外的連線管理員。 如需詳細資訊，請參閱 [連接至 Excel 活頁簿](../connection-manager/connect-to-an-excel-workbook.md)。  
  
 OLE DB 目的地提供用於載入資料的五種不同資料存取模式：  
  
-   資料表或檢視。 您可以指定現有的資料表或檢視，或者建立新資料表。  
  
-   使用快速載入選項的資料表或檢視。 您可以指定現有的資料表，也可以新建資料表。  
  
-   在變數中指定的資料表或檢視。  
  
-   在變數中指定之使用快速載入選項的資料表或檢視。  
  
-   SQL 陳述式的結果。  
  
> [!NOTE]  
>  OLE DB 目的地不支援參數。 如果需要執行參數化 INSERT 陳述式，請考慮 OLE DB 命令轉換。 如需相關資訊，請參閱 [OLE DB Command Transformation](transformations/ole-db-command-transformation.md)。  
  
 當 OLE DB 目的地載入使用雙位元組字元集 (DBCS) 的資料時，如果資料存取模式未使用快速載入選項，而 OLE DB 連接管理員使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB)，則資料可能會損毀。 若要確定 DBCS 資料的完整性，您應該將 OLE DB 連線管理員設定為使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，或使用下列其中一個快速載入存取模式：[資料表或檢視表 - 快速載入] 或 [資料表名稱或檢視名稱變數 - 快速載入]。 兩個選項都可從 [OLE DB 目的地編輯器] 對話方塊使用。 程式設計時[!INCLUDE[ssIS](../../includes/ssis-md.md)]物件模型中，您應該將 AccessMode 屬性設`OpenRowset Using FastLoad`，或`OpenRowset Using FastLoad From Variable`。  
  
> [!NOTE]  
>  如果使用「[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中的 [OLE DB 目的地編輯器] 對話方塊來建立 OLE DB 目的地插入資料的目的地資料表，則您可能必須手動選取新建立的資料表。 當 OLE DB 提供者 (例如 DB2 的 OLE DB 提供者) 自動將結構描述識別碼加入資料表名稱時，需進行手動選取。  
  
> [!NOTE]  
>  視目的地類型而定，[OLE DB 目的地編輯器] 對話方塊產生的 CREATE TABLE 陳述式可能需要進行修改。 例如，某些目的地並不支援 CREATE TABLE 陳述式所使用的資料類型。  
  
 此目的地使用 OLE DB 連接管理員連接到資料來源，且連接管理員會指定要使用的 OLE DB 提供者。 如需相關資訊，請參閱 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案亦提供您建立 OLE DB 連線管理員所在的資料來源物件，讓 OLE DB 目的地使用資料來源和資料來源檢視。  
  
 OLE DB 目的地包含輸入資料行與目的地資料來源中資料行之間的對應。 您不一定要將輸入資料行對應到所有目的地資料行，但因目的地資料行屬性的不同，如果輸入資料行未對應到目的地資料行，則可能發生錯誤。 例如，如果目的地資料行不允許 Null 值，則輸入資料行必須對應到該資料行。 此外，對應之資料行的資料類型必須相容。 例如，您不能將字串資料類型的輸入資料行對應到數值資料類型的目的地資料行。  
  
 OLE DB 目的地具有一個規則輸入和一個錯誤輸出。  
  
 如需有關資料類型的詳細資訊，請參閱＜ [Integration Services Data Types](integration-services-data-types.md)＞。  
  
## <a name="fast-load-options"></a>快速載入選項  
 如果 OLE DB 目的地使用快速載入資料存取模式，則您可以在 **OLE DB 目的地編輯器**這個使用者介面中為目的地指定下列快速載入選項：  
  
-   保留匯入資料檔中的識別值或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指派的唯一值。  
  
-   大量載入作業期間保留 Null 值。  
  
-   大量匯入作業期間檢查目標資料表或檢視的條件約束。  
  
-   大量載入作業期間需要資料表層級鎖定。  
  
-   指定批次中的資料列數目以及認可大小。  
  
 部分快速載入選項儲存在 OLE DB 目的地的特定屬性中。 例如，FastLoadKeepIdentity 指定是否要保留識別值、FastLoadKeepNulls 指定是否要保留 Null 值，而 FastLoadMaxInsertCommitSize 則指定要認可為批次的資料列數目。 其他快速載入選項儲存在 FastLoadOptions 屬性的逗號分隔清單中。 如果 OLE DB 目的地使用，都儲存在 FastLoadOptions 中所列的所有快速載入選項**OLE DB 目的地編輯器**對話方塊中，屬性的值設定為`TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000`。 1000 值代表目的地設定為使用 1000 列的批次。  
  
> [!NOTE]  
>  目的地的任何條件約束失敗都會使 FastLoadMaxInsertCommitSize 所定義的整個資料列批次失敗。  
  
 除了 [OLE DB 目的地編輯器] 對話方塊中公開的快速載入選項以外，您還可以在 [進階編輯器] 對話方塊的 FastLoadOptions 屬性中輸入選項，將 OLE DB 目的地設定為使用下列大量載入選項。  
  
|快速載入選項|描述|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|指定要插入的大小 (以 KB 為單位)。 這個選項沒有表單`KILOBYTES_PER_BATCH`  = \<正整數值**>**。|  
|FIRE_TRIGGERS|指定是否要針對插入資料表上引發觸發程序。 選項的格式為 **FIRE_TRIGGERS**。 選項的存在代表觸發程序會引發。|  
|ORDER|指定如何儲存輸入資料。 選項的格式為 ORDER \<資料行名稱> ASC&#124;DESC。 可以列出任何數目的資料行，也可以選擇包含排序順序。 如果省略排序順序，大量插入作業會假設資料沒有排序。<br /><br /> 注意：如果您使用 ORDER 選項依照資料表的叢集索引排序輸入資料，將可改善效能。|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 關鍵字通常是以大寫字母輸入，但是這些關鍵字並不區分大小寫。  
  
 若要深入了解有關快速載入選項的詳細資訊，請參閱 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)。  
  
## <a name="troubleshooting-the-ole-db-destination"></a>疑難排解 OLE DB 目的地  
 您可以記錄 OLE DB 目的地對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，針對 OLE DB 目的地所執行的將資料儲存至外部資料來源的作業進行疑難排解。 若要記錄 OLE DB 目的地對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱[封裝執行的疑難排解工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ole-db-destination"></a>設定 OLE DB 目的地  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在 [OLE DB 目的地編輯器] 對話方塊中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [OLE DB 目的地編輯器&#40;連接管理員頁面&#41;](../ole-db-destination-editor-connection-manager-page.md)  
  
-   [OLE DB 目的地編輯器&#40;[對應] 頁面&#41;](../ole-db-destination-editor-mappings-page.md)  
  
-   [OLE DB 目的地編輯器&#40;錯誤輸出頁面&#41;](../ole-db-destination-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [Common Properties](../common-properties.md)  
  
-   [OLE DB 自訂屬性](ole-db-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用 OLE DB 目的地來載入資料](ole-db-destination.md)  
  
-   [設定資料流程元件的屬性](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
 [OLE DB 來源](ole-db-source.md)  
  
 [Integration Services &#40;SSIS&#41;變數](../integration-services-ssis-variables.md)  
  
 [資料流程](data-flow.md)  
  
  
