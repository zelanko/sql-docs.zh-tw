---
title: 工作 1： 建立知識庫和定義域 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9114289ed2a4e09a5f7b59ed016c553c1d225dfc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226578"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>工作 1：建立知識庫和定義域
  在這個工作中，您會建立**供應商**知識庫，並建立用來清理資料和比對資料以移除重複項的網域。  
  
1.  啟動**Data Quality Client**。 按一下 **開始**，指向**所有程式**，按一下  **Microsoft SQL Server 2012**，按一下  **Data Quality Services**，然後按一下**Data Quality Client**。  
  
2.  在 **連接到伺服器**對話方塊方塊中，選取 資料庫伺服器執行個體，DQS 已安裝，並按一下**Connect**。  
  
     ![連接到伺服器 對話方塊](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "連接到伺服器 對話方塊")  
  
3.  在 Data Quality Client 首頁上，在**知識庫管理**窗格中，按一下**新知識庫的基礎**。  
  
     ![知識庫管理-新增知識庫](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "知識庫管理-新增知識庫")  
  
4.  請輸入**供應商**for**名稱**的知識庫。  
  
     ![新增知識庫-定義域管理](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "新增知識庫-定義域管理")  
  
5.  確認**建立知識庫來源**欄位設定為**無**由於您會建立**供應商**從頭的知識庫。  
  
6.  確認**定義域管理**選取**活動**然後按一下**下一步**。 [定義域管理] 活動可讓您在知識庫中建立和管理定義域。  
  
7.  在 [**定義域管理**] 視窗中，按一下**建立網域**工具列按鈕，以建立定義域。  
  
     ![建立定義域 工具列按鈕](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "建立定義域 工具列按鈕")  
  
8.  中**建立定義域** 對話方塊中，輸入**Supplier ID**如**網域名稱**，然後按一下**確定**。  
  
     ![建立定義域 對話方塊](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "建立定義域 對話方塊")  
  
9. 重複上述步驟來建立以下包含所有預設值的定義域。 若要簡化本教學課程，您設定**資料型別**做為所有的網域**字串**。 其他允許的資料類型包括：整數、小數和日期。 當**使用前置值**選項是選取 （預設值），所有同義字會都取代在輸出中同義字群組的前置值。 設定**將字串標準化**選項 （預設值） 會移除定義域值中的任何特殊字元。 **輸出格式為**選項可讓您選取的網域中的資料值為輸出時所套用的格式。 選取 **啟用拼字檢查**擴展定義域時，針對所有字串值執行拼字檢查 （預設值）。 **語言**設定會指定哪一個語言版本**拼字檢查**您想要套用。 選取 **停用語法錯誤演算法**來擴展定義域，而不檢查字串值的語法錯誤。 請參閱[建立網域](http://msdn.microsoft.com/library/hh510401.aspx)如需詳細資訊的 MSDN library 中的主題。  
  
    -   Supplier Name  
  
    -   Contact Email  
  
    -   [地址行]  
  
    -   [縣/市]  
  
    -   State  
  
    -   Country  
  
    -   [郵遞區號]  
  
## <a name="next-step"></a>下一個步驟  
 [工作 2：手動新增定義域值](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
