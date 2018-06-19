---
title: 將變更套用到目的地 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],applying changes
ms.assetid: 338a56db-cb14-4784-a692-468eabd30f41
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8450e3aa348b3474e3ed5359c799675e8c34c3af
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408570"
---
# <a name="apply-the-changes-to-the-destination"></a>將變更套用到目的地
  在執行累加式變更資料載入之 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中，第三個工作，也就是最後一個工作是將變更套用到您的目的地。 您將需要一個元件來套用插入、一個元件來套用更新，以及一個元件來套用刪除。  
  
> [!NOTE]  
>  在設計可執行累加式變更資料載入的資料流程時，第二個工作是分隔插入、更新與刪除。 如需此元件的詳細資訊，請參閱[處理插入、更新與刪除](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md)。 如需建立可執行累加式變更資料載入之封裝的完整程序描述，請參閱[變更資料擷取 &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)。  
  
## <a name="applying-inserts"></a>套用插入  
 若要套用插入，您可以使用 OLE DB 目的地，因為新的資料列不需要任何特殊處理。  
  
#### <a name="to-process-inserts-by-using-an-ole-db-destination"></a>使用 OLE DB 目的地來處理插入  
  
1.  在 **[資料流程]** 索引標籤上，加入 OLE DB 目的地。  
  
2.  將包含插入的輸出從「條件式分割」轉換連接到 OLE DB 目的地。  
  
3.  在 **[OLE DB 目的地編輯器]** 的 **[連接管理員]** 頁面上，選取下列選項：  
  
    1.  針對目的地資料庫選取或建立 OLE DB 連接管理員。  
  
    2.  選取 **[資料存取模式]** 選項，然後選取目的地資料表，或輸入包含目的地資料行的 SQL 陳述式。  
  
4.  在編輯器的 **[對應]** 頁面上，將適當的資料行從變更資料對應到目的地資料表。  
  
## <a name="applying-updates"></a>套用更新  
 若要套用更新，您可以使用「OLE DB 命令」轉換。 您必須使用參數化的 UPDATE 陳述式，一次更新一個具有新資料行值的資料列，因此您可以使用這個轉換。  
  
> [!NOTE]  
>  您也可以使用目的地元件套用更新。 使用這個方式時，您可以使用目的地元件，將資料列儲存到針對此用途所建立的暫存資料表。 接著，您可以使用「執行 SQL」工作，根據暫存資料表的目的地，執行大量更新與大量刪除作業。  
  
#### <a name="to-process-updates-by-using-an-ole-db-command-transformation"></a>使用 OLE DB 命令轉換處理更新  
  
1.  在 **[資料流程]** 索引標籤上，加入「OLE DB 命令」轉換。  
  
2.  將包含更新的輸出從「條件式分割」轉換連接到「OLE DB 命令」轉換。  
  
3.  在 **[OLE DB 命令的進階編輯器]** 的 **[連接管理員]** 索引標籤上，選取或建立目的地資料庫的 OLE DB 連接管理員。  
  
4.  在 **[OLE DB 命令的進階編輯器]** 的 **[元件屬性]** 索引標籤上，為 **SqlCommand**輸入一個參數化的 UPDATE 陳述式。  
  
     例如，用於 Customer 資料表的 UPDATE 陳述式語法可能如下：  
  
    ```sql
    update CDCSample.Customer  
    set TerritoryID  = ?,  
        CustomerType  = ?,  
        rowguid  = ?,  
        ModifiedDate  = ?  
    where CustomerID = ?  
  
    ```  
  
5.  在編輯器的 **[資料行對應]** 索引標籤上，將適當的資料行從變更資料對應到 UPDATE 陳述式中的參數。  
  
## <a name="applying-deletes"></a>套用刪除  
 若要套用刪除，您可以使用「OLE DB 命令」轉換。 您必須使用參數化的 DELETE 陳述式，根據唯一識別資料列的資料行值，一次刪除單一資料列，因此您可以使用這個轉換。  
  
> [!NOTE]  
>  您也可以使用目的地元件套用刪除。 使用這個方式時，您可以使用目的地元件，將資料列儲存到針對此用途所建立的暫存資料表。 接著，您可以使用「執行 SQL」工作，根據暫存資料表的目的地，執行大量更新與大量刪除作業。  
  
#### <a name="to-process-deletes-by-using-an-ole-db-command-transformation"></a>使用 OLE DB 命令轉換處理刪除  
  
1.  在 **[資料流程]** 索引標籤上，將「OLE DB 命令」轉換加入到資料流程。  
  
2.  將包含刪除的輸出從「條件式分割」轉換連接到「OLE DB 命令」轉換。  
  
3.  開啟 [進階編輯器] 來設定轉換。  
  
4.  在 **[OLE DB 命令的進階編輯器]** 的 **[連接管理員]** 索引標籤上，選取或建立目的地資料庫的 OLE DB 連接管理員。  
  
5.  在 **[OLE DB 命令的進階編輯器]** 的 **[元件屬性]** 索引標籤上，為 **SqlCommand**輸入一個參數化的 DELETE 陳述式。  
  
     例如，用於 Customer 資料表的 DELETE 陳述式語法可能如下：  
  
    ```sql
    delete from Customer where CustomerID = ?  
  
    ```  
  
6.  在編輯器的 **[資料行對應]** 索引標籤上，將適當的資料行從變更資料對應到 DELETE 陳述式中的參數。  
  
## <a name="optimizing-inserts-and-updates-by-using-merge-functionality"></a>使用 MERGE 功能最佳化插入和更新  
 您可以結合特定的異動資料擷取選項與 Transact-SQL MERGE 關鍵字的使用，將插入和更新的處理最佳化。 如需 MERGE 關鍵字的詳細資訊，請參閱 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)。  
  
 當您呼叫 **cdc.fn_cdc_get_net_changes_<capture_instance>** 函數時，您可以在擷取變更資料的 Transact-SQL 陳述式中，指定 *all with merge* 作為 *row_filter_option* 參數的值。 當這個異動資料擷取函數不必執行區別插入與更新所需的額外處理時，其運作會更有效率。 當您指定 *all with merge* 參數值時，變更資料的 **__$operation** 值為 1 (針對刪除) 或 5 (針對插入或更新所造成的變更)。 如需用於擷取變更資料之 Transact-SQL 函數的詳細資訊，請參閱 [擷取與了解變更資料](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)。利用 *all with merge* 參數值擷取變更後，您可以套用刪除，並將剩餘的資料列輸出到暫存資料表或臨時資料表。 接著，在下游的「執行 SQL」工作中，您可以使用單一 MERGE 陳述式，將所有插入或更新從臨時資料表套用到目的地。  
  
  
