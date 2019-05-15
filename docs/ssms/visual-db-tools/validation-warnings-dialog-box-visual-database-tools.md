---
title: 驗證警告對話方塊 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 77a20360718563f101b44e68bf287e59876d8d38
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65098553"
---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>驗證警告對話方塊 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
如果您嘗試儲存可能具有損壞性副作用 (Side Effect) 的修改，或是資料庫認可操作可能失敗時，便會出現此對話方塊。 此會對話方塊指出有哪些可能的副作用，或是認可操作可能失敗的原因。 它可讓您選擇繼續執行修改或取消操作。  
  
> [!NOTE]  
> 當您嘗試將所做的修改傳輸至資料庫時，或當您儲存變更指令碼時，便會出現此對話方塊。  
  
下列任何一個原因都會使這個對話方塊出現：  
  
-   您可能沒有可以認可所有修改的資料庫權限。  
  
-   您的修改會導致不適當形成的衍生資料行、預設條件約束或檢查條件約束。  
  
-   對資料行的資料類型所做的修改可能造成資料遺失。  
  
-   某項修改會導致索引大於 900 個位元組。  
  
-   某項修改會變更提供結構描述繫結檢視或使用者定義函數的資料表或資料行。  
  
-   某項修改會導致重新建立資料表，該資料表具有一或多個加密的觸發程序；觸發程序將被卸除。  
  
-   您的修改會使一個資料表中的資料行，產生需要特別注意的 ANSI_NULLS、ANSI_PADDING 或兩者的設定。  
  
## <a name="options"></a>選項。  
**是**  
繼續執行作業並產生變更指令碼，或將修改內容傳輸至資料庫。 如果您沒有修改資料庫的權限、如果您的修改將導致索引大於 900 個位元組，或者如果您的修改將導致不適當形成的計算資料行、預設條件約束或檢查條件約束，則認可操作仍然可能失敗。  
  
**否**  
取消儲存動作。  
  
**儲存為文字檔**  
顯示 [另存新檔] 對話方塊，您可在此為包含警告清單的文字檔指定一個位置。  
  
## <a name="see-also"></a>另請參閱  
[設計資料表 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
