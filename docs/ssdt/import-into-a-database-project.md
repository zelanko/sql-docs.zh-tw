---
title: 匯入資料庫專案中 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLPROJECTIMPORTSNAPSHOTSUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.SQLPROJECTIMPORTDATABASESUMMARYDIALOG.DIALOG
- SQL.DATA.TOOLS.IMPORTSCRIPTWIZARD.SUMMARY
ms.assetid: d0a0a394-6cb6-416a-a25f-9babf8ba294a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d2c08af731fc8f75089250c92ec4f0912a96eee6
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65099578"
---
# <a name="import-into-a-database-project"></a>匯入資料庫專案中
您可以使用 [匯入]，將即時資料庫或 .dacpac 中的新物件填入專案，或者使用指令碼中的新定義來更新專案中的現有物件。 這三種路徑之間存在一些需要注意的行為差異，下面將詳細說明。  
  
**匯入功能表**  
  
![SSDT 匯入功能表](../ssdt/media/ssdt-import.gif "SSDT 匯入功能表")  
  
**本主題的章節**  
  
[匯入來源：資料庫或資料層應用程式 (*.dacpac)](#bkmk_import_source_db)  
  
[匯入來源：指令碼 (*.sql)](#bkmk_import_source_script)  
  
[匯入加密的物件](#bkmk_import_encrypted)  
  
## <a name="bkmk_import_source_db"></a>匯入來源：資料庫或資料層應用程式 (*.dacpac)  
只有當專案尚未定義任何結構描述物件時，才能使用從資料庫或 .dacpac 檔案匯入結構描述的功能。 這不包括 RefactorLog 或預先部署/部署後指令碼。  
  
匯入時，系統會針對新物件使用 SSDT 的組織預設，將物件定義編碼成專案檔：新檔案代表最上層物件、階層子系與父系定義於相同的檔案中，並且盡可能以內嵌方式定義資料表/資料行條件約束。 如需提高每個物件的目標可見性和控制能力，請使用 [結構描述比較] 而非 [匯入]。  
  
如果匯入來源包含預先部署和部署後指令碼、RefactorLog 或 SQLCMD 變數定義，它們將匯入專案中。 如果專案已經包含上述任何一種成品，匯入的檔案將加入至專案中的 [匯入時忽略] 資料夾。  
  
**匯入時忽略資料夾**  
  
![SSDT 匯入時忽略資料夾](../ssdt/media/ssdt-ignoredonimport.gif "SSDT 匯入時忽略資料夾")  
  
## <a name="bkmk_import_source_script"></a>匯入來源：指令碼 (*.sql)  
系統會加入來自匯入來源但原本「不」存在專案中的所有物件，而位於匯入來源且「已經」存在專案中的所有物件都將覆寫專案中的物件定義。  
  
> [!NOTE]  
> 這種路徑存在兩個已知錯誤，將於未來的版本修正：  
>   
> -   如果資料表/資料行條件約束定義於專案資料表定義中的 CREATE TABLE 陳述式外部，匯入作業將會覆寫資料表定義，讓條件約束成為內嵌條件約束。 不過，它將保留外部條件約束，因此會在專案中產生重複的條件約束。  
> -   來自來源指令碼且已經存在專案中的任何主要金鑰或資料庫加密金鑰將在匯入時進行複製。 請移除重複項目以便建置專案。  
  
「從指令碼匯入」程序不包含預先部署/部署後指令碼、SQLCMD 變數或 RefactorLog 檔案。 如果系統在匯入時偵測到上述和任何其他不支援的建構，就會將它們放入專案之 [指令碼] 資料夾中的 **ScriptsIgnoredOnImport.sql** 檔案。  
  
 
## <a name="bkmk_import_encrypted"></a>匯入加密的物件  
將加密的物件匯入資料庫專案時，不一定能夠從伺服器擷取物件定義的完整主體。 因此，在處理這個類別的物件時，匯入行為可能有所不同。  
  
無法擷取完整主體定義時，系統會編寫物件頁首/頁尾以及虛擬主體的指令碼。 當您匯入或使用 [結構描述比較] 時，如果來源是即時資料庫或擷取自資料庫的 .dacpac，可能就會出現這種行為。  
  
**包含虛擬主體的指令碼**  
  
![包含虛擬主體的指令碼](../ssdt/media/ssdt-procwithencryption.gif "包含虛擬主體的指令碼")  
  
如果完整物件定義可用且可擷取，[匯入] 和 [結構描述比較] 就會將它完全帶入專案中。 當您從指令碼、建置自資料庫專案的 .dacpac 或另一個資料庫專案更新專案時，就會出現這種行為。  
  
