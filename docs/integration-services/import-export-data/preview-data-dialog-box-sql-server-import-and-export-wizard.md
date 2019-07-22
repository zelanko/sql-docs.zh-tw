---
title: 預覽資料對話方塊 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b766a1615e0dd75efca5a47dca7f4d0dcab553b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901794"
---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>預覽資料對話方塊 (SQL Server 匯入和匯出精靈)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  指定您想要複製的資料之後，即可選擇性地按一下 [預覽]  開啟 [預覽資料]  對話方塊。 在此頁面上，您最多可以預覽 200 筆資料來源的取樣資料列。 這會確認精靈即將複製您想要複製的資料。
  
## <a name="screen-shot-of-the-preview-data-page"></a>[預覽資料] 頁面的螢幕擷取畫面 
 下列螢幕擷取畫面顯示精靈的 [預覽資料]  對話方塊。  
 
![[匯入和匯出精靈] 的 [預覽資料] 頁面](../../integration-services/import-export-data/media/preview-data.png "[匯入和匯出精靈] 的 [預覽資料] 頁面")  
  
## <a name="preview-sample-data"></a>預覽取樣資料  
 **Source**  
顯示精靈用來從資料來源載入資料的查詢。

如果您選取要複製的資料表，[來源]  欄位會顯示 `SELECT * FROM <table>` 查詢，而不是資料表名稱。 
  
 **取樣資料方格**  
 最多顯示 200 筆查詢從資料來源傳回之取樣資料的資料列。  


## <a name="thats-not-right-i-want-to-change-something"></a>不正確，我想要進行變更
在您預覽資料之後，可能會想要變更已在精靈的先前頁面上選取的選項。 若要執行這些變更，請按一下 [確定]  回到 [選取來源資料表和檢視表]  頁面，然後按一下 [上一步]  回到可以變更選取項目的頁面。

## <a name="whats-next"></a>下一步  
 預覽您即將複製的資料並按一下 [確定]  之後，[預覽資料]  對話方塊會將您帶回 [選取來源資料表和檢視]  頁面或 [設定一般檔案目的地]  頁面。 如需詳細資訊，請參閱 [選取來源資料表和檢視](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 或 [設定一般檔案目的地](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="see-also"></a>另請參閱
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)
