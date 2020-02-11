---
title: 建立及管理表格式模型資料分割（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 72c5b69aee10d8ac1342b3f037d76ab6ef5fc36c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66067395"
---
# <a name="create-and-manage-tabular-model-partitions-ssas-tabular"></a>建立及管理表格式模型資料分割 (SSAS 表格式)
  分割區會將一個資料表分割成多個邏輯部分。 接著，每個分割區可以不受其他分割區的影響，單獨處理 (重新整理)。 模型撰寫期間，在已部署的模型中有重複定義的模型資料分割。 部署之後，即可使用 ** 的 [資料分割]**[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 對話方塊或指令碼，管理這些資料分割。 此主題提供的工作描述如何為已部署的模型建立及管理資料分割。  
  
 本主題也包括下列工作：  
  
-   [若要建立新的磁碟分割](#bkmk_create_new)  
  
-   [複製資料分割](#bkmk_copy)  
  
-   [合併兩個以上的分割區](#bkmk_merge)  
  
-   [若要刪除資料分割](#bkmk_delete)  
  
## <a name="tasks"></a>工作  
 若要為已部署的表格式模型資料庫建立及管理資料分割，您可以使用 ** 中的 [資料分割]**[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 對話方塊。 若要檢視 ** [資料分割]**[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 對話方塊，請以滑鼠右鍵按一下資料表，然後按一下 [資料分割]****。  
  
###  <a name="bkmk_create_new"></a>若要建立新的磁碟分割  
  
1.  在 [資料分割]**** 對話方塊中，按一下 [新增]**** 按鈕。  
  
2.  在 **[資料分割名稱]** 中，輸入資料分割的名稱。 依預設，每個新資料分割的預設資料分割名稱是以累加的方式進行編號。  
  
3.  在 [SQL 陳述式]**** 中，於查詢視窗內輸入或貼上 SQL 查詢陳述式，以定義您要包含在資料分割中的資料行及任何子句。  
  
4.  若要驗證陳述式，請按一下 [檢查語法]****。  
  
###  <a name="bkmk_copy"></a>複製資料分割  
  
1.  在 [資料分割]**** 對話方塊的 [資料分割]**** 清單中，選取您要複製的資料分割，然後按一下 [複製]**** 按鈕。  
  
2.  在 **[資料分割名稱]** 中，輸入資料分割的新名稱。  
  
3.  在 [SQL 陳述式]**** 中，編輯 SQL 查詢陳述式。  
  
###  <a name="bkmk_merge"></a>合併兩個以上的分割區  
  
-   在 [資料**分割] 對話方塊的 [** 資料分割 **] 清單中**，使用 Ctrl + 按一下來選取您要合併的資料分割，然後按一下 [**合併**] 按鈕。  
  
> [!IMPORTANT]  
>  合併資料分割並不會更新資料分割中繼資料。 管理員必須針對產生的資料分割改變 SQL 陳述式，以確保處理作業會處理合併之資料分割中的所有資料。  
  
###  <a name="bkmk_delete"></a>若要刪除資料分割  
  
-   在 [資料分割]**** 對話方塊的 [資料分割]**** 清單中，選取您要刪除的資料分割，然後按一下 [刪除]**** 按鈕。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型資料分割 &#40;SSAS 表格式&#41;](partitions-ssas-tabular.md)   
 [處理 &#40;SSAS 表格式&#41;的表格式模型資料分割](process-tabular-model-partitions-ssas-tabular.md)  
  
  
