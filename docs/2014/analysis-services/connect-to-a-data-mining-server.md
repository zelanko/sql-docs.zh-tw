---
title: 連接到資料採礦伺服器 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
- getting started
ms.assetid: 85962ad6-d840-4bc6-905e-c667c3276944
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3c9abd1b891d47f1711db21eec017ec755526e02
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087351"
---
# <a name="connect-to-a-data-mining-server"></a>連接到資料採礦伺服器
  ![連接按鈕](media/misc-connection.gif "連接按鈕")  
  
 按一下 [**連接**] 按鈕，以選取現有的連接，或建立與實例的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]新連接。  
  
 **為什麼需要連接到伺服器？**  
  
 當您建立連接時，便能讓您使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器所提供的資料採礦演算法，以及利用伺服器的最佳化處理。  
  
 您並不需要將資料或結果保存在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫，或是 SQL Server 資料庫中。 Excel 資料採礦增益集只能和儲存在 Excel 中的資料搭配使用，或是和您以 Excel 資料來源的方式所連接的資料搭配使用。  
  
## <a name="how-to-create-a-new-connection"></a>如何建立新的連接  
  
1.  按一下 [**連接**] 按鈕。  
  
2.  在 [ **Analysis Services 連接**] 對話方塊中，按一下 [**新增**]。  
  
3.  在 [**連接到 Analysis Services** ] 對話方塊中，輸入伺服器名稱。  
  
4.  指定驗證方法。  
  
5.  指定將在其中存放資料採礦模型的目錄或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫。  
  
    > [!NOTE]  
    >  如果您尚未建立任何資料庫，則可以使用 (預設值) 建立連接再加以測試；不過，您不能將採礦模型加入至預設連接。 在建立任何採礦模型之前，應該先與現有的資料庫建立連接。  
  
6.  如果您是透過 Web 服務連接到伺服器，請輸入 Web 服務所需要的使用者名稱和密碼。  
  
7.  輸入新連接的易記名稱。  
  
8.  按一下 [**測試連接**]，確認伺服器可供使用。  
  
## <a name="troubleshooting-connections"></a>疑難排解連接  
 本節將提供有關連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的一些常見問題的解答。  
  
 **我收到一則訊息，指出「找不到連接」。**  
  
 如果按鈕下半部的文字顯示 [**沒有連接**]，表示您沒有建立[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料庫的連接，或連接失敗。 您可以繼續從 Access 或其他來源使用 Excel 中的資料，但是若要建立資料採礦模型或執行預測查詢，便必須要有使用中的連接。  
  
 **假設我沒有使用伺服器的許可權嗎？**  
  
 如果您沒有足夠的權限將採礦模型存放在伺服器上，或是想要對資料採礦進行實驗而不要儲存工作，則可以使用資料表分析工具建立暫時性資料結構和暫時性模型。 您仍然需要能夠將暫時性模型存放在伺服器上。 請要求您的系統管理員啟用伺服器上的*會話採礦模型*使用。  
  
 若要確保儲存您的模型，您可以將使用暫時性模型的選項停用，或者也可使用資料採礦用戶端所提供的精靈。 這些精靈會將所有模型儲存在伺服器上。 您需要對儲存模型的資料庫具備系統管理存取權，因此建議您請系統管理員為使用增益集所建立的採礦模型建立一個專用的資料庫。  
  
 **我的連接中斷了，這樣是否會遺失我所有的工作成果？**  
  
 如果您終止與伺服器的連接，您的結果與資料並不會遺失，因為它們是儲存在 Excel 中。 不過，如果您建立了一些暫時性模型，則過不久後就會從伺服器中刪除這些模型。 因此，如果您暫時失去連線，就不會刪除模型。  
  
 任何產生的資料或結果都不會遺失，因為所有報表和資料表都是儲存在 Excel 中。  
  
> [!NOTE]  
>  當增益集與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器進行通訊時，請勿中斷與伺服器或網路的連接。 例如，絕不要在建立模型或處理資料時中斷連接。 在某些情況下，您的資料可能會因而損毀。  
  
 **我無法使用 Visio 工具連接到模型**  
  
 適用於 Visio 的資料採礦範本無法使用暫存採礦結構和模型。 若要建立採礦模型的圖表，此模型必須存放在伺服器上。  
  
 **如何監視連接的使用方式？**  
  
 [適用于 Excel&#41;工具 &#40;資料採礦用戶端的追蹤](trace-data-mining-client-for-excel.md)會在增益集與指定的伺服器之間建立所有活動的記錄檔。  
  
 若要啟用會話模型的監視，請在 [**追蹤**] 對話方塊中選取 [**使用會話模型**] 選項。  
  
 追蹤可讓您檢視模型和結構建立時所產生的 DMX 和 XMLA 命令。 您也可以檢視用戶端所傳送的查詢，藉此在 Excel 中產生結果和報表。  
  
 **什麼是暫時性模型？如何儲存暫時性模型？**  
  
 適用於 Excel 的資料表分析工具預設會建立暫時性資料結構和採礦模型。 只要將活頁簿保持開啟，而且不中斷與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的連接，就可以繼續瀏覽及查詢暫時性模型。  
  
 如果關閉 Excel 活頁簿或變更或是結束與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的連接，您所建立的結構與模型就會遭到刪除。  
  
 當您完成適用於 Excel 的資料採礦用戶端所提供的精靈時，模型預設會儲存至伺服器，但在每個精靈的最後一頁都會有可讓您使用暫時性模型的選項。 如果選取了這個選項，您所建立的資料採礦結構和模型都會存放在暫存檔中。 只要 Excel 維持開啟狀態，您就能夠瀏覽、管理及修改結構與模型。 但是，一旦您關閉 Excel 後，結構和所有相關的模型便會遭到刪除。  
  
 您也可以使用 [**資料採礦] [高級查詢編輯器**]，並選取其中一個 DMX 範本，以明確建立暫存結構或模型。 加入 `USE SESSION MODELS` 子句以指定物件是暫時性的。   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>建立採礦模型和結構的備份  
 若要建立模型或結構的備份，您可以在適用于 Excel 的資料採礦用戶端中，使用 [[管理模型] &#40;SQL Server 資料採礦增益集&#41;](manage-models-sql-server-data-mining-add-ins.md)進行匯出。  
  
 如果您建立的是暫時性採礦模型，它通常會有一個很難理解的名稱，例如 Table5_593679_TS_62446。 不過，您可以使用[追蹤 &#40;適用于 Excel 的資料採礦用戶端&#41;](trace-data-mining-client-for-excel.md)工具來探索資料表分析工具所建立之暫存結構和模型的名稱，然後使用 [**管理模型**] 加以備份。  
  
##### <a name="identify-and-export-a-temporary-model"></a>識別及匯出暫時性模型  
  
1.  在適用于 Excel 的資料採礦用戶端的 [**連接**] 群組中，按一下 [**追蹤**]。  
  
2.  檢視連接活動記錄檔，並透過檢閱資料行和可預測的輸出找出模型 (舉例來說)。  
  
     進階使用者：如果您很熟悉 DMX 或 XMLA，可以將陳述式複製到檔案以供稍後使用。  
  
3.  當您找到暫時模型和結構的名稱時，請開啟 [**管理模型**] 並選取模型。  
  
4.  按一下 [匯出這個採礦模型]，在您指定的位置產生指令碼檔案。  
  
## <a name="see-also"></a>另請參閱  
 [連接到來源資料 &#40;適用于 Excel 的資料採礦用戶端&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [伺服器設定公用程式 &#40;適用于 Excel 的資料採礦增益集&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
