---
title: 如何：比較和同步處理兩個資料庫的資料 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.datacompare.connection.datasources.f1
- sql.data.tools.datacompare.watermark.f1
- sql.data.tools.datacompare.connection.objectselection.f1
ms.assetid: 2148e517-ed42-41c6-b753-1ac625f594c8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0d7654d02cfc35b0dfbaa82b100b9a82a8edacb0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929472"
---
# <a name="how-to-compare-and-synchronize-the-data-of-two-databases"></a>如何：比較和同步處理兩個資料庫的資料
您可以比較兩個資料庫包含的資料。 要比較的資料庫稱為「來源」  和「目標」  。  
  
> [!NOTE]  
> 「資料庫專案」  和 .dacpac 或 .bacpac 套件不能是資料比較的來源或目標。  
  
當比較資料時，會產生「資料操作語言」  (DML) 指令碼。您可以使用這個指令碼來更新目標資料庫中的某些或所有資料，以同步處理不同的資料庫。 當資料比較完成時，其結果會出現在 Visual Studio 的 [資料比較] 視窗中。  
  
在比較完成之後，您可以採取其他步驟：  
  
-   您可以檢視兩個資料庫之間的差異。 如需詳細資訊，請參閱[檢視資料差異](#ViewDifferences)。  
  
-   您可以更新目標的全部或部分以符合來源。 如需詳細資訊，請參閱[同步處理資料庫資料](#Synchronize)。  
  
如需詳細資訊，請參閱[使用參考資料庫中的資料比較和同步處理一個或多個資料表中的資料](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)。  
  
> [!NOTE]  
> 您也可以比較兩個資料庫或相同資料庫兩個版本的「結構描述」  。 如需詳細資訊，請參閱[如何：使用結構描述比較以比較不同的資料庫定義](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)。  
  
## <a name="CompareDatabaseData"></a>比較資料庫資料  
  
#### <a name="to-compare-data-by-using-the-new-data-comparison-wizard"></a>若要使用新增資料比較精靈來比較資料  
  
1.  指向 [SQL]  功能表上的 [資料比較]  ，然後按一下 [新增資料比較]  。  
  
    [新增資料比較] 精靈隨即出現。 此外，也會開啟 [資料比較] 視窗，且 Visual Studio 會自動為其指派 DataCompare1 之類的名稱。  
  
2.  識別來源和目標資料庫。  
  
    如果 [來源資料庫]  清單或 [目標資料庫]  清單是空的，請按一下 [新增連接]  。 在 [連接屬性]  對話方塊中，識別資料庫所在的伺服器以及當連接到資料庫時使用的驗證類型。 然後按一下 [確定]  以關閉 [連接屬性]  對話方塊並返回 [資料比較] 精靈。  
  
    在 [資料比較] 精靈的第一頁，確認每個資料庫的資訊正確、指定哪些記錄要包含在結果中，然後按一下 [下一步]  。 [資料比較] 精靈的第二頁會出現，並顯示資料庫中資料表和檢視表的階層式清單。  
  
3.  針對您要比較之資料表和檢視表選取核取方塊。 選擇性地展開資料庫物件的節點，針對這些物件內您要比較的資料行選取核取方塊。  
  
    > [!NOTE]  
    > 資料表和檢視表必須符合兩個準則才會出現在清單中。 首先，在來源和目標資料庫之間物件的結構描述必須符合。 其次，具有主索引鍵、唯一索引鍵、唯一索引或唯一條件約束的資料表和檢視表才會出現在清單中。 如果資料表或檢視表不符合這兩個準則，清單會是空白。  
  
4.  如果有多個索引鍵存在，您可以使用 [比較索引鍵]  資料行，以指定資料比較所依據的索引鍵。 例如，您可以指定比較所依據的是主索引鍵資料行還是另一個 (可唯一識別的) 索引鍵資料行。  
  
5.  按一下 **[完成]** 。  
  
    比較隨即開始。  
  
    > [!NOTE]  
    > 您可以開啟 [SQL]  功能表、按一下 [資料比較]  ，然後按一下 [停止資料比較]  ，以停止進行中的資料比較作業。  
  
    比較完成時，您可以檢視兩個資料庫之間的資料差異。 您也可以更新目標資料庫中的部分或所有資料，以符合來源資料庫。  
  
#### <a name="to-compare-data-by-using-the-visual-studio-automation-model"></a>若要使用 Visual Studio Automation 模型來比較資料  
  
1.  開啟 [檢視]  功能表、指向 [其他視窗]  ，然後按一下 [命令視窗]  。  
  
2.  在 [命令視窗] 中輸入下列命令：  
  
    ```  
    Sql.NewDataComparison /SrcServerName sServerName /SrcDatabaseName sDatabaseName /SrcUserName sUserName /SrcPassword sPassword /SrcDisplayName sDisplayName /TargetServerName tServerName /TargetDatabaseName tDatabaseName /TargeUserName tUserName /TargetPassword tPassword /TargetDisplayName tDisplayName  
    ```  
  
    將預留位置 (*sServerName*、*sDatabaseName*、*sUserName*、*sPassword*、*sDisplayName*、*tServerName*、*tDatabaseName*、*tUserName*、*tPassword* 和 *tDisplayName*) 取代為來源和目標資料庫的值。  
  
    如果您沒有指定來源和目標，便會顯示 [新增資料比較]  對話方塊。 如需 Sql.NewDataComparison 命令參數的詳細資訊，請參閱 [Visual Studio Team System 資料庫功能的自動化命令參考](https://msdn.microsoft.com/library/dd470565.aspx)。  
  
    對指定的來源和目標資料庫中的資料進行比較。 在資料比較工作階段中顯示結果。 如需如何檢視結果或同步處理資料的詳細資訊，請參閱[檢視資料差異](#ViewDifferences)和[同步處理資料庫資料](#Synchronize)。  
  
## <a name="ViewDifferences"></a>檢視資料差異  
當您比較兩個資料庫的資料之後，[資料比較] 會列出所比較的每個「資料庫物件」  及其狀態。 您也可以檢視每個物件內記錄的結果 (依狀態分組)。 如需狀態指定的詳細資訊，請參閱[使用參考資料庫中的資料比較和同步處理一個或多個資料表中的資料](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)。  
  
當您檢視差異之後，可以針對不同、遺漏或新增的部分或所有物件或記錄，更新目標以符合來源。 如需詳細資訊，請參閱[同步處理資料庫資料](#Synchronize)。  
  
#### <a name="to-view-data-differences"></a>若要檢視資料差異  
  
1.  比較來源和目標資料庫的資料。 如需詳細資訊，請參閱[比較資料庫資料](#CompareDatabaseData)。  
  
2.  (選擇性) 執行下列其中一項或兩項作業：  
  
    -   根據預設，不論其狀態，所有物件的結果都會顯示。 若只要顯示具有特定狀態的物件，請按一下 [篩選]  清單中的選項。  
  
    -   若要檢視在特定物件內記錄的結果，請按一下主要結果窗格中的物件，然後按一下記錄檢視窗格的索引標籤。 每個索引標籤會顯示該物件中具有特定狀態的所有記錄：不同、僅限於來源、僅限於目標和相同。 資料會以記錄和資料行顯示。  
  
## <a name="Synchronize"></a>同步處理資料庫資料  
當您比較兩個資料庫的資料之後，可以更新目標的全部或部分以符合來源，進行同步處理。 您可以比較兩種資料庫物件中的資料：資料表和檢視表。  
  
#### <a name="to-update-target-data-by-using-the-write-updates-command"></a>若要利用寫入更新命令來更新目標資料  
  
1.  比較來源和目標資料庫的資料。 如需詳細資訊，請參閱[比較資料庫資料](#CompareDatabaseData)。  
  
    在比較完成之後，[資料比較] 視窗會列出比較物件的結果。 四個資料行 (名稱為 [不同的記錄]、[僅限於來源]、[僅限於目標] 和 [相同的記錄]) 顯示不同物件的資訊。 對於每個這類物件，這些資料行會顯示找到的不同記錄數目，以及更新作業將會變更的記錄數目。 這兩個數字最初相符，但是您可以在步驟 4 中變更要更新的物件。  
  
    如需詳細資訊，請參閱[使用參考資料庫中的資料比較和同步處理一個或多個資料表中的資料](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)。  
  
2.  在 [資料比較] 視窗中的資料表，按一下資料列。  
  
    針對資料庫物件中您按一下的記錄，詳細資料窗格會顯示其結果。 記錄會在索引標籤上依狀態分組，您可以用來指定要從來源散佈至目標的資料。  
  
3.  在詳細資料窗格中，按一下名稱包含數字非零 (0) 的索引標籤。  
  
    [僅限於目標]  資料表的 [更新]  資料行所包含的核取方塊，可用來選取所要更新的資料列。 根據預設，每個核取方塊都已選取。  
  
4.  對於您不要用來源資料更新的目標記錄，清除核取方塊。  
  
    當您清除核取方塊時，要更新的記錄數目會減少，而且顯示會變更以反映您的動作。 這個數目會顯示在詳細資料窗格中的狀態列以及在主要結果窗格中的對應資料行，如步驟 1 所述。  
  
5.  (選擇性) 按一下 [產生指令碼]  。  
  
    Transact\-SQL 編輯器視窗隨即開啟，並顯示用來更新目標的「資料操作語言」  (DML) 指令碼。  
  
6.  若要同步處理不同、遺漏或新增的記錄，請按一下 [更新物件]  。  
  
    > [!NOTE]  
    > 當目標資料庫更新時，您可以按一下 [停止寫入目標]  以取消作業。  
  
    系統會用來源中對應記錄的資料來更新目標中所選記錄的資料。  
  
    > [!NOTE]  
    > 如果您選擇更新索引檢視，當此動作導致重複索引鍵插入相同的資料表時，**更新目標**作業可能會失敗。  
  
#### <a name="to-update-target-data-by-using-a-transact-sql-script"></a>使用 Transact\-SQL 指令碼來更新目標資料  
  
1.  比較來源和目標資料庫的資料。 如需詳細資訊，請參閱[比較資料庫資料](#CompareDatabaseData)。  
  
    在比較完成之後，[資料比較] 視窗會列出比較的物件。 如需詳細資訊，請參閱[使用參考資料庫中的資料比較和同步處理一個或多個資料表中的資料](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)。  
  
2.  (選擇性) 在詳細資料窗格中，對於您不要更新的記錄清除核取方塊，如先前的程序所述。  
  
3.  按一下 [產生指令碼]  。  
  
    新視窗會顯示 Transact\-SQL 指令碼，可用來散佈讓目標資料符合來源資料所需的變更。 系統會為新視窗指定名稱，例如 **DataUpdate_Database_1.sql**。  
  
    這個指令碼反映您在詳細資料窗格中所做的變更。 例如，您可能已經在 [僅限於目標] 頁面中清除 [dbo].[Shippers] 資料表特定資料列的核取方塊。 在這種情況下，指令碼不會更新該資料列。  
  
4.  (選擇性) 在 **DataUpdate_Database_1.sql** 視窗中編輯這個指令碼。  
  
5.  (選擇性但建議) 備份目標資料庫。  
  
6.  按一下 [執行]  ，以更新目標資料庫。  
  
    指定要更新之目標資料庫的連接。  
  
    > [!IMPORTANT]  
    > 根據預設，在交易範圍內進行更新。 如果發生錯誤，可以回復整個更新。 您可以變更此行為。  
  
    系統會用來源中對應記錄的資料來更新目標中所選記錄的資料。  
  
## <a name="see-also"></a>另請參閱  
[使用參考資料庫中的資料比較和同步處理一個或多個資料表中的資料](../ssdt/compare-and-synchronize-data-in-tables-with-data-in-reference-database.md)  
  
