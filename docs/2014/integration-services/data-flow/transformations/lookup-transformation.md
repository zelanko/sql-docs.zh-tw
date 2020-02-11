---
title: 查閱轉換 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptrans.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47b04c547700eda94d4c4f19b4a1211f8cdbf694
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62900221"
---
# <a name="lookup-transformation"></a>查閱轉換
  「查閱」轉換會藉由聯結輸入資料行中的資料與參考資料集中的資料行來執行查閱。 您可以使用查閱在相關資料表中存取以通用資料行中的值為基礎的其他資訊。  
  
 參考資料集可以是快取檔案、現有的資料表或檢視、新資料表或 SQL 查詢的結果。 「查閱」轉換會使用 OLE DB 連接管理員或快取連接管理員來連接到參考資料集。 如需詳細資訊，請參閱 [OLE DB 連線管理員](../../connection-manager/ole-db-connection-manager.md) 和 [快取連線管理員](../../connection-manager/cache-connection-manager.md)  
  
 您可以利用下列方式設定「查閱」轉換：  
  
-   選取您要使用的連接管理員。 如果想要連接到資料庫，請選取 OLE DB 連接管理員。 如果想要連接到快取檔案，請選取快取連接管理員。  
  
-   指定包含參考資料集的資料表或檢視。  
  
-   藉由指定 SQL 陳述式產生參考資料集。  
  
-   指定輸入與參考資料集之間的聯結。  
  
-   從參考資料集將資料行加入至「查閱」轉換輸出。  
  
-   設定快取選項。  
  
 「查閱」轉換支援下列 OLE DB 連接管理員的資料提供者：  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 「查閱」轉換會嘗試在轉換輸入的值與參考資料集的值之間執行等聯結 (Equi-Join)  (等聯結表示轉換輸入中的各資料列，必須至少符合參考資料集中的某個資料列)。如果無法執行等聯結，則「查閱」轉換會執行下列其中一項動作：  
  
-   如果參考資料集中沒有相符的項目，則不會發生聯結。 根據預設，「查閱」轉換會將沒有相符項目的資料列視為錯誤； 不過，您可以設定「查閱」轉換，以將這些資料列重新導向至無相符結果輸出。 如需詳細資訊，請參閱[查閱轉換編輯器 &#40;一般頁面&#41;](../../lookup-transformation-editor-general-page.md) 和[查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../../lookup-transformation-editor-error-output-page.md)。  
  
-   如果參考資料表中有多個相符項目，「查閱」轉換將只傳回查閱查詢所傳回的第一個相符項目。 如果找到多個相符項目，則「查閱」轉換只會在已設定為將所有參考資料集載入至快取時才產生錯誤或警告。 在這種情況下，「查閱」轉換會在轉換填滿快取時偵測到多個相符項目時產生警告。  
  
 聯結可以是複合聯結，表示您可以將轉換輸入中的多個資料行聯結至參考資料集中的資料行。 轉換支援聯結任何資料類型的資料行，但 DT_R4、DT_R8、DT_TEXT、DT_NTEXT 或 DT_IMAG 除外。 如需詳細資訊，請參閱[Integration Services 資料類型](../integration-services-data-types.md)。  
  
 通常參考資料集的值會加入至轉換輸出。 例如，「查閱」轉換可從使用輸出資料行之值的資料表擷取產品名稱，然後將產品名稱加入至轉換輸出。 參考資料表的值可取代資料行的值，或者可加入至新的資料行。  
  
 「查閱」轉換執行的查閱區分大小寫。 若要避免由於資料中的大小寫不同而造成查閱失敗，請先使用「字元對應」轉換將資料轉換成大寫或小寫， 然後在產生參考資料表的 SQL 陳述式中包含 UPPER 或 LOWER 函數。 如需詳細資訊，請參閱[字元對應轉換](character-map-transformation.md)、[UPPER &#40;Transact-SQL&#41;](/sql/t-sql/functions/upper-transact-sql) 和 [LOWER &#40;Transact-SQL&#41;](/sql/t-sql/functions/lower-transact-sql)。  
  
 「查閱」轉換具有下列的輸入和輸出：  
  
-   輸入。  
  
-   相符結果輸出。 相符結果輸出會處理轉換輸入中，至少符合參考資料集中一個項目的資料列。  
  
-   無相符結果輸出。 無相符結果輸出會處理輸入中沒有至少符合參考資料集中一個項目的資料列。 如果將「查閱」轉換設定為把沒有相符項目的資料列視為錯誤，則這些資料列會重新導向至錯誤輸出； 否則，轉換會將這些資料列重新導向至無相符結果輸出。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)] 中，「查閱」轉換僅具有一個輸出： 如需如何執行在中[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]建立之查閱轉換的詳細資訊，請參閱[升級查閱轉換](../../../sql-server/install/upgrade-lookup-transformations.md)。  
  
