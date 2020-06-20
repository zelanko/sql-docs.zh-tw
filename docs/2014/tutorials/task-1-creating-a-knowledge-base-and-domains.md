---
title: 工作1：建立知識庫和定義域 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f7ad3b085178c0d0cfe3ece010a571992e7fdb99
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064854"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>工作 1：建立知識庫和定義域
  在這項工作中，您會建立**供應商**知識庫，並建立用於清理資料和比對資料以移除重複專案的定義域。  
  
1.  啟動**Data Quality Client**。 按一下 [**開始**]，指向 [**所有程式**]，按一下 [ **Microsoft SQL Server 2012**，按一下 [ **Data Quality Services**]，然後按一下 [ **Data Quality Client**]。  
  
2.  在 [**連接到伺服器**] 對話方塊中，選取安裝 DQS 的資料庫伺服器實例，然後按一下 [**連接]**。  
  
     ![[連接到伺服器] 對話方塊](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "連接到伺服器對話方塊")  
  
3.  在 [Data Quality Client] 首頁的 [**知識庫管理**] 窗格中，按一下 [**新增知識庫**]。  
  
     ![知識庫管理 - 新增知識庫](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "知識庫管理 - 新增知識庫")  
  
4.  輸入 [**供應商**] 做為知識庫的**名稱**。  
  
     ![新增知識庫 - 定義域管理](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "新增知識庫 - 定義域管理")  
  
5.  確認 [**從欄位建立知識庫**] 設定為 [**無**]，因為您是從頭開始建立**供應商**知識庫。  
  
6.  確認已針對**活動**選取 [**定義域管理**]，然後按 **[下一步]**。 [定義域管理] 活動可讓您在知識庫中建立和管理定義域。  
  
7.  在 [**定義域管理**] 視窗中，按一下 [**建立定義域**] 工具列按鈕來建立定義域。  
  
     ![[建立定義域] 工具列按鈕](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "[建立定義域] 工具列按鈕")  
  
8.  在 [**建立定義域**] 對話方塊中，輸入 [**供應商識別碼**] 作為 [**功能變數名稱**]，然後按一下 **[確定]**。  
  
     ![[建立定義域] 對話方塊](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "[建立定義域] 對話方塊")  
  
9. 重複上述步驟來建立以下包含所有預設值的定義域。 為了讓教學課程保持簡單，您可以將所有定義域的**資料類型**設定為 [**字串**]。 其他允許的資料類型包括：整數、小數和日期。 當選取 [**使用前置值**] 選項時（預設值），所有同義字都會取代為輸出中同義字群組的前置值。 設定正規化**字串**選項（預設值）會移除定義域值中的任何特殊字元。 [**格式化輸出至**] 選項可讓您選取當定義域中的資料值為輸出時所套用的格式。 選取 [**啟用檢查**器] （預設），以在擴展定義域時對所有字串值執行拼寫檢查。 [**語言**] 設定會指定您想要套用之**拼寫**器的語言版本。 選取 [**停用語法錯誤演算法**] 以填入定義域，而不檢查字串值是否有語法錯誤。 如需詳細資訊，請參閱 MSDN library 中的[建立網域](https://msdn.microsoft.com/library/hh510401.aspx)主題。  
  
    -   Supplier Name  
  
    -   連絡人電子郵件  
  
    -   [地址行]  
  
    -   City  
  
    -   State  
  
    -   Country  
  
    -   Zip  
  
## <a name="next-step"></a>後續步驟  
 [工作 2：手動新增定義域值](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