-   錯誤輸出。  
  
## <a name="caching-the-reference-dataset"></a>快取參考資料集  
 記憶體中的快取會儲存參考資料集，並儲存編列資料索引的雜湊資料表。 在完成封裝的執行之前，快取都會保留在記憶體中。 您可以將快取保存至快取檔案 (.caw)。  
  
 將快取保存至檔案後，系統就可以更快地載入快取。 如此可改善「查閱」轉換和封裝的效能。 請記住，當您使用快取檔案時，所使用的資料並不如資料庫中的資料新。  
  
 下列是將快取保存至檔案的其他優點：  
  
-   ***在多個封裝之間共用快取檔案。如需詳細資訊，請參閱***  [使用快取連線管理員以完整快取模式來執行查閱轉換](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***。***  
  
-   使用封裝部署快取檔案， ***然後您可以在多部電腦上使用資料。*** 如需詳細資訊，請參閱 [針對查閱轉換來建立及部署快取](create-and-deploy-a-cache-for-the-lookup-transformation.md)。  
  
-   使用「原始檔案」來源從快取檔案讀取資料， 接著就可以使用其他的資料流程元件來轉換或移動資料。 如需相關資訊，請參閱 [Raw File Source](../raw-file-source.md)。  
  
    > [!NOTE]  
    >  快取連接管理員不支援使用「原始檔案」目的地所建立或修改的快取檔案。  
  
-   使用「檔案系統」工作在快取檔案上執行作業和設定屬性。 如需詳細資訊，請參閱 [檔案系統工作](../../control-flow/file-system-task.md)。  
  
 下列是快取選項：  
  
-   參考資料集是藉由執行「查閱」轉換之前使用資料表、檢視或 SQL 查詢而產生並載入快取。 您可以使用 OLE DB 連接管理員來存取資料集。  
  
     此快取選項與 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中用於「查閱」轉換的完整快取選項相容。  
  
-   參考資料集是從資料流程中已連接的資料來源或從快取檔案產生，然後在「查閱」轉換執行之前載入至快取。 您可以使用快取連接管理員或是快取轉換來存取資料集。 如需詳細資訊，請參閱 [快取連線管理員](../../connection-manager/cache-connection-manager.md) 和 [快取轉換](cache-transform.md)。  
  
-   參考資料集是藉由在執行「查閱」轉換期間使用資料表、檢視或 SQL 查詢而產生。 在參考資料集中具有相符項目的資料列，以及在資料集中沒有相符項目的資料列，都可以載入至快取。  
  
     超過快取的記憶體大小時，查閱轉換會自動從快取中移除最不常用的資料列。  
  
     此快取選項與 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中用於「查閱」轉換的部分快取選項相容。  
  
-   參考資料集是藉由在執行「查閱」轉換期間使用資料表、檢視或 SQL 查詢而產生。 不會將任何資料存入快取。  
  
     此快取選項與 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中用於「查閱」轉換的無快取選項相容。  
  
 
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的差異在於比較字串的方式。 如果「查閱」轉換是設定為在執行之前將參考資料集載入至快取，則 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 會在快取中進行查閱比較。 否則，查閱作業會使用參數化的 SQL 陳述式而由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行查閱比較。 這表示「查閱」轉換可能會根據快取類型，從相同的查閱資料表傳回不同數目的相符項目。  
  
## <a name="related-tasks"></a>相關工作  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。 如需進一步詳細資訊，請參閱下列主題。  
  
-   [以沒有快取或部分快取模式實作查閱](implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [使用快取連線管理員以完整快取模式實作查閱轉換](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [使用 OLE DB 連接管理員，以完整快取模式來實作查閱轉換](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [設定資料流程元件的屬性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相關內容  
  
-   位於 msdn.microsoft.com 的影片： [如何：在完整快取模式中實作查閱轉換 (SQL Server 影片)](https://go.microsoft.com/fwlink/?LinkId=131031)  
  
-   位於 blogs.msdn.com 的部落格項目： [Best Practices for Using the Lookup Transformation Cache Modes](https://go.microsoft.com/fwlink/?LinkId=146623)(使用查閱轉換快取模式的最佳做法)  
  
-   位於 blogs.msdn.com 的部落格項目： [Lookup Pattern: Case Insensitive](https://go.microsoft.com/fwlink/?LinkId=157782)(查閱模式：不區分案例)  
  
-   位於 msftisprodsamples.codeplex.com 上的範例： [Lookup Transformation](https://go.microsoft.com/fwlink/?LinkId=267528)(查閱轉換)。  
  
     如需安裝 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 產品範例和範例資料庫的資訊，請參閱 [SQL Server Integration Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=267527)(SQL Server Integration Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [模糊查閱轉換](fuzzy-lookup-transformation.md)   
 [詞彙查閱轉換](term-lookup-transformation.md)   
 [資料流程](../data-flow.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
